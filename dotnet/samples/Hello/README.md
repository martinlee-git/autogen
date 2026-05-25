# 읽어보기

- 원문 저장소: `microsoft/autogen`
- 미러 저장소: `martinlee-git/autogen`
- 원문 문서: https://github.com/microsoft/autogen/blob/main/dotnet/samples/Hello/README.md
- 미러 경로: `dotnet/samples/Hello/README.md`

## 한글 요약

HelloAgent용 다중 프로젝트 앱 호스트 이는 HelloAgent 프로젝트와 에이전트 백엔드를 시작하는 .NET Aspire 앱 호스트입니다. 프로젝트가 시작되면 콘솔에 제공된 링크를 사용하여 Aspire 대시보드에서 원격 측정 및 로그를 볼 수 있습니다. 자세한 내용은 HelloAgent README를 참조하세요.

## 핵심 발췌

HelloAgent용 다중 프로젝트 앱 호스트 이는 HelloAgent 프로젝트와 에이전트 백엔드를 시작하는 .NET Aspire 앱 호스트입니다. 일단

## 원문 내용

# Multiproject App Host for HelloAgent

This is a [.NET Aspire](https://learn.microsoft.com/en-us/dotnet/aspire/get-started/aspire-overview) App Host that starts up the HelloAgent project and the agents backend. Once the project starts up you will be able to view the telemetry and logs in the [Aspire Dashboard](https://learn.microsoft.com/en-us/dotnet/aspire/get-started/aspire-dashboard) using the link provided in the console.

```shell
cd Hello.AppHost
dotnet run
```

For more info see the HelloAgent [README](../HelloAgent/README.md).