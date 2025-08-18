# 01. INTRODECTION

<img width="688" height="194" alt="image" src="https://github.com/user-attachments/assets/a3a469d6-2e6c-4e77-9acb-0a3eb24f63c0" />

## 1. 자연어 (Natural Language)
- 일상생활에서 사용하는 보편적인 언어

## 2. 자연어처리 (Natural Language Processing)
- 컴퓨터가 자연어를 처리하는 일
- 구성요소
  1. NLU : 컴퓨터가 인간 언어를 이해하는 과정
  2. NLG : 컴퓨터가 인간 언어를 생성하는 과정

  ## 3. NLP의 주요 구성 요소
  - Tokenization : 문장을 단어/토큰 단위로 분리
  - Part-of-Speech Tagging : 품사 태깅
  - Entities : 개체명 인식 ( 사람, 장소, 조직 등)
  - Contextual Understanding : 문맥의 이해
  - Utterances : 발화 단위 분석
  - Sentiment Analysis : 감정 분석
  - Intents : 의도 파악
  - Dialogue Manager : 대화 흐름 관리
  - Machine Learning : 기계학습 기반 처리
 
  # 02. Text Preprocessing
  - 자연어 처리를 하기전에 텍스트 데이터를 분석 가능한 형태로 만들기 위한 전처리 과정

 ## 1. 토큰화 (Tokenization)
  - 문장을 의미있는 최소 단위로 분리함
  - 예시
    - 입력 : "자연어 처리는 재미있다."
    - 출력 : ["자연어", "처리", "는", "재미있다"]

 ## 2. 정제 (Cleaning)
- 불필요한 문자나 기호를 제거하여 데이터 품질을 높이는 과정
- 제거대상
  - 특수문자
  - HTML 태그
  - 공백
  - 잡음 데이터

  ## 3. 정규화 (Normalization)
  - 같은 의미를 가진 다양한 표현을 통일된 형태로 변환
  - 예시
    - 대소문자 변환
    - 숫자 단위 표기
    - 띄어쓰기 수정

  ## 4. 불용어 제거
  - 의미 전달에 기여도가 낮은 단어 -> 조사, 접속사, 빈도높은 관용적 단어 등
  - 예시 : "나는 오늘 학교에 간다" → ["오늘", "학교", "간다"]

  ## 5. 어간/표제어 추출
  - 단어의 다양한 활용형을 기본형으로 변환하여 의미를 통일함
  - 비교
    - Stemming : 단순히 어간을 자르는 방식 (`studies → studi`)
    - Lemmatization : 문맥과 품사를 고려한 변환 (`studies → study`)

# 03. N-gram

## 1. N-gram 모델
- 문장 소게서 연속된 N개의 단어 시퀀스를 보고, 다음 단어가 나올 확률
- Chain Rule : 단어 시퀀스의 확률을 조건부 확률 곱으로 표현

    
예시: `"I like pizza"`  
<img width="505" height="121" alt="image" src="https://github.com/user-attachments/assets/083ab6a3-ffad-4eee-9909-a1bf8f927213" />


## 2. Markov Assumptioin (마르코프 가정)
- 다음 단어는 전체 과거 시퀀스가 아니라, 최근 n-1개의 단어에만 의존한다고 가정
<img width="287" height="35" alt="image" src="https://github.com/user-attachments/assets/c546a99f-06eb-4756-9575-5705671285b1" />


## 3. Bigram & N-gram 확률
### Bigram (2-gram) 가정
<img width="436" height="96" alt="image" src="https://github.com/user-attachments/assets/521c6809-e142-45e1-9642-d7fdd264263d" />


### 일반 N-gram 가정
<img width="301" height="48" alt="image" src="https://github.com/user-attachments/assets/6390bc5f-0a06-4312-b416-b98b3ab79beb" />


## 4. 확률 계산 (MLE)
- N-grma확률은 빈도수 기반으로 추정
<img width="206" height="107" alt="image" src="https://github.com/user-attachments/assets/0625fe0a-8092-4fc6-b0b0-9c4750a5cd07" />

## 5. 예시 (Bingram)
<img width="601" height="194" alt="image" src="https://github.com/user-attachments/assets/b1c7776c-9a31-4c90-8e59-b8ff346b659f" />


# 04. Word Embedding

## 1. Word Embedding
- 단어의 의미를 벡터 공간에서의 위치로 정의
- 의미가 비슷한 단어일수록 벡터 공간에서 가깝게 위치함

## 2. Word Embedding 종류
### Static Embedding (정적 임베딩)
- 단어마다 고정된 벡터를 사용
- 대표 기법
  - Word2Vec
  - GloVe

### Contextual Embedding (문맥 임베딩)
- 문맥에 따라서 단어 벡터가 달라짐
- 대표기법
  - ELMo
  - BERT
  - GPT 시리즈

## 3. Word2Vec
### 1) CBOW 
<img width="462" height="323" alt="image" src="https://github.com/user-attachments/assets/a4c53cb1-fc79-4cbc-927e-930465e634ca" />

- 주변 단어로부터 중심단어를 예측하는 방식
<img width="646" height="372" alt="image" src="https://github.com/user-attachments/assets/ea123d5e-ad3c-4578-968b-ceafe874b35d" />

- 예시 문장:  
`The fat cat sat on the mat`

- 중심 단어: `sat`  
- 주변 단어: `fat`, `cat`, `on`, `the`  

### 2) 핵심 개념
- Window : 중심단어 주변에서 context words를 잡기위한 범위
- sliding Window : 문장을 처음부터 끝까지 훑으면서, window를 한 단어씩 이동시켜서 context-target 쌍을 생성

## 4. GloVe
### 1) Word2Vec과의 차이
- Word2Vec : 지역적 윈도우 내에서 예측 학습
- GloVe : 전역적 동계 (코퍼스 전체의 단어 쌍 동시 등장 확률)을 활용함

### 2) 동시 등장 확률 (Co-occurrence Probability)
- 특정 단어 i와 전체 단어 k의 동시 등장 횟수를 카운트
- 특정 단어 i가 등장했을 때 어떤 단어 k가 함께 등장할 확률 (조건부 확률)을 계산함
<img width="275" height="113" alt="image" src="https://github.com/user-attachments/assets/8635628c-190b-40dc-aba9-ad212cb50ce8" />

### 3) 손실 함수 (Loss Function)
- 단어 벡터 학습은 동시 등장 행렬을 기반으로 최적화함
<img width="266" height="51" alt="image" src="https://github.com/user-attachments/assets/61bc36e2-19c3-45bf-a558-6237fdbbf3bc" />


# 05. Sequence Models
## 1. RNN (Recurrent Neural Network, 순환 신경망)
- 현재 시점의 입력값과 이전 시점의 hidden state (은닉 상태)를 연산해 새로운 hidden state를 생성하는 구조
- 연속적 데이터 처리에 적합 (텍스트, 음성)

### 핵심 개념
<img width="568" height="134" alt="image" src="https://github.com/user-attachments/assets/57974ab8-15fb-451a-bc93-c93a5d30ac25" />

### 동작 과정
<img width="331" height="138" alt="image" src="https://github.com/user-attachments/assets/5851ecf5-4d45-4faa-89bb-7db8f91749f1" />

1. 이전 시점의 hidden state와 현재 입력을 기반으로 현재 hidden state 계산
2. 현재 hidden state로 출력값 계산
3. 이를 반복해서 시퀀스 전체 처리

- 각 시점마다 동일한 가중치를 사용함 (parameter 공유)
- 초기 hidden state는 보통 0또는 랜덤 값으로 설정

### 기존 RNN의 문제점
<img width="585" height="148" alt="image" src="https://github.com/user-attachments/assets/df9b3190-aaae-4a71-97ca-f79b25fcffe7" />

1. Long-term dependency 문제
   - 장기 기억이 필요할 경우 Gradient vanishing (기울기 소실) 발생
   - 역전파 과정에서 gradient가 점차 작아져서 학습이 어려워짐
  
> 기울기 소실문제
- 신경망학습은 역전파로 기울기를 전달해 가중치를 업데이트함
- 하지만 RNN처럼 깊은 구족에서는 작은 값이 계쏙 곱해지면서 기울기가 점점 0에 가까워진다
- 그 결과 오래전 입력에 대한 영향력이 거의 사라져 학습이 되지 않는다 -> 장기 의존성을 학습하기가 어렵게 만든다
  
2. 순차적 처리 문제 (Unparallelizable)
   - 입력을 순차적으로 처리해야함
   - 병렬화가 불가능해서 학습 속도가 저하됨

## 2. LSTM
<img width="365" height="170" alt="image" src="https://github.com/user-attachments/assets/094c82aa-0b5f-44c7-af0f-21e1b585da82" />

- RNN의 단점을 보완하기 위해서 등장
- 장점 : 기울기 소실 문제를 완화시켜서 장기 의존성 문제를 해결한다.
- 내부 구조 :  Cell state + 게이트 구조 (Input gate, Forget gate, Output gate)로 정보 흐름을 제어  ]

## 3. GRU 
<img width="470" height="146" alt="image" src="https://github.com/user-attachments/assets/147c6a2c-028a-441c-b19c-f89004786cb9" />

- LSTM의 단순화 버전 ( 학습 속도 증가, 계산 효율 증가, 파라미터 감소)
- 구성요소 : 2개의 Gate
- 차이점 : 별도의 Cell state 없이 hidden state만 사용함

## 4. seq2seq
- sequence 입력을 받아서 sequence를 출력하는 RNN 기반 end-to-end 모델
- 변역, 요약 등 주어진 텍스트를 바탕으로 새로운 텍스트를 생성하는데에 적합함
- 흐름 : 입력 시퀀스 -인코더 - 컨텍스트 벡터 - 디코더 - 출력 시퀀스
<img width="831" height="210" alt="image" src="https://github.com/user-attachments/assets/1eef70c0-d06c-4029-9d4a-4357dae7e921" />

### 한계점
1. 정보 압축 손실
   - 하나의 고정된 벡터에 전체 입력 시퀀스를 압축 - 긴 문장에서 정보 손실 발생
2. Gradient Vnishing 문제
   - RNN 기반 구조이므로 여전히 장기 의존성 문제 존재
   - LSTM / GRU 로 완호 가능하지만 완전히 해결 불가

# 06. Attention
- seq2seq 정보 손실 문제를 해결하기 위해서 도입된 매커니즘
- 디코더가 출력 단어를 예측할 때, 인코더의 모든 hidden state 중 중요한 부분에 더 집중

> 인코더
- 입력 시쿠너스를 읽고 의미를 압축된 벡터 표현으로 변환 = 입력을 이해하는 부분

> 디코더
- 인코더가 만든 context vector를 바탕으로 출력 시퀀스를 생성함 = 출력을 생성하는 부분

## 1. 동작 과정 (Dot-Prodect Attention 기준)
### 1) 유사도 계산 (Attention Score)
<img width="305" height="151" alt="image" src="https://github.com/user-attachments/assets/a36f7543-d1d3-4772-b2a0-e3718b15597b" />

- 현재 시점 디코더 hidden state와 모든 인코더 hidden state간 내적 수행

### 2) 확률 분포 구하기 (Attention Distribution)
- Softmax를 사용해서 각 hidden state의 중요도를 확률로 변환함

### 3) Context Vector 생성
- Attention분포를 가중치해 인코더 hidden state드르이 가중합을 계산함

### 4) Concatenation
- 구한 context vector를 디코더 hidden state와 연결함
- 이를 통해서 최종적으로 다음 단어를 예측

## 2. Attention의 장점
- 긴 문장에서 중요한 단어에 더 집중이 가능하다
- 입력 시퀀스 전체를 활용하므로 정보 손실 완화
- seq2seq의 한게 (고정된 context vector 문제)를 극복함

> Attention 한 줄 정리 : 디코더가 출력할 때마다 인코더 전체를 다시 보면서, 지금 필요한 단어는 어디에 있지?하고 집중하는 메커니즘


## 3. Transformer
### 1) 배경
- seq2seq + Attention 구조는 긴 문장 번역 성능 향상에 큰 기여를 한다
- 하지만 여전히 RNN 셀을 사용하므로 연산이 순차적이기 때문에 속도가 느림

### 2) 아이디어
<img width="260" height="341" alt="image" src="https://github.com/user-attachments/assets/9beb5c7d-6b97-49b1-a5e9-817392d8d9cb" />

- RNN을 아예 제거하고, Attention을 기반으로 인코더와 디코더를 설계 = Transformer
> RNN = 앞에서 본 정보를 기억하며 시퀀스를 처리하는 모델이지만 긴 문장에서는 기억력이 약해짐

## Transformer - Encoder
### Positional Encoding
<img width="527" height="205" alt="image" src="https://github.com/user-attachments/assets/4910d8ce-b0b5-46d4-be8d-a50486384c61" />

<img width="500" height="369" alt="image" src="https://github.com/user-attachments/assets/cbdab151-a087-43e8-9ef9-dcdba611ed86" />

- RNN 은 입력을 순서대로 처리하므로 위치 정보가 자연스럽게 반영된다.
- Transformer는 병렬 처리 구조 -> 단어의 순서 정보를 따로 알려줘야한다
- 따라서 각 단어의 enbedding에 사인/코사인 함수 기반의 위치 정보를 더해줌 -> 순서 정보가 고려된 embedding vector

### Query, Key, Value
- Query : 현재 단어가 어떤 정보를 찾고 싶은지
- Key : 단어의 속성 (비교 대상)
- Value : 실제 단어가 가진 정보
- Attention은 Query와 Key의 유사도를 계산하고 그 가중치로 Value를 종합
<img width="444" height="185" alt="image" src="https://github.com/user-attachments/assets/26ba1973-b6b3-4b06-8a0f-00897ded488f" />

### Self-Attention
- Attention을 자기 자신에게 적용하는 것
- 같은 문장 안에서 단어들 간 연관성을 찾음
- 예: `"The animal didn't cross the street because it was too tired."`  
  - "it" → "animal"에 높은 연관성(attention weight)  
<img width="349" height="401" alt="image" src="https://github.com/user-attachments/assets/c903ec46-0feb-46d2-93ca-cae15ab1c4e6" />

> 입력 문장 내의 단어들끼리 유사도를 구해서 it, animal의 연관성이 높다는 것을 알아냄
> 우리는 그 문장에서 it이 지칭하는 것이 animal인 것을 쉽게 알 수 있지만 기계는 그렇지 않기 때문에

### Scaled Dot-Product Attention

- Attention 점수 계산
<img width="460" height="92" alt="image" src="https://github.com/user-attachments/assets/33c52081-2c5b-46a6-95a2-09cd5a44d35a" />

1. 유사도 계산 (QKᵀ)
   - Query (찾고싶은 것) 과 Key를 내적해서 얼마나 관련이 있는지 점수를 계산
   - 값이 클수록 Query와 Key가 더 잘 맞는다는 의미
2. 스케일링 (√dₖ로 나누기)
   - Key의 차원이 커질수록 내적 결과 값이 너무 커질 수 있음 Softmax가 기울어져서 학습이 불안정해짐
3. Softmax 적용
   - 점수를 확률 분포로 변환 -> 모든 Key에 대한 가중치를 얻음
   - 중요도가 높은 단언느 큰값, 덜 중요한 단어는 작은 값이 됨
4. Value 와 결합
   - 각 Key에 대응되는 Value (실제 단어 정보)에 가중치를 곱해서 합산
   - 즉, 현재 단어 (Query)가 집중해야 할 단른 단어(Value) 정보를 모다 최종 Context vector를 만든다

### Multi-Head Attention
<img width="286" height="167" alt="image" src="https://github.com/user-attachments/assets/58387721-68cd-47d7-9745-9b0d7da5f852" />

- 단일 attention만 쓰면 한 관점에서만 단어 관게를 반영함
- 여러 개의 Head를 병렬로 두어서 다양한 관점에서 학습함
- 각 head에서 나온 attention value들을 concatenate하여 최종 출력 생성

1. head개수 h개의 query, key, value 생성
2. 각 head 별 scaled dot-product attention 수행
3. head에서 나온 attention value들을 concatenate

## Transformer - decoder
### 1) Masked Self-Attention
<img width="483" height="151" alt="image" src="https://github.com/user-attachments/assets/f1bbae4d-7c5c-445c-a5b9-24395ccf17b2" />

- 필요성 : 디코더는 단어를 하나씩 생성해야함
- 아직 나오지 않은 미래 단어까지 참고하면 부정확한 예측이 발생할 수 있다.
- 따라서 Look-ahead Mask를 적용해 현재 시점 이후 단어는 보지 못하도록 차단
- 결과적으로 디코더가 자연스럽게 순차적 예측을 할 수 있도록 만듦

### 2) Encoder-Decoder Attention
- 디코더가 다음 단어를 예측할 때 인코더 출력 (전체 입력 시퀀스 정보)를 참고하도록 함
- Query : 디코더의 현재 시점 hidden state
- Key, Value : 인코더가 만든 hidden state 전체

- 디코더는 Query와 Key를 비교해서 현재 예측에 필요한 Value를 선택적으로 활용
- 즉 , 입력 문장의 전체 의미를 반영해 더 정확한 출력이 가능함

