# 03 - 에이전트 작업자 프로토콜

- 원문 저장소: `microsoft/autogen`
- 미러 저장소: `martinlee-git/autogen`
- 원문 문서: https://github.com/microsoft/autogen/blob/main/docs/design/03 - Agent Worker Protocol.md
- 미러 경로: `docs/design/03 - Agent Worker Protocol.md`

## 한글 요약

에이전트 작업자 프로토콜 시스템 아키텍처 시스템은 여러 프로세스로 구성되며 각 프로세스는 서비스 프로세스 또는 작업자 프로세스입니다. 작업자는 호스트 애플리케이션 코드(에이전트)를 처리하고 서비스 프로세스에 연결합니다. 작업자는 자신이 지원하는 에이전트를 서비스에 알리므로 서비스는 에이전트를 배치할 작업자를 결정할 수 있습니다. 서비스 프로세스는 작업자 프로세스에서 에이전트 배치를 조정하고 에이전트 간의 통신을 촉진합니다. 에이전트 인스턴스는 (네임스페이스: str, 이름: str)의 튜플로 식별됩니다. 네임스페이스와 이름은 모두 애플리케이션에서 정의됩니다. 네임스페이스에는 시스템에서 암시하는 의미가 없습니다. 이는 자유 형식이며 모든 의미는 애플리케이션 코드에 의해 구현됩니다. 이름은 해당 이름을 가진 에이전트를 지원하는 작업자에게 요청을 라우팅하는 데 사용됩니다. 작업자는 서비스에 호스팅할 수 있는 에이전트 이름 집합을 광고합니다. 작업자는 서비스에서 받은 메시지에 대한 응답으로 에이전트를 활성화합니다. 서비스는 이름을 사용하여

## 핵심 발췌

e 현재 비활성 에이전트를 배치할 위치는 에이전트 이름에서 해당 에이전트를 지원하는 작업자 집합으로의 매핑을 유지 관리합니다. 서비스는 식별된 에이전트를 호스팅하는 작업자 프로세스에 활성 에이전트 ID를 매핑하는 디렉터리를 유지 관리합니다. 에이전트 수명 주기 에이전트는 명시적으로 생성되거나 삭제되지 않습니다. 현재 활성화되지 않은 에이전트에 대한 요청이 수신되면 해당 에이전트를 호스팅할 수 있는 작업자를 선택하고 해당 작업자에게 요청을 라우팅하는 것은 서비스의 책임입니다. 작업자 프로토콜 흐름 작업자 프로토콜은 작업자 수명에 따라 초기화, 작업 및 종료의 세 단계로 구성됩니다. 초기화 작업자 프로세스가 시작되면 서비스 프로세스에 대한 연결을 시작하여 양방향 통신 연결을 설정합니다.

## 원문 내용

# Agent Worker Protocol

## System architecture

The system consists of multiple processes, each being either a _service_ process or a _worker_ process.
Worker processes host application code (agents) and connect to a service process.
Workers advertise the agents which they support to the service, so the service can decide which worker to place agents on.
Service processes coordinate placement of agents on worker processes and facilitate communication between agents.

Agent instances are identified by the tuple of `(namespace: str, name: str)`.
Both _namespace_ and _name_ are application-defined.
The _namespace_ has no semantics implied by the system: it is free-form, and any semantics are implemented by application code.
The _name_ is used to route requests to a worker which supports agents with that name.
Workers advertise the set of agent names which they are capable of hosting to the service.
Workers activate agents in response to messages received from the service.
The service uses the _name_ to determine where to place currently-inactive agents, maintaining a mapping from agent name to a set of workers which support that agent.
The service maintains a _directory_ mapping active agent ids to worker processes which host the identified agent.

### Agent lifecycle

Agents are never explicitly created or destroyed. When a request is received for an agent which is not currently active, it is the responsibility of the service to select a worker which is capable of hosting that agent, and to route the request to that worker.

## Worker protocol flow

The worker protocol has three phases, following the lifetime of the worker: initialization, operation, and termination.

### Initialization

When the worker process starts, it initiates a connection to a service process, establishing a bi-directional communication channel which messages are passed across.
Next, the worker issues zero or more `RegisterAgentType(name: str)` messages, which tell the service the names of the agents which it is able to host.

* TODO: What other metadata should the worker give to the service?
* TODO: Should we give the worker a unique id which can be used to identify it for its lifetime? Should we allow this to be specified by the worker process itself?

### Operation

Once the connection is established, and the service knows which agents the worker is capable of hosting, the worker may begin receiving requests for agents which it must host.
Placement of agents happens in response to an `Event(...)` or `RpcRequest(...)` message.
The worker maintains a _catalog_ of locally active agents: a mapping from agent id to agent instance.
If a message arrives for an agent which does not have a corresponding entry in the catalog, the worker activates a new instance of that agent and inserts it into the catalog.
The worker dispatches the message to the agent:

* For an `Event`, the agent processes the message and no response is generated.
* For an `RpcRequest` message, the agent processes the message and generates a response of type `RpcResponse`. The worker routes the response to the original sender.

The worker maintains a mapping of outstanding requests, identified by `RpcRequest.id`, to a promise for a future `RpcResponse`.
When an `RpcResponse` is received, the worker finds the corresponding request id and fulfils the promise using that response.
If no response is received in a specified time frame (eg, 30s), the worker breaks the promise with a timeout error.

### Termination

When the worker is ready to shutdown, it closes the connection to the service and terminates. The service de-registers the worker and all agent instances which were hosted on it.