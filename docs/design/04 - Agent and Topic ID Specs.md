# 04 - 상담원 및 주제 ID 사양

- 원문 저장소: `microsoft/autogen`
- 미러 저장소: `martinlee-git/autogen`
- 원문 문서: https://github.com/microsoft/autogen/blob/main/docs/design/04 - Agent and Topic ID Specs.md
- 미러 경로: `docs/design/04 - Agent and Topic ID Specs.md`

## 한글 요약

에이전트 및 주제 ID 사양 이 문서에서는 에이전트 ID 및 주제 ID의 구조, 제약 조건 및 동작을 설명합니다. 에이전트 ID 필수 속성 유형 유형: 문자열 설명: 에이전트 유형이 에이전트 클래스가 아닙니다. 에이전트를 동일한 에이전트 유형의 에이전트 인스턴스를 생성하는 특정 팩토리 기능과 연관시킵니다. 예를 들어, 서로 다른 팩토리 함수는 동일한 에이전트 클래스를 생성할 수 있지만 생성자 매개변수는 다릅니다. 제약 조건: UTF8이며 영숫자 문자(a z) 및 (0 9) 또는 밑줄(\ )만 포함합니다. 유효한 식별자는 숫자로 시작하거나 공백을 포함할 수 없습니다. 예: 코드 검토자 WebSurfer UserProxy 키 유형: 문자열 설명: 에이전트 키는 지정된 에이전트 유형에 대한 인스턴스 식별자입니다. 제약 조건: UTF8 및 ASCII 32(공백)에서 126( ) 사이의 문자만 포함합니다. 예: 기본값 메모리 주소 UUID 문자열 주제 ID 필수 속성 유형 유형: 문자열 설명: 주제 유형은 일반적으로 애플리케이션에 의해 정의됩니다.

## 핵심 발췌

n 주제의 메시지 유형을 표시하는 코드입니다. 제약 조건: UTF8이며 영숫자 문자(a z) 및 (0 9), ':', '=' 또는 밑줄(\)만 포함합니다. 유효한 식별자는 숫자로 시작하거나 공백을 포함할 수 없습니다. 예: GitHub 문제 소스 유형: 문자열 설명: 주제 소스는 주제 유형 내 주제에 대한 고유 식별자입니다. 일반적으로 애플리케이션 데이터에 의해 정의됩니다. 제약 조건: UTF8이며 ASCII 32(공백)에서 126( ) 사이의 문자만 포함합니다. 예: github.com/{repo 이름}/issues/{문제 번호}

## 원문 내용

# Agent and Topic ID Specs

This document describes the structure, constraints, and behavior of Agent IDs and Topic IDs.

## Agent ID

### Required Attributes

#### type

- Type: `string`
- Description: The agent type is not an agent class. It associates an agent with a specific factory function, which produces instances of agents of the same agent `type`. For example, different factory functions can produce the same agent class but with different constructor perameters.
- Constraints: UTF8 and only contain alphanumeric letters (a-z) and (0-9), or underscores (\_). A valid identifier cannot start with a number, or contain any spaces.
- Examples:
  - `code_reviewer`
  - `WebSurfer`
  - `UserProxy`

#### key

- Type: `string`
- Description: The agent key is an instance identifier for the given agent `type`
- Constraints: UTF8 and only contain characters between (inclusive) ascii 32 (space) and 126 (~).
- Examples:
  - `default`
  - A memory address
  - a UUID string

## Topic ID

### Required Attributes

#### type

- Type: `string`
- Description: Topic type is usually defined by application code to mark the type of messages the topic is for.
- Constraints: UTF8 and only contain alphanumeric letters (a-z) and (0-9), ':', '=', or underscores (\_). A valid identifier cannot start with a number, or contain any spaces.
- Examples:
  - `GitHub_Issues`

#### source

- Type: `string`
- Description: Topic source is the unique identifier for a topic within a topic type. It is typically defined by application data.
- Constraints: UTF8 and only contain characters between (inclusive) ascii 32 (space) and 126 (~).
- Examples:
  - `github.com/{repo_name}/issues/{issue_number}`