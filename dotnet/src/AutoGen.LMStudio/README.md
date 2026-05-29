# 읽어보기

- 원문 저장소: `microsoft/autogen`
- 미러 저장소: `martinlee-git/autogen`
- 원문 문서: https://github.com/microsoft/autogen/blob/main/dotnet/src/AutoGen.LMStudio/README.md
- 미러 경로: `dotnet/src/AutoGen.LMStudio/README.md`

## 한글 요약

AutoGen.LMStudio 이 패키지는 LMStudio 로컬 서버에서 API와 같은 openai 사용을 지원합니다. 설치 AutoGen.LMStudio를 사용하려면 .csproj 파일에 다음 패키지를 추가하세요. 0.0.7(2024 02 11)의 사용 업데이트 기록 업데이트 LMStudio 로컬 서버에서 API와 같은 openai 사용을 지원하려면 LMStudioAgent를 추가하세요.

## 핵심 발췌

AutoGen.LMStudio 이 패키지는 LMStudio 로컬 서버에서 API와 같은 openai 사용을 지원합니다. ## 설치 AutoGen.LMStudio를 사용하려면 .csproj 파일에 다음 패키지를 추가하세요. ```xml <ItemGrou

## 원문 내용

## AutoGen.LMStudio

This package provides support for consuming openai-like API from LMStudio local server.

## Installation
To use `AutoGen.LMStudio`, add the following package to your `.csproj` file:

```xml
<ItemGroup>
    <PackageReference Include="AutoGen.LMStudio" Version="AUTOGEN_VERSION" />
</ItemGroup>
```

## Usage
```csharp
using AutoGen.LMStudio;
var localServerEndpoint = "localhost";
var port = 5000;
var lmStudioConfig = new LMStudioConfig(localServerEndpoint, port);
var agent = new LMStudioAgent(
    name: "agent",
    systemMessage: "You are an agent that help user to do some tasks.",
    lmStudioConfig: lmStudioConfig)
    .RegisterPrintMessage(); // register a hook to print message nicely to console

await agent.SendAsync("Can you write a piece of C# code to calculate 100th of fibonacci?");
```

## Update history
### Update on 0.0.7 (2024-02-11)
- Add `LMStudioAgent` to support consuming openai-like API from LMStudio local server.