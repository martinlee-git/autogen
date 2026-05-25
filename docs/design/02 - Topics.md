# 02 - 주제

- 원문 저장소: `microsoft/autogen`
- 미러 저장소: `martinlee-git/autogen`
- 원문 문서: https://github.com/microsoft/autogen/blob/main/docs/design/02 - Topics.md
- 미러 경로: `docs/design/02 - Topics.md`

## 한글 요약

주제 이 문서에서는 메시지 게시 및 주제 구독의 의미와 구성 요소를 설명합니다. 개요 주제는 특정 게시 메시지를 수신하는 에이전트를 관리하기 위한 기본 요소로 사용됩니다. 에이전트는 주제를 구독합니다. 주제에서 에이전트 인스턴스로의 매핑을 정의한 애플리케이션이 있습니다. 이러한 개념은 의도적으로 CloudEvents 사양에 매핑됩니다. 이를 통해 기존 시스템 및 도구와 쉽게 통합할 수 있습니다. 목표가 아님 이 문서는 RPC/직접 메시징 식별자를 지정하지 않습니다. 주제는 두 가지 구성 요소(TopicId라고 함)로 식별됩니다. 유형은 발생하는 이벤트 유형을 나타내며, 이는 정적이며 코드에 정의됩니다. 이름 충돌을 피하기 위해 역 도메인 이름 표기법을 사용해야 합니다. 예: com.example.my 주제. 허용되는 값은 정규식과 일치해야 합니다. ^[\w\ \.\:\=]+\Z 특히 이는 = 및 : 문자가 추가된 에이전트 유형과 동일합니다. 소스는 이벤트가 발생한 위치를 나타내며, 이는 동적이며 메시지 자체를 기반으로 해야 합니다.

## 핵심 발췌

URI 에이전트 인스턴스는 두 가지 구성 요소(AgentId라고 함)로 식별됩니다. 유형은 에이전트 유형을 나타내며 이는 정적이며 코드에 정의되어 있습니다. 허용되는 값은 정규식과 일치해야 합니다. ^[\w\ \.]+\Z 키는 키에 대한 에이전트 유형의 인스턴스를 나타냅니다. URI여야 합니다. 예: GraphicDesigner:1234 구독 구독은 어떤 에이전트가 주제에 게시된 메시지를 수신하는지 정의합니다. 구독은 동적이며 언제든지 추가하거나 제거할 수 있습니다. 구독은 다음 두 가지를 정의합니다. TopicId bool 유형의 Matcher func, "이 구독이 이 주제와 일치합니까?"를 알려주는 TopicId AgentId 유형의 Mapper func, "이 구독이 이 주제와 일치하면 어떤 에이전트에 매핑하는지"를 알려줍니다. 이러한 함수는 평가를 캐시할 수 있도록 부작용이 없어야 합니다. 에이전트

## 원문 내용

# Topics

This document describes the semantics and components of publishing messages and subscribing to topics.

## Overview

Topics are used as the primitive to manage which agents receive a given published message. Agents subscribe to topics. There is an application defined mapping from topic to agent instance.

These concepts intentionally map to the [CloudEvents](https://cloudevents.io/) specification. This allows for easy integration with existing systems and tools.

### Non-goals

This document does not specify RPC/direct messaging

## Identifiers

A topic is identified by two components (called a `TopicId`):

- [`type`](https://github.com/cloudevents/spec/blob/v1.0.2/cloudevents/spec.md#type) - represents the type of event that occurs, this is static and defined in code
  - SHOULD use reverse domain name notation to avoid naming conflicts. For example: `com.example.my-topic`.
  - Allowed values MUST match the regex: `^[\w\-\.\:\=]+\Z`
  - Notably, this is the same as agent type with the addition of `=` and `:` characters
- [`source`](https://github.com/cloudevents/spec/blob/v1.0.2/cloudevents/spec.md#source-1) - represents where the event originated from, this is dynamic and based on the message itself
  - SHOULD be a URI

Agent instances are identified by two components (called an `AgentId`):

- `type` - represents the type of agent, this is static and defined in code
  - Allowed values MUST match the regex: `^[\w\-\.]+\Z`
- `key` - represents the instance of the agent type for the key
  - SHOULD be a URI

For example: `GraphicDesigner:1234`

## Subscriptions

Subscriptions define which agents receive messages published to a topic. Subscriptions are dynamic and can be added or removed at any time.

A subscription defines two things:

- Matcher func of type `TopicId -> bool`, telling us "does this subscription match this topic"
- Mapper func of type `TopicId -> AgentId`, telling us "given this subscription matches this topic, which agent does it map to"

These functions MUST be be free of side effects such that the evaluation can be cached.

### Agent instance creation

If a message is received on a topic that maps to an agent that does not yet exist the runtime will instantiate an agent to fullfil the request.

## Message types

Agents are able to handle certain types of messages. This is an internal detail of an agent's implementation. All agents in a channel will receive all messages, but will ignore messages that it cannot handle.

> [!NOTE]
> This might be revisited based on scaling and performance considerations.

## Well known topic types

Agents should subscribe via a prefix subscription to the `{AgentType}:` topic as a direct message channel for the agent type.

For this subscription source should map directly to agent key.

This subscription will therefore receive all events for the following well known topics:

- `{AgentType}:` - General purpose direct messages. These should be routed to the appropriate message handler.
- `{AgentType}:rpc_request={RequesterAgentType}` - RPC request messages. These should be routed to the appropriate RPC handler, and RequesterAgentType used to publish the response
- `{AgentType}:rpc_response={RequestId}` - RPC response messages. These should be routed back to the response future of the caller.
- `{AgentType}:error={RequestId}` - Error message that corresponds to the given request.