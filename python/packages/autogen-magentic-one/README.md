# 읽어보기

- 원문 저장소: `microsoft/autogen`
- 미러 저장소: `martinlee-git/autogen`
- 원문 문서: https://github.com/microsoft/autogen/blob/main/python/packages/autogen-magentic-one/README.md
- 미러 경로: `python/packages/autogen-magentic-one/README.md`

## 한글 요약

Magentic One 이제 Autogen AgentChat 라이브러리의 일부로 Magentic One을 사용할 수 있습니다. 자세한 내용은 사용자 가이드를 참조하세요. Magentic One의 원래 구현을 찾고 계십니까? 여기서 이용 가능합니다. Magentic One은 다양한 도메인에 걸쳐 개방형 웹 및 파일 기반 작업을 해결하기 위한 일반 다중 에이전트 시스템입니다. 이는 여러 에이전트 벤치마크에서 경쟁력 있는 성능을 달성하여 다중 에이전트 시스템의 중요한 발전을 의미합니다(자세한 내용은 기술 보고서 ​​참조). 2024년 11월에 처음 출시되었을 때 Magentic One은 Autogen 코어 라이브러리에서 직접 구현되었습니다. 이제 Autogen AgentChat을 사용하도록 Magentic One을 포팅하여 보다 모듈화되고 사용하기 쉬운 인터페이스를 제공합니다. 이를 위해 이전 구현은 더 이상 사용되지 않지만 https://github.com/microsoft/autogen/tree/v0.4.4/python/packages/autogen magentic에서 액세스할 수 있습니다. 앞으로 Magentic One 오케스트레이터인 MagenticOneGroupChat은 이제 단순히 AgentChat 팀이 되었습니다.

## 핵심 발췌

모든 표준 AgentChat 에이전트 및 기능을 rting합니다. 마찬가지로, Magentic One의 MultimodalWebSurfer, FileSurfer 및 MagenticOneCoderAgent 에이전트는 이제 모든 AgentChat 워크플로우에서 사용할 수 있는 AgentChat 에이전트로 광범위하게 제공됩니다. 마지막으로 최소한의 구성으로 논문에 나온 대로 이 모든 것을 함께 묶는 도우미 클래스인 MagenticOne이 있습니다.

## 원문 내용

# Magentic-One

> Magentic-One is now available as part of the `autogen-agentchat` library.
> Please see the [user guide](https://microsoft.github.io/autogen/stable/user-guide/agentchat-user-guide/magentic-one.html) for information.

> Looking for the original implementation of Magentic-One? It is available [here](https://github.com/microsoft/autogen/tree/v0.4.4/python/packages/autogen-magentic-one).

[Magentic-One](https://aka.ms/magentic-one-blog) is a generalist multi-agent system for solving open-ended web and file-based tasks across a variety of domains. It represents a significant step forward for multi-agent systems, achieving competitive performance on a number of agentic benchmarks (see the [technical report](https://arxiv.org/abs/2411.04468) for full details).

When originally released in [November 2024](https://aka.ms/magentic-one-blog) Magentic-One was [implemented directly on the `autogen-core` library](https://github.com/microsoft/autogen/tree/v0.4.4/python/packages/autogen-magentic-one). We have now ported Magentic-One to use `autogen-agentchat`, providing a more modular and easier to use interface. To this end, the older implementation is deprecated, but can be accessed at [https://github.com/microsoft/autogen/tree/v0.4.4/python/packages/autogen-magentic-one](https://github.com/microsoft/autogen/tree/v0.4.4/python/packages/autogen-magentic-one).

Moving forward, the Magentic-One orchestrator [MagenticOneGroupChat](https://microsoft.github.io/autogen/stable/reference/python/autogen_agentchat.teams.html#autogen_agentchat.teams.MagenticOneGroupChat) is now simply an AgentChat team, supporting all standard AgentChat agents and features. Likewise, Magentic-One's [MultimodalWebSurfer](https://microsoft.github.io/autogen/stable/reference/python/autogen_ext.agents.web_surfer.html#autogen_ext.agents.web_surfer.MultimodalWebSurfer), [FileSurfer](https://microsoft.github.io/autogen/stable/reference/python/autogen_ext.agents.file_surfer.html#autogen_ext.agents.file_surfer.FileSurfer), and [MagenticOneCoderAgent](https://microsoft.github.io/autogen/stable/reference/python/autogen_ext.teams.magentic_one.html) agents are now broadly available as AgentChat agents, to be used in any AgentChat workflows.

Lastly, there is a helper class, [MagenticOne](https://microsoft.github.io/autogen/stable/reference/python/autogen_ext.teams.magentic_one.html#autogen_ext.teams.magentic_one.MagenticOne), which bundles all of this together as it was in the paper with minimal configuration

## Citation

```
@misc{fourney2024magenticonegeneralistmultiagentsolving,
      title={Magentic-One: A Generalist Multi-Agent System for Solving Complex Tasks},
      author={Adam Fourney and Gagan Bansal and Hussein Mozannar and Cheng Tan and Eduardo Salinas and Erkang and Zhu and Friederike Niedtner and Grace Proebsting and Griffin Bassman and Jack Gerrits and Jacob Alber and Peter Chang and Ricky Loynd and Robert West and Victor Dibia and Ahmed Awadallah and Ece Kamar and Rafah Hosn and Saleema Amershi},
      year={2024},
      eprint={2411.04468},
      archivePrefix={arXiv},
      primaryClass={cs.AI},
      url={https://arxiv.org/abs/2411.04468},
}
```