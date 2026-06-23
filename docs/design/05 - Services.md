# 05 - 서비스

- 원문 저장소: `microsoft/autogen`
- 미러 저장소: `martinlee-git/autogen`
- 원문 문서: https://github.com/microsoft/autogen/blob/main/docs/design/05 - Services.md
- 미러 경로: `docs/design/05 - Services.md`

## 한글 요약

AutoGen 서비스 개요 각 AutoGen 에이전트 시스템에는 하나 이상의 에이전트 작업자와 에이전트 관리/지원을 위한 서비스 세트가 있습니다. 서비스와 작업자는 모두 동일한 프로세스 또는 분산 시스템에서 호스팅될 수 있습니다. 동일한 프로세스에서 통신 및 이벤트 전달이 메모리에 있을 때. 배포되면 작업자는 gRPC를 통해 서비스와 통신합니다. 모든 경우에 이벤트는 CloudEvents로 패키지됩니다. 백엔드 서비스에는 여러 가지 옵션이 있습니다. 메모리 내: 에이전트 작업자 및 서비스는 모두 동일한 프로세스에서 호스팅되며 메모리 채널을 통해 통신합니다. Python 및 .NET에서 사용할 수 있습니다. Python 전용: 에이전트 작업자는 메모리 내 메시지 버스 및 에이전트 레지스트리를 구현하는 Python 호스팅 서비스와 통신합니다. Micrososft Orleans: 서비스와 작업자를 호스팅할 수 있고, 영구 스토리지로 분산 상태를 활성화하고, 여러 이벤트 버스 유형과 언어 간 에이전트 통신을 활용할 수 있는 분산 행위자 시스템입니다. 로드맵: 다른 언어 지원

## 핵심 발췌

dapr 또는 Akka와 같은 분산 시스템을 사용합니다. 시스템의 서비스는 다음과 같습니다. 작업자: 에이전트를 호스팅하고 게이트웨이에 대한 클라이언트입니다. 게이트웨이: 다른 서비스 API를 위한 RPC 게이트웨이 작업자와 이벤트 버스 메시지 세션 상태 사이에 RPC 브리지를 제공합니다. 메시지 세션 상태(메시지 큐/전달 추적) 레지스트리: 시스템의 {에이전트:에이전트 유형}:{구독/주제} 및 처리할 수 있는 이벤트를 추적합니다. 로드맵: 게이트웨이에 조회 API 추가 AgentState: 에이전트에 대한 영구 상태 라우팅: 이벤트를 기반으로 에이전트에 이벤트를 전달합니다. 구독+주제 로드맵: 구독 관리 API 추가 로드맵: 에이전트 시스템용 관리 API 로드맵: 예약: 에이전트 배치 관리 로드맵: 검색: 에이전트 및 서비스 검색 허용

## 원문 내용

# AutoGen Services

## Overview

Each AutoGen agent system has one or more Agent Workers and a set of services for managing/supporting the agents. The services and workers can all be hosted in the same process or in a distributed system.  When in the same process communication and event delivery is in-memory. When distributed, workers communicate with the service over gRPC. In all cases, events are packaged as CloudEvents. There are multiple options for the backend services:

- In-Memory: the Agent Workers and Services are all hosted in the same process and communicate over in-memory channels. Available for python and .NET.
- Python only: Agent workers communicate with a python hosted service that implements an in-memory message bus and agent registry.
- Micrososft Orleans: a distributed actor system that can host the services and workers, enables distributed state with persistent storage, can leverage multiple event bus types, and cross-language agent communication.
- *Roadmap: support for other languages distributed systems such as dapr or Akka.*

The Services in the system include:

- Worker: Hosts the Agents and is a client to the Gateway
- Gateway:
-- RPC gateway for the other services APIs
-- Provides an RPC bridge between the workers and the Event Bus
-- Message Session state (track message queues/delivery)
- Registry: keeps track of the {agents:agent types}:{Subscription/Topics} in the system and which events they can handle
-- *Roadmap: add lookup api in gateway*
- AgentState: persistent state for agents
- Routing: delivers events to agents based on their subscriptions+topics
-- *Roadmap: add subscription management APIs*
- *Roadmap: Management APIs for the Agent System*
- *Roadmap: Scheduling: manages placement of agents*
- *Roadmap: Discovery: allows discovery of agents and services*