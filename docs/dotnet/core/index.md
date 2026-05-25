# 색인

- 원문 저장소: `microsoft/autogen`
- 미러 저장소: `martinlee-git/autogen`
- 원문 문서: https://github.com/microsoft/autogen/blob/main/docs/dotnet/core/index.md
- 미러 경로: `docs/dotnet/core/index.md`

## 한글 요약

AutoGen Core AutoGen Core for .NET은 Python 대응 항목과 동일한 개념 및 규칙을 따릅니다. 실제로 .NET 버전의 개념을 이해하려면 먼저 Python 설명서를 읽어 보는 것이 좋습니다. 달리 명시하지 않는 한 Python 버전의 개념은 .NET에 매핑됩니다. 언어 버전 간의 중요한 차이점은 Python과의 차이점 섹션에 설명되어 있습니다. 종속성 주입이나 호스트 빌더 패턴과 같이 특정 언어에만 영향을 미치는 항목의 경우 차이점 문서에 지정되지 않습니다. 시작하기 SDK를 너겟 패키지로 얻거나 저장소를 복제하여 얻을 수 있습니다. SDK는 NuGet에서 사용할 수 있습니다. 최소한 다음 사항이 필요합니다. 모든 관련 패키지 설치에 대한 자세한 내용은 설치를 참조하세요. 저장소의 샘플 디렉터리에 있는 샘플을 보면 빠르게 시작할 수 있습니다. 에이전트 생성 에이전트를 생성하려면 BaseAgent에서 상속하고 이벤트 핸들러를 구현할 수 있습니다.

## 핵심 발췌

당신이 관심 있는 이벤트를 위해. 다음은 BaseAgent에서 상속하고 이벤트 핸들러를 구현하는 방법을 보여주는 최소한의 예입니다. BaseAgent를 재정의하면 런타임 및 로깅 유틸리티에 액세스할 수 있고 IHandle<T를 구현하면 사용자 정의 메시지에 대한 이벤트 처리 방법을 쉽게 정의할 수 있습니다. 응용 프로그램에서 에이전트 실행 응용 프로그램에서 에이전트를 실행하려면 AgentsAppBuilder 클래스를 사용할 수 있습니다. 다음은 애플리케이션에서 'HelloAgent' 에이전트를 실행하는 방법에 대한 예입니다. .NET SDK 런타임 .NET SDK에는 클라우드에서 에이전트를 실행하기 위한 InMemory 단일 프로세스 런타임과 원격 분산 런타임이 모두 포함되어 있습니다. 분산 런타임은 Python 및 .NET에서 에이전트 실행을 지원하므로 해당 에이전트가 서로 통신할 수 있습니다. 분산 런타임

## 원문 내용

# AutoGen Core

AutoGen Core for .NET follows the same concepts and conventions of its Python counterpart. In fact, in order to understand the concepts in the .NET version, we recommend reading the [Python documentation](https://microsoft.github.io/autogen/stable/) first. Unless otherwise stated, the concepts in the Python version map to .NET.

Any important differences between the language versions are documented in the [Differences from Python](./differences-from-python.md) section. For things that only affect a given language, such as dependency injection or host builder patterns, these will not be specified in the differences document.

## Getting Started

You can obtain the SDK as a nuget package or by cloning the repository. The SDK is available on [NuGet](https://www.nuget.org/packages/Microsoft.AutoGen).
Minimally you will need the following:

```bash
dotnet add package Microsoft.AutoGen.Contracts
dotnet add package Microsoft.AutoGen.Core
```

See [Installation](./installation.md) for more detailed notes on installing all the related packages. 

You can quickly get started by looking at the samples in the [samples](https://github.com/microsoft/autogen/tree/main/dotnet/samples) directory of the repository.

### Creating an Agent

To create an agent, you can inherit from BaseAgent and implement event handlers for the events you care about. Here is a minimal example demonstrating how to inherit from BaseAgent and implement an event handler:

```csharp
public class MyAgent : BaseAgent, IHandle<MyMessage>
{
    // ...
    public async ValueTask HandleAsync(MyMessage item, MessageContext context)
    {
        // ...logic here...
    }
}
```

By overriding BaseAgent, you gain access to the runtime and logging utilities, and by implementing IHandle<T>, you can easily define event-handling methods for your custom messages.

### Running an Agent in an Application

To run your agent in an application, you can use the `AgentsAppBuilder` class. Here is an example of how to run an agent 'HelloAgent' in an application:

```csharp
AgentsAppBuilder appBuilder = new AgentsAppBuilder()
    .UseInProcessRuntime(deliverToSelf: true)
    .AddAgent<HelloAgent>("HelloAgent");

var app = await appBuilder.BuildAsync();

// start the app by publishing a message to the runtime
await app.PublishMessageAsync(new NewMessageReceived
{
    Message = "Hello from .NET"
}, new TopicId("HelloTopic"));

// Wait for shutdown
await app.WaitForShutdownAsync();
```

## .NET SDK Runtimes

The .NET SDK includes both an InMemory Single Process Runtime and a Remote, Distributed Runtime meant for running your agents in the cloud. The Distributed Runtime supports running agents in python and in .NET, allowing those agents to talk to one another. The distributed runtime uses Microsoft Orleans to provide resilience, persistence, and integration with messaging services such as Azure Event Hubs.  The xlang functionality requires that your agent's Messages are serializable as CloudEvents.  The messages are exchanged as CloudEvents over Grpc, and the runtime takes care of ensuring that the messages are delivered to the correct agents. 

To use the Distributed Runtime, you will need to add the following package to your project:

```bash
dotnet add package Microsoft.AutoGen.Core.Grpc
```

This is the package that runs in the application with your agent(s) and connects to the distributed system. 

To Run the backend/server side you need:

```bash
dotnet add package Microsoft.AutoGen.RuntimeGateway
dotnet add package Microsoft.AutoGen.AgentHost
```

You can run the backend on its own:

```bash
dotnet run --project Microsoft.AutoGen.AgentHost
```

or you can include it inside your own application:

```csharp
using Microsoft.AutoGen.RuntimeGateway;
using Microsoft.AutoGen.AgentHost;
var autogenBackend = await Microsoft.AutoGen.RuntimeGateway.Grpc.Host.StartAsync(local: false, useGrpc: true).ConfigureAwait(false);
```

You can also install the runtime as a dotnet tool:

```
dotnet pack --no-build --configuration Release --output './output/release' -bl\n
dotnet tool install --add-source ./output/release Microsoft.AutoGen.AgentHost
# run the tool
# dotnet agenthost 
# or just...  
agenthost 
```

### Running Multiple Agents and the Runtime in separate processes with .NET Aspire

The [Hello.AppHost project](https://github.com/microsoft/autogen/blob/50d7587a4649504af3bb79ab928b2a3882a1a394/dotnet/samples/Hello/Hello.AppHost/Program.cs#L4) illustrates how to orchestrate a distributed system with multiple agents and the runtime in separate processes using .NET Aspire. It also points to a [python agent that illustrates how to run agents in different languages in the same distributed system](https://github.com/microsoft/autogen/blob/50d7587a4649504af3bb79ab928b2a3882a1a394/python/samples/core_xlang_hello_python_agent/README.md#L1).

```csharp
// Copyright (c) Microsoft Corporation. All rights reserved.
// Program.cs

using Microsoft.Extensions.Hosting;

var builder = DistributedApplication.CreateBuilder(args);
var backend = builder.AddProject<Projects.Microsoft_AutoGen_AgentHost>("backend").WithExternalHttpEndpoints();
var client = builder.AddProject<Projects.HelloAgent>("HelloAgentsDotNET")
    .WithReference(backend)
    .WithEnvironment("AGENT_HOST", backend.GetEndpoint("https"))
    .WithEnvironment("STAY_ALIVE_ON_GOODBYE", "true")
    .WaitFor(backend);
// xlang is over http for now - in prod use TLS between containers
builder.AddPythonApp("HelloAgentsPython", "../../../../python/samples/core_xlang_hello_python_agent", "hello_python_agent.py", "../../.venv")
    .WithReference(backend)
    .WithEnvironment("AGENT_HOST", backend.GetEndpoint("http"))
    .WithEnvironment("STAY_ALIVE_ON_GOODBYE", "true")
    .WithEnvironment("GRPC_DNS_RESOLVER", "native")
    .WithOtlpExporter()
    .WaitFor(client);
using var app = builder.Build();
await app.StartAsync();
var url = backend.GetEndpoint("http").Url;
Console.WriteLine("Backend URL: " + url);
await app.WaitForShutdownAsync();
```

You can find more examples of how to use Aspire and XLang agents in the [Microsoft.AutoGen.Integration.Tests.AppHost](https://github.com/microsoft/autogen/blob/acd7e864300e24a3ee67a89a916436e8894bb143/dotnet/test/Microsoft.AutoGen.Integration.Tests.AppHosts/) directory. 

### Configuring Logging

The SDK uses the Microsoft.Extensions.Logging framework for logging. Here is an example appsettings.json file with some useful defaults:

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Warning",
      "Microsoft.Hosting.Lifetime": "Information",
      "Microsoft.AspNetCore": "Information",
      "Microsoft": "Information",
      "Microsoft.Orleans": "Warning",
      "Orleans.Runtime": "Error",
      "Grpc": "Information"
    }
  },
  "AllowedHosts": "*",
  "Kestrel": {
    "EndpointDefaults": {
      "Protocols": "Http2"
    }
  }
}
```

### Defining Message Types in Protocol Buffers

A convenient way to define common event or message types to be used in both python and .NET agents is to define your events. This is covered here: [Using Protocol Buffers to Define Message Types](./protobuf-message-types.md).