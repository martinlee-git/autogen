# 01 - 프로그래밍 모델

- 원문 저장소: `microsoft/autogen`
- 미러 저장소: `martinlee-git/autogen`
- 원문 문서: https://github.com/microsoft/autogen/blob/main/docs/design/01 - Programming Model.md
- 미러 경로: `docs/design/01 - Programming Model.md`

## 한글 요약

프로그래밍 모델 워크플로를 이해하고 이를 에이전트에 매핑하는 것이 AutoGen에서 에이전트 시스템을 구축하는 열쇠입니다. 프로그래밍 모델은 기본적으로 게시 구독입니다. 에이전트는 관심 있는 이벤트를 구독하고 다른 에이전트가 관심을 가질 만한 이벤트를 게시할 수도 있습니다. 상담원은 메모리, 프롬프트, 데이터 소스, 스킬(외부 API)과 같은 추가 자산을 보유할 수도 있습니다. CloudEvents로 전달되는 이벤트 시스템의 각 이벤트는 CloudEvents 사양을 사용하여 정의됩니다. 이를 통해 다양한 시스템과 언어에서 사용할 수 있는 공통 이벤트 형식이 가능해졌습니다. CloudEvents에서 각 이벤트에는 다음을 포함해야 하는 "컨텍스트 속성"이 있습니다. 1. id 고유 ID(예: UUID)입니다. 2. 소스 이벤트의 출처를 나타내는 URI 또는 ​​URN입니다. 3. 역방향 DNS 이름이 앞에 붙은 이벤트의 네임스페이스를 입력합니다. 접두사가 붙은 도메인은 이 이벤트 유형의 의미를 정의하는 조직을 나타냅니다(예: com.github.pull request.opened 또는 com.example.object.deleted.v2). 선택적으로 필드 d

## 핵심 발췌

데이터 스키마/콘텐츠 유형 또는 확장을 기술합니다. 이벤트 핸들러 각 에이전트에는 CloudEvents 유형에 대한 특정 일치 항목에 바인딩되는 이벤트 핸들러 세트가 있습니다. 이벤트 처리기는 정확한 유형과 일치하거나 유형 계층 구조에서 특정 수준의 이벤트 패턴과 일치할 수 있습니다(예: 시스템 네임스페이스의 모든 이벤트에 대해 com.Microsoft.AutoGen.Agents.System.). 각 이벤트 처리기는 상태를 변경하고, 모델을 호출하고, 메모리에 액세스하고, 외부 도구를 호출하고, 다른 이벤트를 내보내고, 다른 시스템과 데이터를 주고받을 수 있는 함수입니다. 각 이벤트 핸들러는 간단한 함수일 수도 있고 상태 시스템이나 기타 제어 논리를 사용하는 더 복잡한 함수일 수도 있습니다. 에이전트 조정 외부 이벤트에만 반응하는 기능적이고 확장 가능한 에이전트 시스템을 구축하는 것이 가능합니다. 많은 경우에, h

## 원문 내용

# Programming Model

Understanding your workflow and mapping it to agents is the key to building an agent system in AutoGen.

The programming model is basically publish-subscribe. Agents subscribe to events they care about and also can publish events that other agents may care about. Agents may also have additonal assets such as Memory, prompts, data sources, and skills (external APIs).

## Events Delivered as CloudEvents

Each event in the system is defined using the [CloudEvents Specification](https://cloudevents.io/). This allows for a common event format that can be used across different systems and languages. In CloudEvents, each event has "Context Attributes" that must include:

1. *id* - A unique id (eg. a UUID).
2. *source* - A URI or URN indicating the event's origin.
3. *type* - The namespace of the event - prefixed with a reverse-DNS name.
   - The prefixed domain dictates the organization which defines the semantics of this event type: e.g (`com.github.pull_request.opened` or `com.example.object.deleted.v2`), and optionally fields describing the data schema/content-type or extensions.

## Event Handlers

Each agent has a set of event handlers, that are bound to a specific match against a CloudEvents *type*. Event Handlers could match against an exact type or match for a pattern of events of a particular level in the type heirarchy (eg: `com.Microsoft.AutoGen.Agents.System.*` for all Events in the `System` namespace) Each event handler is a function that can change state, call models, access memory, call external tools, emit other events, and flow data to/from other systems. Each event handler can be a simple function or a more complex function that uses a state machine or other control logic.

## Orchestrating Agents

It is possible to build a functional and scalable agent system that only reacts to external events. In many cases, however, you will want to orchestrate the agents to achieve a specific goal or follow a pre-determined workflow. In this case, you will need to build an orchestrator agent that manages the flow of events between agents.

## Built-in Event Types

The AutoGen system comes with a set of built-in event types that are used to manage the system. These include:

- *System Events* - Events that are used to manage the system itself. These include events for starting and stopping the Agents, sending messages to all agents, and other system-level events.
- *Insert other types here*

## Agent Contracts

You may want to leverage more prescriptive agent behavior contracts, and AutoGen also includes base agents that implement different approaches to agent behavior, including layering request/response patterns on top of the event-driven model. For an example of this see the ChatAgents in the Python examples. In this case your agent will have a known set of events which it must implement and specific behaviors expected of those events.