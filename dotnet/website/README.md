# 읽어보기

- 원문 저장소: `microsoft/autogen`
- 미러 저장소: `martinlee-git/autogen`
- 원문 문서: https://github.com/microsoft/autogen/blob/main/dotnet/website/README.md
- 미러 경로: `dotnet/website/README.md`

## 한글 요약

웹 사이트를 빌드하고 실행하는 방법 전제 조건 dotnet 7.0 이상 빌드 먼저 autogen/dotnet 폴더로 이동하고 다음 명령을 실행하여 웹 사이트를 빌드합니다. 명령이 실행된 후 브라우저를 열고 http://localhost:8080으로 이동하여 웹 사이트를 볼 수 있습니다.

## 핵심 발췌

웹 사이트 빌드 및 실행 방법 ### 전제 조건 dotnet 7.0 이상 ### 빌드 먼저 autogen/dotnet 폴더로 이동하여 다음 명령을 실행하여 웹 사이트를 빌드합니다. ```bash dotnet tool Restore dotnet tool run

## 원문 내용

## How to build and run the website

### Prerequisites
- dotnet 7.0 or later

### Build
Firstly, go to autogen/dotnet folder and run the following command to build the website:
```bash
dotnet tool restore
dotnet tool run docfx website/docfx.json --serve
```

After the command is executed, you can open your browser and navigate to `http://localhost:8080` to view the website.