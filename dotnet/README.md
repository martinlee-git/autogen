# 읽어보기

- 원문 저장소: `microsoft/autogen`
- 미러 저장소: `martinlee-git/autogen`
- 원문 문서: https://github.com/microsoft/autogen/blob/main/dotnet/README.md
- 미러 경로: `dotnet/README.md`

## 한글 요약

.NET용 AutoGen 여기에는 두 가지 패키지 세트가 있습니다. AutoGen.\ .NET용 AutoGen 0.2에서 파생된 이전 패키지는 점차적으로 더 이상 사용되지 않으며 새 패키지인 Microsoft.AutoGen으로 이식됩니다. 이벤트 기반 모델을 사용하는 .NET용 새 패키지 이러한 API는 아직 안정적이지 않으며 변경될 수 있습니다. 새 패키지를 시작하려면 샘플, 특히 Hello 샘플을 참조하세요. 다음 피드에서 새 패키지와 이전 패키지를 모두 설치할 수 있습니다. [!NOTE] Nightly 빌드는 다음에서 사용할 수 있습니다. <https://pkgs.dev.azure.com/AGPublish/AGPublic/packaging/AutoGen Nightly/nuget/v3/index.json 먼저 설치 가이드에 따라 AutoGen 패키지를 설치합니다. 그런 다음 다음 코드 조각으로 시작하여 대화 가능한 에이전트를 만들고 대화할 수 있습니다. 샘플 샘플 프로젝트에서 더 많은 예제를 찾을 수 있습니다. 기능 ConversableAgent [x] 함수 호출 [x] 코드 실행(dotnet 전용, dotnet Interactive 기반) 에이전트 통신 [x] 두 에이전트 채팅

## 핵심 발췌

[x] 그룹 채팅 [ ] dotnet 전용의 향상된 LLM 추론 [x] 유형 안전 함수 정의 생성을 위한 소스 생성기

## 원문 내용

# AutoGen for .NET

Thre are two sets of packages here:
AutoGen.\* the older packages derived from AutoGen 0.2 for .NET - these will gradually be deprecated and ported into the new packages
Microsoft.AutoGen.* the new packages for .NET that use the event-driven model - These APIs are not yet stable and are subject to change.

To get started with the new packages, please see the [samples](./samples/) and in particular the [Hello](./samples/Hello) sample.

You can install both new and old packages from the following feeds:

[![dotnet-ci](https://github.com/microsoft/autogen/actions/workflows/dotnet-build.yml/badge.svg)](https://github.com/microsoft/autogen/actions/workflows/dotnet-build.yml)
[![NuGet version](https://badge.fury.io/nu/AutoGen.Core.svg)](https://badge.fury.io/nu/AutoGen.Core)

> [!NOTE]
> Nightly build is available at:
>
> - [![Static Badge](https://img.shields.io/badge/azure_devops-grey?style=flat)](https://dev.azure.com/AGPublish/AGPublic/_artifacts/feed/AutoGen-Nightly) : <https://pkgs.dev.azure.com/AGPublish/AGPublic/_packaging/AutoGen-Nightly/nuget/v3/index.json>

Firstly, following the [installation guide](./website/articles/Installation.md) to install AutoGen packages.

Then you can start with the following code snippet to create a conversable agent and chat with it.

```csharp
using AutoGen;
using AutoGen.OpenAI;

var openAIKey = Environment.GetEnvironmentVariable("OPENAI_API_KEY") ?? throw new Exception("Please set OPENAI_API_KEY environment variable.");
var gpt35Config = new OpenAIConfig(openAIKey, "gpt-3.5-turbo");

var assistantAgent = new AssistantAgent(
    name: "assistant",
    systemMessage: "You are an assistant that help user to do some tasks.",
    llmConfig: new ConversableAgentConfig
    {
        Temperature = 0,
        ConfigList = [gpt35Config],
    })
    .RegisterPrintMessage(); // register a hook to print message nicely to console

// set human input mode to ALWAYS so that user always provide input
var userProxyAgent = new UserProxyAgent(
    name: "user",
    humanInputMode: HumanInputMode.ALWAYS)
    .RegisterPrintMessage();

// start the conversation
await userProxyAgent.InitiateChatAsync(
    receiver: assistantAgent,
    message: "Hey assistant, please do me a favor.",
    maxRound: 10);
```

## Samples

You can find more examples under the [sample project](https://github.com/microsoft/autogen/tree/dotnet/samples/AgentChat/Autogen.Basic.Sample).

## Functionality

- ConversableAgent
  - [x] function call
  - [x] code execution (dotnet only, powered by [`dotnet-interactive`](https://github.com/dotnet/interactive))

- Agent communication
  - [x] Two-agent chat
  - [x] Group chat

- [ ] Enhanced LLM Inferences

- Exclusive for dotnet
  - [x] Source generator for type-safe function definition generation