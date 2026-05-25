# 읽어보기

- 원문 저장소: `microsoft/autogen`
- 미러 저장소: `martinlee-git/autogen`
- 원문 문서: https://github.com/microsoft/autogen/blob/main/python/docs/README.md
- 미러 경로: `python/docs/README.md`

## 한글 요약

AutoGen 문서 작성 AutoGen 문서는 스핑크스 문서 시스템을 기반으로 하며 myst 파서를 사용하여 마크다운 파일을 렌더링합니다. pydata 스핑크스 테마를 사용하여 문서 스타일을 지정합니다. 전제 조건 Autogen Core 패키지에 대한 모든 개발 종속성이 설치되어 있는지 확인하십시오. Python 리포지토리 루트에서 다음 명령을 실행하여 설치할 수 있습니다. Docs 빌드 문서를 빌드하려면 python 디렉터리 루트에서 다음 명령을 실행합니다. 문서를 로컬로 제공하려면 python 디렉터리 루트에서 다음 명령을 실행합니다. Sphinx는 마지막 빌드 이후 변경된 파일만 다시 빌드합니다. 전체 재빌드를 강제로 수행하려면 docs build 명령을 실행하기 전에 ./docs/build 디렉터리를 삭제하면 됩니다.

## 핵심 발췌

AutoGen 문서 작성 AutoGen 문서는 스핑크스 문서 시스템을 기반으로 하며 myst 파서를 사용하여 마크다운 파일을 렌더링합니다. [pydata 스핑크스 테마](https://pydata sphinx theme.re)를 사용합니다.

## 원문 내용

## Building the AutoGen Documentation

AutoGen documentation is based on the sphinx documentation system and uses the myst-parser to render markdown files. It uses the [pydata-sphinx-theme](https://pydata-sphinx-theme.readthedocs.io/en/latest/) to style the documentation.

### Prerequisites

Ensure you have all of the dev dependencies for the `autogen-core` package installed. You can install them by running the following command from the root of the python repository:

```bash
uv sync
source .venv/bin/activate
```

## Building Docs

To build the documentation, run the following command from the root of the python directory:

```bash
poe docs-build
```

To serve the documentation locally, run the following command from the root of the python directory:

```bash
poe docs-serve
```

[!NOTE]
Sphinx will only rebuild files that have changed since the last build. If you want to force a full rebuild, you can delete the `./docs/build` directory before running the `docs-build` command.