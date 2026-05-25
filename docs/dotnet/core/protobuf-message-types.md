# protobuf 메시지 유형

- 원문 저장소: `microsoft/autogen`
- 미러 저장소: `martinlee-git/autogen`
- 원문 문서: https://github.com/microsoft/autogen/blob/main/docs/dotnet/core/protobuf-message-types.md
- 미러 경로: `docs/dotnet/core/protobuf-message-types.md`

## 한글 요약

프로토콜 버퍼를 사용하여 메시지 유형 정의 @Microsoft.AutoGen.Core.InProcessRuntime 이외의 런타임을 사용하여 메시지를 전송하려면 해당 메시지를 프로토콜 버퍼 메시지로 정의해야 합니다. 이는 메시지가 프로토콜 버퍼를 사용하여 직렬화 및 역직렬화되기 때문입니다. 이 요구 사항은 변환기, 사용자 지정 직렬화 또는 기타 메커니즘을 허용하여 향후 완화될 수 있습니다. .NET 프로젝트에 프로토콜 버퍼를 포함하는 방법 메시지 유형을 정의하는 .proto 파일은 메시지에 대한 C# 클래스를 자동으로 생성하는 프로젝트에 포함되어야 합니다. 1. .csproj 파일에 Grpc.Tools 패키지를 포함합니다. 2. 프로젝트에 .proto 파일 포함을 만듭니다. 3. 프로토콜 버퍼 언어 가이드에 지정된 대로 메시지를 정의합니다. 4. 메시지 처리, 전송 및 게시를 위해 생성된 클래스에 대한 코드:

## 핵심 발췌

프로토콜 버퍼를 사용하여 메시지 유형 정의 @Microsoft.AutoGen.Core.InProcessRuntime 이외의 런타임을 사용하여 메시지를 전송하려면 해당 메시지를 프로토콜 버퍼 메시지로 정의해야 합니다. 이건 나 때문이야

## 원문 내용

# Using Protocol Buffers to Define Message Types

For a message to be sent using a runtime other than the @Microsoft.AutoGen.Core.InProcessRuntime, it must be defined as a Protocol Buffers message. This is because the message is serialized and deserialized using Protocol Buffers. This requirement may be relaxed in future by allowing for converters, custom serialization, or other mechanisms.

## How to include Protocol Buffers in a .NET project

The .proto file which defines the message types must be included in the project, which will automatically generate the C# classes for the messages.

1. Include `Grpc.Tools` package in your `.csproj` file:

```xml
  <PackageReference Include="Grpc.Tools" PrivateAssets="All" />
```

2. Create an include a `.proto` file in the project:

```xml
<ItemGroup>
  <Protobuf Include="messages.proto" GrpcServices="Client;Server" Link="messages.proto" />
</ItemGroup>
```

3. define your messages as specified in the [Protocol Buffers Language Guide](https://protobuf.dev/programming-guides/proto3/)

```proto
syntax = "proto3";

package HelloAgents;

option csharp_namespace = "MyAgentsProtocol";

message TextMessage {
    string Source = 1;
    string Content = 2;
}
```

4. Code against the generated class for handling, sending and publishing messages:

```csharp
using Microsoft.AutoGen.Contracts;
using Microsoft.AutoGen.Core;
using MyAgentsProtocol;

[TypeSubscription("default")]
public class Checker(
    AgentId id,
    IAgentRuntime runtime,
    ) :
        BaseAgent(id, runtime, "MyAgent", null),
        IHandle<TextMessage>
{
    public async ValueTask HandleAsync(TextMessage item, MessageContext messageContext)
    {
        Console.WriteLine($"Received message from {item.Source}: {item.Content}");
    }
}
```