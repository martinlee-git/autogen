# 읽어보기

- 원문 저장소: `microsoft/autogen`
- 미러 저장소: `martinlee-git/autogen`
- 원문 문서: https://github.com/microsoft/autogen/blob/main/python/packages/agbench/benchmarks/README.md
- 미러 경로: `python/packages/agbench/benchmarks/README.md`

## 한글 요약

에이전트 벤치마킹 이 디렉토리는 AgBench를 사용하여 에이전트(예: Autogen을 사용하여 구축)를 벤치마킹하는 기능을 제공합니다. 아래 지침을 사용하여 벤치마킹을 위한 환경을 준비하세요. 완료되면 관련 벤치마크 디렉터리(예: 벤치마크/GAIA)로 이동하여 추가 시나리오별 지침을 확인하세요. WSL에서 설정 1. Docker Desktop을 설치합니다. 설치 후 다시 시작해야 하며 설정, 리소스, WSL 통합에서 Docker Desktop을 열고 추가 배포판과 통합 활성화 – Ubuntu 2. 자동 생성을 복제하고 AUTOGEN REPO BASE를 내보냅니다. 이 환경 변수를 사용하면 Docker 컨테이너가 올바른 버전 에이전트를 사용할 수 있습니다. 3. 어그벤치를 설치합니다. AgBench는 현재 Autogen 저장소의 도구입니다.

## 핵심 발췌

에이전트 벤치마킹 이 디렉토리는 AgBench를 사용하여 에이전트(예: Autogen을 사용하여 구축)를 벤치마킹하는 기능을 제공합니다. 아래 지침을 사용하여 벤치마킹을 위한 환경을 준비하세요. 완료되면 relev로 진행하세요.

## 원문 내용

# Benchmarking Agents

This directory provides ability to benchmarks agents (e.g., built using Autogen) using AgBench. Use the instructions below to prepare your environment for benchmarking. Once done, proceed to relevant benchmarks directory (e.g., `benchmarks/GAIA`) for further scenario-specific instructions.

## Setup on WSL

1. Install Docker Desktop. After installation, restart is needed, then open Docker Desktop, in Settings, Ressources, WSL Integration, Enable integration with additional distros – Ubuntu
2. Clone autogen and export `AUTOGEN_REPO_BASE`. This environment variable enables the Docker containers to use the correct version agents.
    ```bash
    git clone git@github.com:microsoft/autogen.git
    export AUTOGEN_REPO_BASE=<path_to_autogen>
    ```
3. Install `agbench`. AgBench is currently a tool in the Autogen repo.

    ```bash
    cd autogen/python/packages/agbench
    pip install -e .
    ```