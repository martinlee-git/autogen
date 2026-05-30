# Python과의 차이점

- 원문 저장소: `microsoft/autogen`
- 미러 저장소: `martinlee-git/autogen`
- 원문 문서: https://github.com/microsoft/autogen/blob/main/docs/dotnet/core/differences-from-python.md
- 미러 경로: `docs/dotnet/core/differences-from-python.md`

## 한글 요약

에이전트가 TLDR도 구독하는 주제에 대한 Python 게시와의 차이점 기본 동작은 동일합니다. 에이전트가 수신 대기 중인 주제에 메시지를 게시하면 메시지를 보낸 에이전트가 해당 메시지를 수신하지 않습니다. 이는 Python 런타임의 동작이기도 합니다. 그러나 이전 사용을 지원하려면 @Microsoft.AutoGen.Core.InProcessRuntime에서 TopicSubscription 특성의 @Microsoft.AutoGen.Core.InProcessRuntime.DeliverToSelf 속성을 true로 설정하여 에이전트가 보내는 메시지를 수신하도록 허용할 수 있습니다.

## 핵심 발췌

Python과의 차이점 ## 에이전트가 구독하는 주제에 게시 [!NOTE] TLDR; 기본 동작은 동일합니다. 에이전트가 수신 대기 중인 주제에 메시지를 게시하면 해당 메시지는

## 원문 내용

# Differences from Python

## Publishing to a topic that an agent is also subscribed to

> [!NOTE]
> TLDR; Default behavior is identical.

When an agent publishes a message to a topic to which it also listens, the message will not be received by the agent that sent it. This is also the behavior in the Python runtime. However to support previous usage, in @Microsoft.AutoGen.Core.InProcessRuntime, you can set the @Microsoft.AutoGen.Core.InProcessRuntime.DeliverToSelf property to true in the TopicSubscription attribute to allow an agent to receive messages it sends.