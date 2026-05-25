# 설치

- 원문 저장소: `microsoft/autogen`
- 미러 저장소: `martinlee-git/autogen`
- 원문 문서: https://github.com/microsoft/autogen/blob/main/docs/dotnet/core/installation.md
- 미러 경로: `docs/dotnet/core/installation.md`

## 한글 요약

설치 .NET cli를 통해 설치 또는 패키지 관리자를 통해 설치 또는 <PackageReference를 통해 추가 추가 패키지 Core 및 Contracts 패키지는 단일 프로세스 내에서 Core API를 사용하여 에이전트를 작성하고 실행하는 데 필요한 것을 제공합니다. Microsoft.AutoGen.AgentChat Core SDK 위에 채팅 중심 에이전트 오케스트레이션을 구축하기 위한 AgentChat 패키지 구현 Microsoft.AutoGen.Agents는 사용할 수 있는 소수의 기본 에이전트가 포함된 패키지입니다. Microsoft.AutoGen.Extensions Aspire, Microsoft.Extensions.AI 및 Semantic Kernel을 포함하여 밀접하게 관련된 프로젝트를 지원하는 확장 Python과 .NET 에이전트 간의 x 언어 통신을 허용하는 다양한 프로세스의 에이전트로 시스템을 실행할 수 있도록 하기 위해 추가 패키지가 있습니다. Microsoft.AutoGen.Core.Grpc 분산 시스템의 에이전트에 대한 .NET 클라이언트 런타임입니다. Microsoft.AutoGen.Core 와 동일한 API가 있습니다. Microsoft.AutoGen.RuntimeGatewway.Grpc 분산의 .NET 서버측

## 핵심 발췌

여러 게이트웨이를 실행하여 에이전트 집합을 관리하고 x 언어 상호 운용성을 가능하게 하는 시스템입니다. Microsoft.AutoGen.AgentHost Grpc 서비스를 호스팅하는 .NET Aspire 프로젝트

## 원문 내용

# Installation

Install via `.NET cli`

```sh
dotnet add package Microsoft.AutoGen.Contracts --version 0.4.0-dev.1
dotnet add package Microsoft.AutoGen.Core --version 0.4.0-dev.1
```

Or, install via `Package Manager`

```pwsh
PM> NuGet\Install-Package Microsoft.AutoGen.Contracts -Version 0.4.0-dev.1
PM> NuGet\Install-Package Microsoft.AutoGen.Core -Version 0.4.0-dev.1
```

Or, add via `<PackageReference>`

```xml
<PackageReference Include="Microsoft.AutoGen.Contracts" Version="0.4.0-dev.1" />
<PackageReference Include="Microsoft.AutoGen.Core" Version="0.4.0-dev.1" />
```

# Additional Packages

The *Core* and *Contracts* packages will give you what you need for writing and running agents using the Core API within a single process. 

- *Microsoft.AutoGen.AgentChat* - An implementation of the AgentChat package for building chat-centric agent orchestration on top of the Core SDK
- *Microsoft.AutoGen.Agents* - a package that has a small number of default agents you can use. 
- *Microsoft.AutoGen.Extensions* - Extensions to support closely related projects including Aspire, Microsoft.Extensions.AI, and Semantic Kernel

```sh
dotnet add package Microsoft.AutoGen.AgentChat --version 0.4.0-dev-1
dotnet add package Microsoft.AutoGen.Agents --version 0.4.0-dev-1
dotnet add package Microsoft.AutoGen.Extensions --version 0.4.0-dev-1
```

To enable running a system with agents in different processes that allows for x-language communication between python and .NET agents, there are additional packages:

- *Microsoft.AutoGen.Core.Grpc* - the .NET client runtime for agents in a distributed system. It has the same API as *Microsoft.AutoGen.Core*. 
- *Microsoft.AutoGen.RuntimeGatewway.Grpc* - the .NET server side of the distributed system that allows you to run multiple gateways to manage fleets of agents and enables x-language interoperability. 
- *Microsoft.AutoGen.AgentHost* - A .NET Aspire project that hosts the Grpc Service

```sh
dotnet add package Microsoft.AutoGen.Core.Grpc --version 0.4.0-dev-1
dotnet add package Microsoft.AutoGen.RuntimeGateway.Grpc --version 0.4.0-dev-1
dotnet add package Microsoft.AutoGen.AgentHost --version 0.4.0-dev-1
```