# 읽어보기

- 원문 저장소: `microsoft/autogen`
- 미러 저장소: `martinlee-git/autogen`
- 원문 문서: https://github.com/microsoft/autogen/blob/main/python/packages/agbench/benchmarks/GAIA/README.md
- 미러 경로: `python/packages/agbench/benchmarks/GAIA/README.md`

## 한글 요약

GAIA 벤치마크 이 시나리오는 GAIA 에이전트 벤치마크를 구현합니다. 시작하기 전에 ../README.md의 지침에 따라 환경을 준비했는지 확인하세요. AgBench용 환경 변수 설정 GAIA 업데이트 config.yaml로 이동하여 적절하게 모델 호스트를 가리킵니다. 기본 구성은 'gpt 4o'를 가리킵니다. 이제 작업을 초기화합니다. 참고: Hugginface에서 GAIA 다운로드를 시도하지만 인증이 필요합니다. 결과 폴더 구조는 다음과 같아야 합니다. 그런 다음 Scripts/init task.py를 다시 실행합니다. 스크립트가 완료되면 이제 템플릿의 템플릿당 하나의 JSONL 파일이 포함된 Tasks라는 폴더가 현재 디렉터리에 표시됩니다. GAIA 실행 이제 GAIA 사용의 특정 하위 집합을 실행하려면: 명령줄에서 에이전트의 작동을 보여주는 원시 로그를 인쇄해야 합니다. 결과 요약(예: 작업 완료율)을 보려면 새 터미널에서 다음을 실행하세요. 참조 GAIA: 일반 AI 보조자에 대한 벤치마크 <br/ Grégoi

## 핵심 발췌

다시 Mialon, Clémentine Fourrier, Craig Swift, Thomas Wolf, Yann LeCun, Thomas Scialom <br/ https://arxiv.org/abs/2311.12983

## 원문 내용

# GAIA Benchmark

This scenario implements the [GAIA](https://arxiv.org/abs/2311.12983) agent benchmark. Before you begin, make sure you have followed instruction in `../README.md` to prepare your environment.

### Setup Environment Variables for AgBench

Navigate to GAIA

```bash
cd benchmarks/GAIA
```

Update `config.yaml` to point to your model host, as appropriate. The default configuration points to 'gpt-4o'.

Now initialize the tasks.

```bash
python Scripts/init_tasks.py
```

Note: This will attempt to download GAIA from Hugginface, but this requires authentication.

The resulting folder structure should look like this:

```
.
./Downloads
./Downloads/GAIA
./Downloads/GAIA/2023
./Downloads/GAIA/2023/test
./Downloads/GAIA/2023/validation
./Scripts
./Templates
./Templates/TeamOne
```

Then run `Scripts/init_tasks.py` again.

Once the script completes, you should now see a folder in your current directory called `Tasks` that contains one JSONL file per template in `Templates`.

### Running GAIA

Now to run a specific subset of GAIA use:

```bash
agbench run Tasks/gaia_validation_level_1__MagenticOne.jsonl
```

You should see the command line print the raw logs that shows the agents in action To see a summary of the results (e.g., task completion rates), in a new terminal run the following:

```bash
agbench tabulate Results/gaia_validation_level_1__MagenticOne/
```

## References

**GAIA: a benchmark for General AI Assistants** `<br/>`
Grégoire Mialon, Clémentine Fourrier, Craig Swift, Thomas Wolf, Yann LeCun, Thomas Scialom `<br/>`
[https://arxiv.org/abs/2311.12983](https://arxiv.org/abs/2311.12983)