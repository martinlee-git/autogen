# 읽어보기

- 원문 저장소: `microsoft/autogen`
- 미러 저장소: `martinlee-git/autogen`
- 원문 문서: https://github.com/microsoft/autogen/blob/main/dotnet/test/Microsoft.AutoGen.Integration.Tests.AppHosts/core_xlang_hello_python_agent/README.md
- 미러 경로: `dotnet/test/Microsoft.AutoGen.Integration.Tests.AppHosts/core_xlang_hello_python_agent/README.md`

## 한글 요약

Python 및 dotnet 에이전트 상호 운용성 샘플 이 샘플은 .NET 에이전트와 상호 작용하는 Python 에이전트를 만드는 방법을 보여줍니다. 샘플을 실행하려면 autogen 저장소를 확인하세요. 그런 다음 다음을 수행합니다. 1. autogen/dotnet/samples/Hello/Hello.AppHost로 이동합니다. 2. dotnet run을 실행하여 3개의 프로젝트를 실행하는 .NET Aspire 앱 호스트를 시작합니다. 백엔드(.NET 에이전트 런타임) HelloAgent(.NET 에이전트) 이 Python 에이전트 hello python Agent.py 3. AppHost는 https://localhost:15887에서 Aspire 대시보드를 시작합니다. Python 에이전트는 .NET 런타임에 메시지를 보내 .NET 에이전트에 메시지를 전달함으로써 .NET 에이전트와 상호 작용합니다.

## 핵심 발췌

Python 및 dotnet 에이전트 상호 운용성 샘플 이 샘플은 .NET 에이전트와 상호 작용하는 Python 에이전트를 만드는 방법을 보여줍니다. 샘플을 실행하려면 autogen 저장소를 확인하세요. 그런 다음 다음을 수행하십시오. 1.

## 원문 내용

# Python and dotnet agents interoperability sample

This sample demonstrates how to create a Python agent that interacts with a .NET agent.
To run the sample, check out the autogen repository.
Then do the following:

1. Navigate to autogen/dotnet/samples/Hello/Hello.AppHost
2. Run `dotnet run` to start the .NET Aspire app host, which runs three projects:
    - Backend (the .NET Agent Runtime)
    - HelloAgent (the .NET Agent)
    - this Python agent - hello_python_agent.py
3. The AppHost will start the Aspire dashboard on [https://localhost:15887](https://localhost:15887).

The Python agent will interact with the .NET agent by sending a message to the .NET runtime, which will relay the message to the .NET agent.