## [LLM Visualization](https://bbycroft.net/llm) 을 한글로 번역하고 요약했습니다.

### Introduction
트랜스포머 모델에서의 입력 처리는 주로 토큰 매핑과 임베딩의 두 주요 단계로 구성됩니다. 이 과정은 자연어 텍스트를 모델이 처리할 수 있는 숫자 형태로 변환하는 데 필수적입니다.

### Embedding
토큰 매핑: 입력 텍스트는 먼저 개별 토큰으로 분리됩니다. 
각 토큰은 사전에 정의된 어휘 목록에 따라 고유한 정수 인덱스로 매핑됩니다. 이 매핑은 각 토큰을 모델 내에서 구별 가능하고 처리 가능한 유일한 식별자로 변환하는 역할을 합니다.

토큰 임베딩: 매핑된 인덱스를 사용하여 토큰 임베딩 매트릭스에서 해당 인덱스에 위치한 고차원 벡터를 추출합니다. 
이 벡터는 해당 토큰의 의미적 특성을 나타내며, 모델이 이해할 수 있는 형태로 정보를 제공합니다.

위치 임베딩: 각 토큰의 위치에 따라 위치 임베딩 벡터가 추가됩니다. 이는 토큰의 문장 내 위치 정보를 모델에 제공하며, 순서 정보가 문장의 의미 해석에 중요하기 때문에 필수적입니다.

벡터의 합성: 최종적으로, 토큰 임베딩과 위치 임베딩은 합쳐져 각 토큰의 최종 임베딩 벡터를 형성합니다. 
이 벡터는 토큰의 의미적 정보와 위치 정보를 모두 포함합니다.

### Layer Norm
이렇게 변환된 입력 벡터들은 트랜스포머 모델의 다음 단계인 자기 주의 계층으로 전달되어 복잡한 언어 처리 작업을 위한 기반을 마련합니다. 
이 과정은 트랜스포머가 텍스트를 숫자 데이터로 변환하고, 문장의 의미와 구조를 이해하는 데 중요한 첫 걸음입니다 

### Self Attention
다음은 트랜스포머 모델의 Self-attention계층은 입력 데이터의 모든 부분 간의 관계를 병렬적으로 처리하여 문맥적 이해를 깊게 합니다. 
Self-attention은 입력 시퀀스 내 각 토큰 간의 상호 의존성과 관계를 분석하여 문맥적인 정보를 추출합니다. 토큰의 중요도를 평가하여 문장 전체의 의미를 구성하는 데 필요한 특정 정보를 강조합니다. 
작동원리는 아래와 같습니다. 

Q, K, V 벡터 생성: 각 입력 토큰에 대해 쿼리(Query), 키(Key), 값(Value) 벡터가 생성됩니다. 이 벡터들은 입력 데이터를 다양한 방식으로 표현합니다.

점곱과 유사성 측정: 쿼리 벡터와 모든 키 벡터간의 점곱을 계산하여 유사성 점수를 생성합니다.

소프트맥스 정규화: 유사성 점수에 소프트맥스를 적용하여, 각 키-값 쌍의 중요도를 확률적으로 조정합니다.

출력 벡터 계산: 정규화된 점수를 사용하여 각 값 벡터를 가중합하여 최종 출력 벡터를 생성합니다.

### Projection
Self-attention 메커니즘을 통해 모델은 입력 시퀀스의 각 부분이 전체에 어떻게 기여하는지를 평가하고, 이를 바탕으로 보다 정확하고 문맥에 맞는 출력을 생성할 수 있습니다 
데이터는 여러 후속 처리 단계를 거쳐 최종적으로 다음 층으로 전달됩니다.

### MLP, Transformer
Self-attention 계층 후의 처리 과정과 Multi-head Self-attention에서 생성된 여러 head의 출력이 조합되어 통합된 출력 벡터를 형성합니다.
그 후 통합된 출력 벡터는 선형 변환을 통해 원래의 입력 차원으로 투영되며, 필요한 경우 편향이 추가됩니다. 
그리고 Self-attention계층의 출력에 원래 입력 임베딩을 더하여, 잔차 연결을 통해 정보의 흐름을 개선하고 깊은 네트워크에서 학습을 안정화합니다. 
잔차 연결 후 출력에 계층 정규화를 적용하여, 각 입력의 평균과 표준 편차를 조정합니다. 
처리된 데이터는 피드 포워드 네트워크(FFN)로 전달되어 추가적인 비선형 변환을 수행합니다.
이 후속 처리 과정을 통해 트랜스포머는 각 단계에서 생성된 정보를 효과적으로 통합하고, 깊은 네트워크 구조에서도 안정적으로 학습할 수 있습니다.

Transformer 모델 내의 피드 포워드 네트워크 (FFN)는 입력 데이터에 대해 두 개의 선형 변환과 하나의 활성화 함수를 독립적으로 적용하는 구조로, 모델이 복잡한 패턴을 학습할 수 있도록 비선형성을 추가합니다. 
주요 과정은 다음과 같습니다:

입력 벡터의 차원을 확장하여 더 많은 정보를 포착할 수 있는 용량을 확보합니다. 
다음으로는 GELU 함수를 적용해 필요한 비선형성을 제공하며, 더 복잡한 데이터 패턴을 처리합니다. 
다음 차원으로 확장된 벡터를 원래 차원으로 축소하여, 다음 계층이나 최종 출력에 적합한 형태로 만듭니다. 
마지막으로 FFN의 출력에 원래 입력을 더해 잔차 연결을 형성하고, 계층 정규화를 통해 입력 벡터의 평균과 표준 편차를 조정합니다.

이 과정을 통해 FFN은 트랜스포머 아키텍처에서 중요한 역할을 하며, 각 입력에 대해 독립적으로 작동하여 모델의 전체적인 성능과 학습 안정성을 향상시킵니다.

### Softmax
Transformer 모델의 마지막 단계에서는 최종 트랜스포머 블록의 출력을 처리하여 사용자가 해석할 수 있는 결과를 생성합니다. 
마지막 블록의 출력을 정규화하여 학습과 수렴을 안정화합니다. 
선형 변환 및 로짓 생성을 위해정규화된 출력을 어휘 사전 크기에 맞는 차원으로 매핑하고, 각 차원의 값을 로짓으로 변환하여 다음 토큰 선택의 로그 확률을 제공합니다. 
그 다음 로짓을 소프트맥스 함수로 확률로 변환하여, 각 토큰의 선택 확률을 계산합니다. 
계산된 결과로 확률 분포에 따라 다음 토큰을 선택하고, 이 과정을 반복하여 새로운 문장이나 문서를 생성합니다. 

### Output
다음으로 temperature 변수로 출력 분포의 부드러움을 조절하여, 다양한 출력을 산출하거나 특정 출력을 강조합니다.
이러한 단계를 통해 트랜스포머 모델은 복잡한 입력 데이터를 처리하고, 자연어 처리 작업에 적합한 결과를 생성합니다.
이렇듯 대규모 언어 모델의 작동 원리는 복잡하지만, 그 핵심은 방대한 양의 텍스트 데이터로부터 언어의 패턴과 구조를 학습하여, 이를 기반으로 새로운 텍스트를 생성하거나, 주어진 텍스트의 의미를 이해하는 것입니다. 
Transformer 아키텍처와 Self-attention메커니즘을 통해, 이 모델들은 문맥을 고려한 언어 이해와 생성을 가능하게 하며, 파인 튜닝을 통해 다양한 작업과 도메인에 적용될 수 있습니다.
