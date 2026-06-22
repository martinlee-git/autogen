# 읽어보기

- 원문 저장소: `microsoft/autogen`
- 미러 저장소: `martinlee-git/autogen`
- 원문 문서: https://github.com/microsoft/autogen/blob/main/python/packages/agbench/benchmarks/HumanEval/README.md
- 미러 경로: `python/packages/agbench/benchmarks/HumanEval/README.md`

## 한글 요약

HumanEval 벤치마크 이 시나리오는 HumanEval 벤치마크의 수정된 버전을 구현합니다. 원래 벤치마크와 비교할 때 여기에는 두 가지 주요 차이점이 있습니다. 완료 모델이 아닌 채팅 모델이 사용됩니다. 에이전트는 구현에 대한 통과/실패 피드백을 받고 성공하거나 토큰 또는 턴이 부족할 때까지 계속 시도할 수 있습니다. 작업 실행 HumanEval 업데이트 config.yaml로 이동하여 적절하게 모델 호스트를 가리킵니다. 기본 구성은 'gpt 4o'를 가리킵니다. 이제 작업을 초기화합니다. 참고: HumanEval 다운로드를 시도한 다음 Scripts/init task.py를 다시 실행합니다. 스크립트가 완료되면 이제 템플릿의 템플릿당 하나의 JSONL 파일이 포함된 Tasks라는 폴더가 현재 디렉터리에 표시됩니다. 이제 HumanEval 사용의 특정 하위 집합을 실행하려면: 명령줄에서 에이전트의 작업을 보여주는 원시 로그를 인쇄해야 합니다. 결과 요약(예: 작업 완료율)을 보려면 새 터미널에서 다음을 실행하세요.

## 핵심 발췌

코드에서 훈련된 대규모 언어 모델 평가 <br/ Mark Chen, Jerry Tworek, Heewoo Jun, Qiming Yuan, Henrique Ponde de Oliveira Pinto, Jared Kaplan, Harri Edwards, Yuri Burda, Nicholas Joseph, Greg Brockman, Alex Ray, Raul Puri, Gretchen Krueger, Michael Petrov, Heidy Khlaaf, Girish Sastry, Pamela Mishkin, Brooke Chan, Scott 그레이, 닉 라이더, 미하일 파블로프, 알레시아 파워, 루카스 카이저, 모하마드 바바리안, 클레멘스 윈터, 필립 틸레, 펠리페 페트로스키 수, 데이브 커밍스, 마티아스 플래퍼트, 포티오스 챈치스, 엘리자베스 반스, 아리엘 허버트 보스, 윌리엄 헵겐 거스, 알렉스 니콜, 알렉스 파이노, 니콜라스 테작, 지에 탕, 이고르 바부쉬킨, 수치르 발라지, 샨타누 자인, 윌리엄 손더스, 크리스토퍼 헤세, 앤드류 N. 카, 얀 레이케, 조쉬 아치암, 베던트 미스라, 에반 모리카와, 알렉 래드포드, 매트

## 원문 내용

# HumanEval Benchmark

This scenario implements a modified version of the [HumanEval](https://arxiv.org/abs/2107.03374) benchmark.
Compared to the original benchmark, there are **two key differences** here:

- A chat model rather than a completion model is used.
- The agents get pass/fail feedback about their implementations, and can keep trying until they succeed or run out of tokens or turns.

## Running the tasks


Navigate to HumanEval

```bash
cd benchmarks/HumanEval
```

Update `config.yaml` to point to your model host, as appropriate. The default configuration points to 'gpt-4o'.


Now initialize the tasks.

```bash
python Scripts/init_tasks.py
```

Note: This will attempt to download HumanEval

Then run `Scripts/init_tasks.py` again.

Once the script completes, you should now see a folder in your current directory called `Tasks` that contains one JSONL file per template in `Templates`.

Now to run a specific subset of HumanEval use:

```bash
agbench run Tasks/human_eval_AgentChat.jsonl
```

You should see the command line print the raw logs that shows the agents in action To see a summary of the results (e.g., task completion rates), in a new terminal run the following:

```bash
agbench tabulate Results/human_eval_AgentChat
```


## References

**Evaluating Large Language Models Trained on Code**`<br/>`
Mark Chen, Jerry Tworek, Heewoo Jun, Qiming Yuan, Henrique Ponde de Oliveira Pinto, Jared Kaplan, Harri Edwards, Yuri Burda, Nicholas Joseph, Greg Brockman, Alex Ray, Raul Puri, Gretchen Krueger, Michael Petrov, Heidy Khlaaf, Girish Sastry, Pamela Mishkin, Brooke Chan, Scott Gray, Nick Ryder, Mikhail Pavlov, Alethea Power, Lukasz Kaiser, Mohammad Bavarian, Clemens Winter, Philippe Tillet, Felipe Petroski Such, Dave Cummings, Matthias Plappert, Fotios Chantzis, Elizabeth Barnes, Ariel Herbert-Voss, William Hebgen Guss, Alex Nichol, Alex Paino, Nikolas Tezak, Jie Tang, Igor Babuschkin, Suchir Balaji, Shantanu Jain, William Saunders, Christopher Hesse, Andrew N. Carr, Jan Leike, Josh Achiam, Vedant Misra, Evan Morikawa, Alec Radford, Matthew Knight, Miles Brundage, Mira Murati, Katie Mayer, Peter Welinder, Bob McGrew, Dario Amodei, Sam McCandlish, Ilya Sutskever, Wojciech Zaremba`<br/>`
[https://arxiv.org/abs/2107.03374](https://arxiv.org/abs/2107.03374)