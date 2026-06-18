# 지도 시간

- 원문 저장소: `microsoft/autogen`
- 미러 저장소: `martinlee-git/autogen`
- 원문 문서: https://github.com/microsoft/autogen/blob/main/docs/dotnet/core/tutorial.md
- 미러 경로: `docs/dotnet/core/tutorial.md`

## 한글 요약

자습서 [!TIP] 코드만 보고 싶다면 여기에서 전체 샘플을 프로젝트로 사용할 수 있습니다. 이 튜토리얼에서는 10에서 1까지 카운트다운하는 두 개의 에이전트인 Modifier와 Checker를 정의할 것입니다. Modifier 에이전트는 카운트를 수정하고 Checker 에이전트는 카운트를 확인하고 카운트가 1에 도달하면 애플리케이션을 중지합니다. 메시지 유형 정의 가장 먼저 해야 할 일은 에이전트 간에 전달될 메시지를 정의하는 것입니다. 우리는 이를 클래스로 정의할 것입니다. CountMessage를 사용하여 현재 개수를 전달하고 CountUpdate를 사용하여 업데이트된 개수를 전달하겠습니다. !code csharp[] !code csharp[] 메시지 유형을 강력한 유형의 클래스로 분리함으로써 에이전트가 특정 유형에 반응하고 특정 유형을 생성하는 워크플로를 구축할 수 있습니다. BaseAgent에서 상속되는 에이전트 만들기 AutoGen에서 에이전트는 메시지를 받고 보낼 수 있는 클래스입니다. 에이전트는 수신한 메시지로 수행할 작업에 대한 자체 논리를 정의합니다. a를 정의하려면

## 핵심 발췌

gent, 다음과 같이 @Microsoft.AutoGen.Core.BaseAgent에서 상속되는 클래스를 만듭니다. 에이전트가 생성될 때 에이전트에 인수를 전달하는 방법을 살펴보겠습니다. 하지만 지금은 @Microsoft.AutoGen.Contracts.AgentId 및 @Microsoft.AutoGen.Core.IAgentRuntime이 항상 생성자에 전달되고 이러한 내용이 기본 클래스 생성자에 전달되어야 한다는 점만 알아야 합니다. 다른 두 인수는 에이전트에 대한 설명과 선택적 로거입니다. 여기에서 에이전트 ID가 무엇인지 자세히 알아보세요. 핸들러 생성 이제 Modifier가 CountMessage를 수신하고 카운트를 수정한 후 CountUpdate를 생성하도록 합니다. 이를 위해서는 IHandle<CountMessage 인터페이스를 구현해야 합니다. 구독 추가 CountMessage가 이 에이전트에 전달될 때 호출될 함수를 정의했지만

## 원문 내용

# Tutorial

> [!TIP]
> If you'd prefer to just see the code the entire sample is available as a [project here](https://github.com/microsoft/autogen/tree/main/dotnet/samples/GettingStarted).

In this tutorial we are going to define two agents, `Modifier` and `Checker`, that will count down from 10 to 1. The `Modifier` agent will modify the count and the `Checker` agent will check the count and stop the application when the count reaches 1.

## Defining the message types

The first thing we need to do is to define the messages that will be passed between the agents, we're simply going to define them as classes.

We're going to use `CountMessage` to pass the current count and `CountUpdate` to pass the updated count.

[!code-csharp[](../../../dotnet/samples/GettingStarted/CountMessage.cs#snippet_CountMessage)]
[!code-csharp[](../../../dotnet/samples/GettingStarted/CountUpdate.cs#snippet_CountUpdate)]

By separating out the message types into strongly typed classes, we can build a workflow where agents react to certain types and produce certain types.

## Creating the agents

### Inherit from `BaseAgent`

In AutoGen an agent is a class that can receive and send messages. The agent defines its own logic of what to do with the messages it receives. To define an agent, create a class that inherits from @Microsoft.AutoGen.Core.BaseAgent, like so:

```csharp
using Microsoft.AutoGen.Contracts;
using Microsoft.AutoGen.Core;

public class Modifier(
    AgentId id,
    IAgentRuntime runtime,
    ) :
        BaseAgent(id, runtime, "MyAgent", null),
{
}
```

We will see how to pass arguments to an agent when it is constructed, but for now you just need to know that @Microsoft.AutoGen.Contracts.AgentId and @Microsoft.AutoGen.Core.IAgentRuntime will always be passed to the constructor, and those should be forwarded to the base class constructor. The other two arguments are a description of the agent and an optional logger.

Learn more about what an Agent ID is [here](https://microsoft.github.io/autogen/stable/user-guide/core-user-guide/core-concepts/agent-identity-and-lifecycle.html#agent-id).

### Create a handler

Now, we want `Modifier` to receive `CountMessage` and produce `CountUpdate` after it modifies the count. To do this, we need to implement the `IHandle<CountMessage>` interface:

```csharp
public class Modifier(
    // ...
    ) :
        BaseAgent(...),
        IHandle<CountMessage>
{

    public async ValueTask HandleAsync(CountMessage item, MessageContext messageContext)
    {
        // ...
    }
}
```

### Add a subscription

We've defined a function that will be called when a `CountMessage` is delivered to this agent, but there is still one step before the message will actually be delivered to the agent. The agent must subscribe to the topic to the message is published to. We can do this by adding the `TypeSubscription` attribute to the class:

```csharp
[TypeSubscription("default")]
public class Modifier(
    // ...
```

Learn more about topics and subscriptions [here](https://microsoft.github.io/autogen/stable/user-guide/core-user-guide/core-concepts/topic-and-subscription.html).

### Publish a message

Now that we have a handler for `CountMessage`, and we have the subscription in place we can publish a result out of the handler.

```csharp
public async ValueTask HandleAsync(CountMessage item, MessageContext messageContext)
{
    int newValue = item.Content - 1;
    Console.WriteLine($"\nModifier:\nModified {item.Content} to {newValue}");

    CountUpdate updateMessage = new CountUpdate { NewCount = newValue };
    await this.PublishMessageAsync(updateMessage, topic: new TopicId("default"));
}
```

You'll notice that when we publish the message, we specify the topic to publish to. We're using a topic called `default` in this case, which is the same topic which we subscribed to. We could have used a different topic, but in this case we're keeping it simple.

### Passing arguments to the agent

Let's extend our agent to make what we do to the count configurable. We'll do this by passing a function to the agent that will be used to modify the count.

```csharp
using ModifyF = System.Func<int, int>;

// ...

[TypeSubscription("default")]
public class Modifier(
    AgentId id,
    IAgentRuntime runtime,
    ModifyF modifyFunc // <-- Add this
    ) :
        BaseAgent(...),
        IHandle<CountMessage>
{

    public async ValueTask HandleAsync(CountMessage item, MessageContext messageContext)
    {
        int newValue = modifyFunc(item.Content); // <-- use it here

        // ...
    }
}

```

### Final Modifier implementation

Here is the final implementation of the Modifier agent:

[!code-csharp[](../../../dotnet/samples/GettingStarted/Modifier.cs#snippet_Modifier)]

### Checker

We'll also define a Checker agent that will check the count and stop the application when the count reaches 1. Additionally, we'll use dependency injection to get a reference to the `IHostApplicationLifetime` service, which we can use to stop the application.

[!code-csharp[](../../../dotnet/samples/GettingStarted/Checker.cs#snippet_Checker)]

## Putting it all together

Now that we have our agents defined, we can put them together in a simple application that will count down from 10 to 1.

After includes, the first thing to do is to define the two functions for modifying and checking for completion.

[!code-csharp[](../../../dotnet/samples/GettingStarted/Program.cs#snippet_Program_funcs)]

Then, we create a builder and do the following things:

- Specify that we are using the in process runtime
- Register our functions as services
- Register the agent classes we defined earlier
- Finally, build and start our app

[!code-csharp[](../../../dotnet/samples/GettingStarted/Program.cs#snippet_Program_builder)]

The app is now running, but we need to kick off the process with a message. We do this by publishing a `CountMessage` with an initial value of 10.
Importantly we publish this to the "default" topic which is what our agents are subscribed to. Finally, we wait for the application to stop.

[!code-csharp[](../../../dotnet/samples/GettingStarted/Program.cs#snippet_Program_publish)]

That's it! You should see the count down from 10 to 1 in the console.

Here's the full code for the `Program` class:

[!code-csharp[](../../../dotnet/samples/GettingStarted/Program.cs#snippet_Program)]

## Things to try

Here are some ideas to try with this sample:

- Change the initial count
- Create a new modifier function that counts up instead. (Don't forget to change the checker too!)
- Create an agent that outputs to the console instead of the modifier or checker agent doing it themselves (hint: use a new message type)