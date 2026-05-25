# 색인

- 원문 저장소: `microsoft/autogen`
- 미러 저장소: `martinlee-git/autogen`
- 원문 문서: https://github.com/microsoft/autogen/blob/main/docs/dotnet/index.md
- 미러 경로: `docs/dotnet/index.md`

## 한글 요약

비활성화Affix: true <div class="center" <h1 AutoGen .NET</h1 <p class="subheader" AI 에이전트 및 애플리케이션 구축을 위한 <i .NET</i 프레임워크 </p </div <div class="row" <div class="col sm 6" <div class="card" <div class="card body" <h5 class="card title" Core</h5 <p </p <p class="card text" 구축을 위한 이벤트 기반 프로그래밍 프레임워크 확장 가능한 다중 에이전트 AI 시스템.</p 비즈니스 프로세스를 위한 결정적이고 동적 에이전트 워크플로 다중 에이전트 협업에 대한 연구 다국어 애플리케이션을 위한 분산 에이전트 이벤트 중심 클라우드 네이티브 애플리케이션과 통합 워크플로 또는 분산 에이전트 시스템을 구축하는 경우 여기에서 시작하세요. </div </div </div <div class="col sm 6" <div class="card" <div class="card body" <h5 class="card title" AgentChat</h5 <p class="card text" 대화식 노래를 만들기 위한 프로그래밍 프레임워크

## 핵심 발췌

파일 및 다중 에이전트 애플리케이션. 코어를 기반으로 제작되었습니다.</p <a href="#" class="btn btnprimarydisabled" 출시 예정</a </div </div </div </div

## 원문 내용

---
_disableAffix: true
---

<div class="center">
    <h1>AutoGen .NET</h1>
    <p class="subheader">
    A <i>.NET</i> framework for building AI agents and applications
    </p>
</div>

<div class="row">
  <div class="col-sm-6">
    <div class="card">
      <div class="card-body">
        <h5 class="card-title">Core</h5>
<p>

[![dotnet-ci](https://github.com/microsoft/autogen/actions/workflows/dotnet-build.yml/badge.svg)](https://github.com/microsoft/autogen/actions/workflows/dotnet-build.yml)
[![NuGet version](https://badge.fury.io/nu/Microsoft.AutoGen.Contracts.svg)](https://badge.fury.io/nu/Microsoft.AutoGen.Contracts)
[![NuGet version](https://badge.fury.io/nu/Microsoft.AutoGen.Core.svg)](https://badge.fury.io/nu/Microsoft.AutoGen.Core)
[![NuGet version](https://badge.fury.io/nu/Microsoft.AutoGen.Core.Grpc.svg)](https://badge.fury.io/nu/Microsoft.AutoGen.Core.Grpc)
[![NuGet version](https://badge.fury.io/nu/Microsoft.AutoGen.RuntimeGateway.Grpc.svg)](https://badge.fury.io/nu/Microsoft.AutoGen.RuntimeGateway.Grpc)
[![NuGet version](https://badge.fury.io/nu/Microsoft.AutoGen.AgentHost.svg)](https://badge.fury.io/nu/Microsoft.AutoGen.AgentHost)

</p>
        <p class="card-text">An event-driven programming framework for building scalable multi-agent AI systems.</p>

- Deterministic and dynamic agentic workflows for business processes
- Research on multi-agent collaboration
- Distributed agents for multi-language applications
- integration with event-driven, cloud native applications

*Start here if you are building workflows or distributed agent systems*

<p>
<div class="highlight">
<pre id="codecell0" tabindex="0">

```bash
dotnet add package Microsoft.AutoGen.Contracts
dotnet add package Microsoft.AutoGen.Core

# optionally - for distributed agent systems:
dotnet add package Microsoft.AutoGen.RuntimeGateway.Grpc
dotnet add package Microsoft.AutoGen.AgentHost

# other optional packages
dotnet add package Microsoft.AutoGen.Agents
dotnet add package Microsoft.AutoGen.Extensions.Aspire
dotnet add package Microsoft.AutoGen.Extensions.MEAI
dotnet add package Microsoft.AutoGen.Extensions.SemanticKernel
```

</pre></div></p>
<p>
        <a href="core/index.md" class="btn btn-primary">Get started</a>
      </div>
    </div>
  </div>
  <div class="col-sm-6">
    <div class="card">
      <div class="card-body">
        <h5 class="card-title">AgentChat</h5>
        <p class="card-text">A programming framework for building conversational single and multi-agent applications. Built on Core.</p>
        <a href="#" class="btn btn-primary disabled">Coming soon</a>
      </div>
    </div>
  </div>
</div>