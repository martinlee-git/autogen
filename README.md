# 읽어보기

- 원문 저장소: `microsoft/autogen`
- 미러 저장소: `martinlee-git/autogen`
- 원문 문서: https://github.com/microsoft/autogen/blob/main/README.md
- 미러 경로: `README.md`

## 한글 요약

<a name="readme top" </a <div align="center" <img src="https://microsoft.github.io/autogen/0.2/img/ag.svg" alt="AutoGen Logo" width="100" </div AutoGen AutoGen은 자율적으로 작동하거나 인간과 함께 작업할 수 있는 다중 에이전트 AI 애플리케이션을 만들기 위한 프레임워크입니다. 주의] ⚠️ 유지 관리 모드 AutoGen은 이제 유지 관리 모드에 있습니다. 새로운 기능이나 개선 사항은 제공되지 않으며 앞으로는 커뮤니티에서 관리됩니다. 신규 사용자는 Microsoft Agent Framework로 시작해야 합니다. 기존 사용자는 AutoGen → Microsoft Agent Framework 마이그레이션 가이드를 사용하여 마이그레이션하는 것이 좋습니다. MAF(Microsoft Agent Framework)는 AutoGen의 기업용 후속 제품입니다. Microsoft Agent FrameworkAF는 이제 프로덕션 준비 릴리스로 제공됩니다. 안정적인 API와 장기적인 지원을 약속합니다. 단일 도우미를 구축하든 전문 에이전트 그룹을 오케스트레이션하든 Microsoft Agent Framework 1.0은 엔터프라이즈급 다중 에이전트 오케스트레이션, 다중 공급자 모델 지원 및 cr을 제공합니다.

## 핵심 발췌

A2A 및 MCP를 통한 oss 런타임 상호 운용성. 설치 AutoGen에는 Python 3.10 이상이 필요합니다. 현재 안정 버전은 릴리스에서 찾을 수 있습니다. AutoGen v0.2에서 업그레이드하는 경우 코드 및 구성을 업데이트하는 방법에 대한 자세한 지침은 마이그레이션 가이드를 참조하세요. 빠른 시작 다음 샘플은 OpenAI API를 호출하므로 먼저 계정을 만들고 내보내기 OPENAI API KEY="sk ..."로 키를 내보내야 합니다. Hello World OpenAI의 GPT 4o 모델을 사용하여 보조 에이전트를 만듭니다. 다른 지원 모델을 확인하세요. MCP 서버 Playwright MCP 서버를 사용하는 웹 브라우징 보조 에이전트를 만듭니다. 경고 : 로컬 환경에서 명령을 실행하거나 민감한 정보를 노출할 수 있으므로 신뢰할 수 있는 MCP 서버에만 연결하세요. 다중 에이전트 오케스트레이션 귀하는 다음을 수행할 수 있습니다.

## 원문 내용

<a name="readme-top"></a>

<div align="center">
<img src="https://microsoft.github.io/autogen/0.2/img/ag.svg" alt="AutoGen Logo" width="100">

[![Twitter](https://img.shields.io/twitter/url/https/twitter.com/cloudposse.svg?style=social&label=Follow%20%40pyautogen)](https://twitter.com/pyautogen)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Company?style=flat&logo=linkedin&logoColor=white)](https://www.linkedin.com/company/105812540)
[![Discord](https://img.shields.io/badge/discord-chat-green?logo=discord)](https://aka.ms/autogen-discord)
[![Documentation](https://img.shields.io/badge/Documentation-AutoGen-blue?logo=read-the-docs)](https://microsoft.github.io/autogen/)
[![Blog](https://img.shields.io/badge/Blog-AutoGen-blue?logo=blogger)](https://devblogs.microsoft.com/autogen/)

</div>

# AutoGen [![Maintenance Mode](https://img.shields.io/badge/status-maintenance%20mode-orange)](https://github.com/microsoft/agent-framework)

**AutoGen** is a framework for creating multi-agent AI applications that can act autonomously or work alongside humans.

> [!CAUTION]
> **⚠️ Maintenance Mode**
>
> AutoGen is now in maintenance mode. It will not receive new features or enhancements and is community managed going forward.
>
> New users should start with [Microsoft Agent Framework](https://github.com/microsoft/agent-framework). Existing users are encouraged to migrate using the [AutoGen → Microsoft Agent Framework migration guide](https://learn.microsoft.com/en-us/agent-framework/migration-guide/from-autogen/).
>
> Microsoft Agent Framework (MAF) is the enterprise‑ready successor to AutoGen. Microsoft Agent FrameworkAF in now available as a production-ready release: stable APIs, and a commitment to long-term support. Whether you're building a single assistant or orchestrating a fleet of specialized agents, Microsoft Agent Framework 1.0 gives you enterprise-grade multi-agent orchestration, multi-provider model support, and cross-runtime interoperability via A2A and MCP.

## Installation

AutoGen requires **Python 3.10 or later**.

```bash
# Install AgentChat and OpenAI client from Extensions
pip install -U "autogen-agentchat" "autogen-ext[openai]"
```

The current stable version can be found in the [releases](https://github.com/microsoft/autogen/releases). If you are upgrading from AutoGen v0.2, please refer to the [Migration Guide](https://microsoft.github.io/autogen/stable/user-guide/agentchat-user-guide/migration-guide.html) for detailed instructions on how to update your code and configurations.

```bash
# Install AutoGen Studio for no-code GUI
pip install -U "autogenstudio"
```

## Quickstart

The following samples call OpenAI API, so you first need to create an account and export your key as `export OPENAI_API_KEY="sk-..."`.

### Hello World

Create an assistant agent using OpenAI's GPT-4o model. See [other supported models](https://microsoft.github.io/autogen/stable/user-guide/agentchat-user-guide/tutorial/models.html).

```python
import asyncio
from autogen_agentchat.agents import AssistantAgent
from autogen_ext.models.openai import OpenAIChatCompletionClient

async def main() -> None:
    model_client = OpenAIChatCompletionClient(model="gpt-4.1")
    agent = AssistantAgent("assistant", model_client=model_client)
    print(await agent.run(task="Say 'Hello World!'"))
    await model_client.close()

asyncio.run(main())
```

### MCP Server

Create a web browsing assistant agent that uses the Playwright MCP server.

```python
# First run `npm install -g @playwright/mcp@latest` to install the MCP server.
import asyncio
from autogen_agentchat.agents import AssistantAgent
from autogen_agentchat.ui import Console
from autogen_ext.models.openai import OpenAIChatCompletionClient
from autogen_ext.tools.mcp import McpWorkbench, StdioServerParams


async def main() -> None:
    model_client = OpenAIChatCompletionClient(model="gpt-4.1")
    server_params = StdioServerParams(
        command="npx",
        args=[
            "@playwright/mcp@latest",
            "--headless",
        ],
    )
    async with McpWorkbench(server_params) as mcp:
        agent = AssistantAgent(
            "web_browsing_assistant",
            model_client=model_client,
            workbench=mcp, # For multiple MCP servers, put them in a list.
            model_client_stream=True,
            max_tool_iterations=10,
        )
        await Console(agent.run_stream(task="Find out how many contributors for the microsoft/autogen repository"))


asyncio.run(main())
```

> **Warning**: Only connect to trusted MCP servers as they may execute commands
> in your local environment or expose sensitive information.

### Multi-Agent Orchestration

You can use `AgentTool` to create a basic multi-agent orchestration setup.

```python
import asyncio

from autogen_agentchat.agents import AssistantAgent
from autogen_agentchat.tools import AgentTool
from autogen_agentchat.ui import Console
from autogen_ext.models.openai import OpenAIChatCompletionClient


async def main() -> None:
    model_client = OpenAIChatCompletionClient(model="gpt-4.1")

    math_agent = AssistantAgent(
        "math_expert",
        model_client=model_client,
        system_message="You are a math expert.",
        description="A math expert assistant.",
        model_client_stream=True,
    )
    math_agent_tool = AgentTool(math_agent, return_value_as_last_message=True)

    chemistry_agent = AssistantAgent(
        "chemistry_expert",
        model_client=model_client,
        system_message="You are a chemistry expert.",
        description="A chemistry expert assistant.",
        model_client_stream=True,
    )
    chemistry_agent_tool = AgentTool(chemistry_agent, return_value_as_last_message=True)

    agent = AssistantAgent(
        "assistant",
        system_message="You are a general assistant. Use expert tools when needed.",
        model_client=model_client,
        model_client_stream=True,
        tools=[math_agent_tool, chemistry_agent_tool],
        max_tool_iterations=10,
    )
    await Console(agent.run_stream(task="What is the integral of x^2?"))
    await Console(agent.run_stream(task="What is the molecular weight of water?"))


asyncio.run(main())
```

For more advanced multi-agent orchestrations and workflows, read
[AgentChat documentation](https://microsoft.github.io/autogen/stable/user-guide/agentchat-user-guide/index.html).

### AutoGen Studio

Use AutoGen Studio to prototype and run multi-agent workflows without writing code.

> **Caution**: AutoGen Studio is meant to help you rapidly prototype multi-agent workflows and
> demonstrate an example of end user interfaces built with AutoGen. It is **not meant to be a
> production-ready app**. Developers are encouraged to use the AutoGen framework to build their own
> applications, implementing authentication, security and other features required for deployed
> applications. See the [security note](https://microsoft.github.io/autogen/dev/user-guide/autogenstudio-user-guide/index.html#a-note-on-security) for more details.

```bash
# Run AutoGen Studio on http://localhost:8080
autogenstudio ui --port 8080 --appdir ./my-app
```

## Why AutoGen?

<div align="center">
  <img src="autogen-landing.jpg" alt="AutoGen Landing" width="500">
</div>

Pioneered in Microsoft Research, AutoGen opened the door to experimental multi-agent orchestration patterns that inspired the community. While AutoGen is now in maintenance mode, existing users can continue to use the framework with the architecture described below. **For new projects, we recommend [Microsoft Agent Framework](https://github.com/microsoft/agent-framework)**, which builds on the lessons learned from AutoGen with enterprise-grade support.

The autogen _framework_ uses a layered and extensible design. Layers have clearly divided responsibilities and build on top of layers below. This design enables you to use the framework at different levels of abstraction, from high-level APIs to low-level components.

- [Core API](./python/packages/autogen-core/) implements message passing, event-driven agents, and local and distributed runtime for flexibility and power. It also support cross-language support for .NET and Python.
- [AgentChat API](./python/packages/autogen-agentchat/) implements a simpler but opinionated API for rapid prototyping. This API is built on top of the Core API and is closest to what users of v0.2 are familiar with and supports common multi-agent patterns such as two-agent chat or group chats.
- [Extensions API](./python/packages/autogen-ext/) enables first- and third-party extensions continuously expanding framework capabilities. It support specific implementation of LLM clients (e.g., OpenAI, AzureOpenAI), and capabilities such as code execution.

The ecosystem also supports two essential _developer tools_:

<div align="center">
  <img src="https://media.githubusercontent.com/media/microsoft/autogen/refs/heads/main/python/packages/autogen-studio/docs/ags_screen.png" alt="AutoGen Studio Screenshot" width="500">
</div>

- [AutoGen Studio](./python/packages/autogen-studio/) provides a no-code GUI for building multi-agent applications.
- [AutoGen Bench](./python/packages/agbench/) provides a benchmarking suite for evaluating agent performance.

You can use the AutoGen framework and developer tools to create applications for your domain. For example, [Magentic-One](./python/packages/magentic-one-cli/) is a state-of-the-art multi-agent team built using AgentChat API and Extensions API that can handle a variety of tasks that require web browsing, code execution, and file handling.

For community support, visit our [Discord server](https://aka.ms/autogen-discord) or [GitHub Discussions](https://github.com/microsoft/autogen/discussions). Note that AutoGen is now community-managed and responses may be limited.

## Where to go next?

> **Starting a new project?** Head to [Microsoft Agent Framework](https://github.com/microsoft/agent-framework) for the latest multi-agent capabilities with long-term support.
>
> **Existing AutoGen user?** Use the [migration guide](https://learn.microsoft.com/en-us/agent-framework/migration-guide/from-autogen/) to transition, or refer to the resources below for current AutoGen documentation.

<div align="center">

|               | [![Python](https://img.shields.io/badge/AutoGen-Python-blue?logo=python&logoColor=white)](./python)                                                                                                                                                                                                                                                                                                                | [![.NET](https://img.shields.io/badge/AutoGen-.NET-green?logo=.net&logoColor=white)](./dotnet)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | [![Studio](https://img.shields.io/badge/AutoGen-Studio-purple?logo=visual-studio&logoColor=white)](./python/packages/autogen-studio)                        |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Installation  | [![Installation](https://img.shields.io/badge/Install-blue)](https://microsoft.github.io/autogen/stable/user-guide/agentchat-user-guide/installation.html)                                                                                                                                                                                                                                                         | [![Install](https://img.shields.io/badge/Install-green)](https://microsoft.github.io/autogen/dotnet/dev/core/installation.html)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | [![Install](https://img.shields.io/badge/Install-purple)](https://microsoft.github.io/autogen/stable/user-guide/autogenstudio-user-guide/installation.html) |
| Quickstart    | [![Quickstart](https://img.shields.io/badge/Quickstart-blue)](https://microsoft.github.io/autogen/stable/user-guide/agentchat-user-guide/quickstart.html#)                                                                                                                                                                                                                                                         | [![Quickstart](https://img.shields.io/badge/Quickstart-green)](https://microsoft.github.io/autogen/dotnet/dev/core/index.html)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | [![Usage](https://img.shields.io/badge/Quickstart-purple)](https://microsoft.github.io/autogen/stable/user-guide/autogenstudio-user-guide/usage.html#)      |
| Tutorial      | [![Tutorial](https://img.shields.io/badge/Tutorial-blue)](https://microsoft.github.io/autogen/stable/user-guide/agentchat-user-guide/tutorial/index.html)                                                                                                                                                                                                                                                          | [![Tutorial](https://img.shields.io/badge/Tutorial-green)](https://microsoft.github.io/autogen/dotnet/dev/core/tutorial.html)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | [![Usage](https://img.shields.io/badge/Tutorial-purple)](https://microsoft.github.io/autogen/stable/user-guide/autogenstudio-user-guide/usage.html#)        |
| API Reference | [![API](https://img.shields.io/badge/Docs-blue)](https://microsoft.github.io/autogen/stable/reference/index.html#)                                                                                                                                                                                                                                                                                                 | [![API](https://img.shields.io/badge/Docs-green)](https://microsoft.github.io/autogen/dotnet/dev/api/Microsoft.AutoGen.Contracts.html)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | [![API](https://img.shields.io/badge/Docs-purple)](https://microsoft.github.io/autogen/stable/user-guide/autogenstudio-user-guide/usage.html)               |
| Packages      | [![PyPi autogen-core](https://img.shields.io/badge/PyPi-autogen--core-blue?logo=pypi)](https://pypi.org/project/autogen-core/) <br> [![PyPi autogen-agentchat](https://img.shields.io/badge/PyPi-autogen--agentchat-blue?logo=pypi)](https://pypi.org/project/autogen-agentchat/) <br> [![PyPi autogen-ext](https://img.shields.io/badge/PyPi-autogen--ext-blue?logo=pypi)](https://pypi.org/project/autogen-ext/) | [![NuGet Contracts](https://img.shields.io/badge/NuGet-Contracts-green?logo=nuget)](https://www.nuget.org/packages/Microsoft.AutoGen.Contracts/) <br> [![NuGet Core](https://img.shields.io/badge/NuGet-Core-green?logo=nuget)](https://www.nuget.org/packages/Microsoft.AutoGen.Core/) <br> [![NuGet Core.Grpc](https://img.shields.io/badge/NuGet-Core.Grpc-green?logo=nuget)](https://www.nuget.org/packages/Microsoft.AutoGen.Core.Grpc/) <br> [![NuGet RuntimeGateway.Grpc](https://img.shields.io/badge/NuGet-RuntimeGateway.Grpc-green?logo=nuget)](https://www.nuget.org/packages/Microsoft.AutoGen.RuntimeGateway.Grpc/) | [![PyPi autogenstudio](https://img.shields.io/badge/PyPi-autogenstudio-purple?logo=pypi)](https://pypi.org/project/autogenstudio/)                          |

</div>

Interested in contributing? See [CONTRIBUTING.md](./CONTRIBUTING.md) for guidelines. As AutoGen is in maintenance mode, contributions are limited to bug fixes, security patches, and documentation improvements. For feature development, consider contributing to [Microsoft Agent Framework](https://github.com/microsoft/agent-framework).

Have questions? Check out our [Frequently Asked Questions (FAQ)](./FAQ.md) for answers to common queries. Community support is available through [GitHub Discussions](https://github.com/microsoft/autogen/discussions) and the [Discord server](https://aka.ms/autogen-discord), though response times may vary as AutoGen is now community-managed. For actively supported tooling, see [Microsoft Agent Framework](https://github.com/microsoft/agent-framework).

## Legal Notices

Microsoft and any contributors grant you a license to the Microsoft documentation and other content
in this repository under the [Creative Commons Attribution 4.0 International Public License](https://creativecommons.org/licenses/by/4.0/legalcode),
see the [LICENSE](LICENSE) file, and grant you a license to any code in the repository under the [MIT License](https://opensource.org/licenses/MIT), see the
[LICENSE-CODE](LICENSE-CODE) file.

Microsoft, Windows, Microsoft Azure, and/or other Microsoft products and services referenced in the documentation
may be either trademarks or registered trademarks of Microsoft in the United States and/or other countries.
The licenses for this project do not grant you rights to use any Microsoft names, logos, or trademarks.
Microsoft's general trademark guidelines can be found at <http://go.microsoft.com/fwlink/?LinkID=254653>.

Privacy information can be found at <https://go.microsoft.com/fwlink/?LinkId=521839>

Microsoft and any contributors reserve all other rights, whether under their respective copyrights, patents,
or trademarks, whether by implication, estoppel, or otherwise.

<p align="right" style="font-size: 14px; color: #555; margin-top: 20px;">
  <a href="#readme-top" style="text-decoration: none; color: blue; font-weight: bold;">
    ↑ Back to Top ↑
  </a>
</p>