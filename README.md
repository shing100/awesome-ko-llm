# awesome ko llm
한국어로된 llm 정보 모음

## 학습
- Microsft 에서 제공 : [generative-ai-for-beginners](https://github.com/microsoft/generative-ai-for-beginners)
- 한국어 랭체인 듀토리얼 langchain-kr : [langchain-kr](https://github.com/teddylee777/langchain-kr)
- Large Language Model Course : [llm-course](https://github.com/mlabonne/llm-course)

## 실제 모델 학습, 실행 관련
- [axolotl](https://github.com/OpenAccess-AI-Collective/axolotl)
- [text-generation-webui](https://github.com/oobabooga/text-generation-webui)
- [mergekit](https://github.com/arcee-ai/mergekit)
- [open-webui](https://github.com/open-webui/open-webui)

# llm-evaluation 
레포트 작성할때 정리한 데이터 및 평가 데이터


### HellaSwag 영문 한글 결과
| ChatGPT4 | ChatGPT3,5 | Gemma-7b-it | Mixtral-8x7B-Instruct-v0.1 | openchat-3.5-0106 | Nous-Hermes-2-Mixtral-8x7B-DPO | Solar-Mini | qwen:14B |
|----------|------------|-------------|----------------------------|-------------------|--------------------------------|------------|----------|
| 9/10     | 8/10       | 5/10        | 6/10                       | 8/10              | 8/10                           | 7/10       | 7/10     |  - 영문
| 9(10)/10 | 6/10       | 3/10        | 6/10                       | 2/10              | 3/10                           | 7(8)/10    | 6/10     |  - 한글
| 한글답변  | 한글답변    |멀티턴 이해 불가 | 영어로답변 | 한글답변    | 한글답변           | 한글답변                       | 한글답변    | 한글답변  |

## 리서치

### 대규모 언어 모델 평가 방법

대규모 언어 모델(LLM)의 평가에 대한 광범위한 관점을 제공하고자 합니다. 

LLM는 다양한 작업에서 뛰어난 능력을 보여주며 많은 주목을 받고 있지만, 개인 데이터 유출, 부적절하거나 해로운 콘텐츠 생성, 그리고 충분한 안전장치 없이 초지능 시스템이 등장할 수 있다는 우려도 있습니다. 

LLM의 잠재력을 효과적으로 활용하고 안전하고 유익한 발전을 보장하기 위해, LLM의 철저하고 포괄적인 평가가 필수적입니다. 위에서 소개한 평가지표에 주로 소개되는 MMLU, Big-Bench, HellaSwag, HumanEval, Boolq 등 다양한 평가 방법이 이에 해당합니다. 

리서치 도중 찾은 Evaluating Large Language Models: A Comprehensive Survey에서는 LLM 평가를 Knowledge and Capability Evaluation, Alignment Evaluation, Safety Evaluation, Specialized LLMs Evaluation, Evaluation Organization 로 분류합니다.

### 한국(ko-llm)에서는 다음의 데이터셋을 사용하여 한국어 LLM 모델의 성능을 평가하고 있습니다.
### 평가 데이터셋
- Ko-ARC
- Ko-HellaSwag  
- Ko-MMLU
- Ko-TruthfulQA
- Ko-CommonGen V2

## 평가 도구

모델 평가를 쉽게 할 수 있도록 도와주는 툴로는 다음과 같은 것들이 있습니다.

- [lm-evaluation-harness](https://github.com/EleutherAI/lm-evaluation-harness) (한국어 평가 지원)
- [ko-lm-evaluation-harness](https://github.com/Beomi/ko-lm-evaluation-harness)
- [llm-kr-eval](https://github.com/wandb/llm-kr-eval)
- [LogicKor](https://github.com/StableFluffy/LogicKor)

이들 툴을 사용하면 간단한 명령어로 모델들을 평가할 수 있습니다.

## VRAM 요구사항

모델의 파라메터 수에 따른 VRAM 요구사항은 다음과 같습니다.
> [cant-it-run-llm](https://huggingface.co/spaces/Vokturz/can-it-run-llm)

| 파라메터 수 | FP16 | INT8 (양자화) | INT4 (양자화) |
|-------------|------|----------------|----------------|
| 7B          | 14GB | 7GB            | 4GB            |
| 13B         | 27GB | 14GB           | 7GB            |
| 33B         | 68GB | 34GB           | 17GB           |
| 65B         | 135GB| 68GB           | 34GB           |

## GPU 가격

2024년 3월 27일 기준으로 A100 (80GB) 그래픽카드 가격은 대략 3천만원 수준입니다. A100 80G 1장으로는 65B개의 파라메터를 가진 INT8 (양자화) 모델까지 추론이 가능합니다.

## 모델 크기와 성능

일반적으로 모델의 크기가 커질수록 성능이 향상되는 경향이 있지만, 더 큰 모델이 항상 더 나은 성능을 보장하지는 않습니다. 고품질 데이터로 파인 튜닝된 작은 모델도 경쟁력 있는 성능을 낼 수 있습니다.

또한, 명시적인 지시(instruction tuning)가 모델의 성능 향상에 중요한 역할을 합니다. 이를 통해 모델이 특정 태스크의 뉘앙스를 더 잘 이해할 수 있게 됩니다.
