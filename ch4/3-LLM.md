# 01.언어 모델링 (Language Modeling)
: 문장을 구성하는 단어 등에 각각 확률을 부여한 모델로 중간에 비워져 있거나 다음에 나올 단어를 예측하여 생성하는 방법

#### 언어 모델의 발전 과정
1. 통계적 언어 모델
2. 신경망을 사용한 언어 모델
3. 트랜스포머 기반의 언어 모델-> 최근의 LLM은 대부분 트랜스포머 구조에 기초함

#### 언어 모델, LLM 분야의 폭발적 성장을 이뤄낸 두 가지 요소
1. 트랜스포머 아키텍처
2. 자기 지도 학습(self-supervised learning)을 통한 사전 훈련 모델

## 1. 통계적 언어모델
<img width="289" height="173" alt="image" src="https://github.com/user-attachments/assets/c280c319-08d9-425c-a7eb-7dd4fa3d965c" />

### 1) 희소문제
: 충분한 데이터가 없다면 실세계에서 사용되는 단어가 학습하는 말뭉치에서는 존재하지 않을 수 있음
- 해결책 : 충분한 데이터가 없다면 실세계에서 사용되는 단어가 학습하는 말뭉치에서는 존재하지 않을 수 있음
- 문제점 : 시퀀스의 길이가 커질수록 특정 조합이 말뭉치에서 등장하지 않을 가능성 증가

### 2) 여전히 존재하는 희소 문제
- 적절한 n 선택의 trade-off 중요
  - n을 크게하면 더 정확한 예측이 가능해지지만 희소 문제가 더 커질 수 있다
- 도메인마다 큰 차이를 보이는 말뭉치(corpus) 존재함

### 3) 언어 모델 분야 학습의 어려움 -> 인공신경망을 활용한 언어모델의 사용 제안

## 2. 신경망을 사용한 언어모델
### 1) 분포가설 : 비슷한 위치에 있는 단어들은 비슷한 의미를 가짐
- 학습한 말뭉치에 존재하지 않는 단어이더라도 유사한 단어가 존재했다면 확률을 계산할 수 있음 01.언어 모델링 (Language Modeling)
: 문장을 구성하는 단어 등에 각각 확률을 부여한 모델로 중간에 비워져 있거나 다음에 나올 단어를 예측하여 생성하는 방법

#### 언어 모델의 발전 과정
1. 통계적 언어 모델
2. 신경망을 사용한 언어 모델
3. 트랜스포머 기반의 언어 모델-> 최근의 LLM은 대부분 트랜스포머 구조에 기초함

#### 언어 모델, LLM 분야의 폭발적 성장을 이뤄낸 두 가지 요소
1. 트랜스포머 아키텍처
2. 자기 지도 학습(self-supervised learning)을 통한 사전 훈련 모델

## 1. 통계적 언어모델
<img width="289" height="173" alt="image" src="https://github.com/user-attachments/assets/c280c319-08d9-425c-a7eb-7dd4fa3d965c" />

### 1) 희소문제
: 충분한 데이터가 없다면 실세계에서 사용되는 단어가 학습하는 말뭉치에서는 존재하지 않을 수 있음
- 해결책 : 충분한 데이터가 없다면 실세계에서 사용되는 단어가 학습하는 말뭉치에서는 존재하지 않을 수 있음
- 문제점 : 시퀀스의 길이가 커질수록 특정 조합이 말뭉치에서 등장하지 않을 가능성 증가

### 2) 여전히 존재하는 희소 문제
- 적절한 n 선택의 trade-off 중요
  - n을 크게하면 더 정확한 예측이 가능해지지만 희소 문제가 더 커질 수 있다
- 도메인마다 큰 차이를 보이는 말뭉치(corpus) 존재함

### 3) 언어 모델 분야 학습의 어려움 -> 인공신경망을 활용한 언어모델의 사용 제안

## 2. 신경망을 사용한 언어모델

### 1) 분포가설 : 비슷한 위치에 있는 단어들은 비슷한 의미를 가짐
- 학습한 말뭉치에 존재하지 않는 단어이더라도 유사한 단어가 존재했다면 확률을 계산할 수 있음

### 2) MLP(Multi-Layer Perception)
- 신경망을 이용해 단어의 의미적 유사성을 학습하고 희소 문제를 해결함

<img width="762" height="270" alt="image" src="https://github.com/user-attachments/assets/afd7ae16-93d4-4145-b101-d23f09565f77" />

단어의 희소한 원-핫 인코딩에서 밀집 표현으로 바꾸며, 단어 벡터 간의 유사도를 생각할 수 있는 단어 임베딩(word Enbedding) 등장

### 3) 재귀신경망 (Recurrnt Neural Network) : 순환 신경망을 사용한 언어모델
<img width="621" height="164" alt="image" src="https://github.com/user-attachments/assets/8377fac3-af8f-442e-9392-7280c3f5aca9" />

<img width="443" height="290" alt="image" src="https://github.com/user-attachments/assets/1cc650c9-c976-409f-98ae-25b43b057ac9" />

1. 기존의 신경망을 사용한 언어모델은 고정된 길이의 입력만 사용가능 -> 하지만 재귀 신경망을 사용한 언어모델은 다양한 길이의 입력 시퀀스를 다룰 수 있음
2. 작업을 위한 corpus의 특성을 인간이 직접 선택할 필요없이 의미있는 표현 (representation)자체를 신경망이 학습 가능

### 3) 장점
<img width="1189" height="203" alt="image" src="https://github.com/user-attachments/assets/758b50b4-1ee2-4c83-bdd4-435493bfb5b0" />

- 장기 의존성 문제의 해결방안임
<img width="507" height="286" alt="image" src="https://github.com/user-attachments/assets/bdc52a69-6c0d-4ed9-a46e-d49a9a3d7174" />

1. 장단기 메모리
<img width="415" height="299" alt="image" src="https://github.com/user-attachments/assets/6685ac6e-6399-43f3-a49a-b70ee635a1d1" />

2. 게이트 순환 유닛

# 02.Trasformer Architecture

## 1. 트랜스포머의 등장 배경
- RNN/LSTM/GRU 같은 순환 신경망의 한계점
  - 문장을 한 단어씩 순서대로 처리하므로 병렬화가 어렵고 긴 문맥을 기억하기 힘들다
- 기계 번역에서 사용한 시퀀스-투-시퀀스 모델의 한계점
  - 고정 길이 벡터 사용에 따른 정보 손실
  - 기울기 소실

-> 현재 트랜스포머 등장
  - NLP의 판도를 완전히 바꿈
  - 지금의 ChatGPT, Bard Claude, LLaMA같은 LLM들 다 트랜스포머 기반

## 2. 트랜스포머의 정의
- 트랜스포머 : 기존의 seq2seq2 구조인 인코더-디코더를 따르면서도 RNN을 사용하지 않고 attention mechanism으로만 설계한 구조
  - stacked self-attention
  - point-wise, fully connected layer
- N개의 셀로 구성되는 인코더/디코더 구조 + Multi-head self attention 사용
  1. Sequential conputation의 감소 -> 더 많은 병렬 연산 가능
  2. 더 많은 단어 간의 dependency를 모델링
- 단어 입력을 순차적으로 받았던 RNN 방식이 아니므로 입력 문장에서 단어의 위치 정보를 알려주는 새로운 방식이 필요함 = Positional Encoding

## 3. 트랜스포머 아키텍처의 핵심 : 셀프 어텐션 (Self-Attention)
<img width="365" height="353" alt="image" src="https://github.com/user-attachments/assets/c16914ae-57e7-496d-b1ea-92f9c3dc8d55" />

: 주어진 작업을 해결하기 위해서 각 단어가 시퀀스 내의 다른 단얻르과 상호작용하는 연관성을 가중치로 부여해 문맥적인 관계를 파악함

ex. it의 의미는 ? animal vs street
- 문장 전체를 참고해서 연관된 단어를 좀 더 집중 (Attention)
<img width="719" height="415" alt="image" src="https://github.com/user-attachments/assets/4f29c523-dd89-45c8-b0f8-21569358e289" />

- 결국 트랜스포머 기반으로 하는 LMM은 고정된 수의 단어만을 고려하지 않고 전체 문맥을 고려할 수 있다.

## 4. 트랜스포머 구조
<img width="388" height="533" alt="image" src="https://github.com/user-attachments/assets/ad0dea3d-5cd8-48a3-964e-a162ca99e273" />

<img width="484" height="325" alt="image" src="https://github.com/user-attachments/assets/2119e792-028c-4dd7-b039-d7b9bb2c5a17" />

- 인코더 : 주어진 입력 시퀀스를 이해한다.
- 디코더 : 파악한 정보를 바탕으로 텍스트를 생성한다

## 5. 트랜스포머의 각 단계 설명

### 1) 단어 임베딩 Word Embedding
<img width="1063" height="133" alt="image" src="https://github.com/user-attachments/assets/b0b3c7f3-9d6b-4337-914f-36d248797837" />

- input과 output 토큰을 d_model 차원의 벡터로 전환하기 위해서 임베딩 학습
- 임베디 과정은 맨 아래 레이어에서만 수행됨
- d_model = 임베팅 벡터의 차원 = 인코더에서 정해진 입력의 크기 = 디코더에서 정해진 출력의 크기

### 2) Positional Encoding
<img width="597" height="232" alt="image" src="https://github.com/user-attachments/assets/05a7e23a-ce45-460c-9091-5442c866f626" />

- transformer의 입력으로 사용되기 전에 Positional encoding을 더해서 단어의 위치 정보를 전달한다.
<img width="416" height="214" alt="image" src="https://github.com/user-attachments/assets/28d24004-3f10-4850-9961-64780502bd5e" />

- enbedding vector와 더해질 수 있도록 positional encoding도 d_model 차원
- pos : 입력 문장에서 임베딩 벡터의 위치
- 유의점
  - 순서 정보가 보존됨
  - 같은 단어라고 해도 문장 내의 위치에 따라서 임베딩 벡터의 값이 달라질 수 있음
 
### 3) Encoder
  <img width="582" height="286" alt="image" src="https://github.com/user-attachments/assets/53703787-ddeb-456d-bf9b-452ba9ec64e7" />

- Transformer의 인코더는 6개의 레이어로 구성되며 하나의 레이어는 2개의 서브 레이어로 구성됨
 <img width="654" height="308" alt="image" src="https://github.com/user-attachments/assets/34a1625a-c86c-4a32-aeda-92c73c231d85" />

- 2개의 서브 레이어와 더불어서 Add&Norm으로 표현됨
- Residual connection, Layer Normalization이 사용됨

### 4) Decoder
<img width="546" height="574" alt="image" src="https://github.com/user-attachments/assets/07303052-69f2-4356-a378-a25370378e27" />

- Transformer의 디코더는 6개의 레이어로 구성되며 인코더와 달리 하나의 레이어는 3개의 서브 레이어로 구성되어 있음
- self-attention sub-layer는 인코더와 다르게 masking 되어 있음
  -> 이를 통해 현재 단어가 뒤에 있는 단어를 참조하지 못하도록 막는다

# 03. LLM : Large + Language Model

## 1. LLM 
<img width="1305" height="378" alt="image" src="https://github.com/user-attachments/assets/a7584fec-b7ae-4e88-b5dc-d921c8d798e6" />

: 대규모 + 언어 모델의 결합이 성능 향상을 이끈다
- 수십 억 ~수천 억의 파라미터를 갖는 LLM의 출현
  - 언어 모델의 성능 향상 + 새로운 문제 해결 능력의 발현
  - 자연어 처리의 한 분야였던 언어 모델링에서 벗어나 다양한 작업을 수행할 수 있는 사전 학습 모델이 됨
 
## 2. LLM과 Foundation Model
- Foundation Model
  - 대규모 데이터로 학습된 범용적인 사전학습 모델 (Base) -> 다양한 Task에 적용 가능
- LLM은 Foundation Model의 대표사례
  - 대규모 텍스트 데이터 학습
  - 단순 다음 단어 예측 Task를 벗어나 다양한 작업 수행이 가능함
> LLM은 현재 가장 흔하게 쓰이는 Foundation Model

# 04. Self-Supervised Learning(자기 지도 학습)

: 라벨이 없는 untagged 데이터를 활용하며 데이터 자체에서 정답을 만들어내어 학습하는 방식
<img width="584" height="252" alt="image" src="https://github.com/user-attachments/assets/2c86f2f6-ea98-4272-8e2f-edfa797bb64a" />

- 등장배경 : Tagged data의 수집 및 확보에 큰 비용이 요구됨
- 자기 지도 학습은 적은 수의 Tagged data로 모델 size 증가와 성능을 높일 수 있다는 장점

<img width="641" height="340" alt="image" src="https://github.com/user-attachments/assets/04b2a3f5-01d6-44ef-870b-e4df3db4af41" />

1. Pre-trained 모델 생성
   : 대량의 Untagged data를 이용해 데이터셋에 내재되어 있는 특징을 학습

2. Downstream task
   : 소량의 Targged data와 Pre-train 모델을 활용해 Fine-tuning을 진행함

<img width="462" height="348" alt="image" src="https://github.com/user-attachments/assets/1c86ed90-e164-42df-aa25-120089e1d482" />

## 1. 자동 인코딩 언어모델 (Autoencoding Language Model - AE)
: 마스킹처럼 입력이 손상된 상태에서 원래 입력을 복원하는 방식
- 주변 컨텍스트를 활용해 텍스트에서 누락되거나 가려진 단어를 예측하도록 훈련됨

-> 입력 문장의 의미와 구조를 이해하는데 탁월함

EX) BERT, RoBERTa, ELECTRA

## 2. Masked Language NOdel (MLM)
<img width="466" height="336" alt="image" src="https://github.com/user-attachments/assets/24797a09-ba46-4e96-9603-6fe51a327799" />

: AE의 대표적인 학습 방식
- 입력 문장으 일부 토큰을 MASK로 바꾸고 이를 예측하도록 학습함
- 주변 컨텍스트(문맥, 주변 단어들 정보)를 이해하는데 효과적

## 3. Encoder-only-model
- AE 기반 모델은 주로 Transformer Endocer만을 이용함
- 입력 : 전체를 인코딩한느 모델 구조
- 출력 : 입력과 길이가 같은 시퀀스 (각 입력 토큰의 벡터 표현)

<img width="866" height="205" alt="image" src="https://github.com/user-attachments/assets/75c4fa2c-aa0b-4f91-92e3-ad65737acde3" />

- 한 단어를 인코딩할 때 앞과 뒤 단어를 함께 고려함
- 현재 단어를 이해할 때 양옆의 모든 단어 정보를 활용

## 4. BERT 
<img width="593" height="303" alt="image" src="https://github.com/user-attachments/assets/f933f9c4-fd17-4c78-b5a5-366345c26f91" />

: AE 계열에 속하며 MLM방식으로 학습된 Endocer-only 구조의 모델
<img width="577" height="237" alt="image" src="https://github.com/user-attachments/assets/bec0da0b-80e5-410d-997b-5409c394414b" />

## 5. AR(Autoregressive Language Modle - AR)
<img width="726" height="317" alt="image" src="https://github.com/user-attachments/assets/0049439d-8fb3-455f-b33a-c820cab37015" />

: 문장의 앞에서부터 한 단어씩 순차적으로 예측하는 방식 - 다음 단어를 맞추를 과제에 적합함
ex) GPT 시리즈, LLaMA , Flacon
- Casual Laguage Modeling : AR의 대표적인 학습 방식, 현재 단어 예측 시 앞 단어만 이용함
  - 각 토큰의 예측은 기존 입력에만 의존하며 미래 토큰은 절대 접근하지 않음
 
## 6. Decoder-only-model
<img width="376" height="514" alt="image" src="https://github.com/user-attachments/assets/7fdb9a77-fc93-49d1-a6d2-fb5df1d26101" />

: Transformer의 디코더만을 사용하는 모델 구조 -> 출력 = 다음 단어의 확률 분포
- GPT : AR계열의 CLM 방식으로 학습된 Decoder-only  구조의 모델

## 7.  Encoder & Decoder with Tasformer
<img width="326" height="441" alt="image" src="https://github.com/user-attachments/assets/037d375c-29c5-450d-a8f6-8bbeefcd9d8f" />

### Encoder
- 입력 : 전체 문장
- 구조 : Self-Attention
  - 입력 문장의 모든 단어가 서로를 참고 (양방향)
- 출력 : 입력과 같은 길이의 단어 의미 벡터
- 특징 : 문장 의미, 관계 파악에 최적화

### Decoder 
- 입력 : 이전까지 생성된 단어 시퀀스
- 구조 :
  - Masked Self-Attention: 현재 단어는 이전 단어까지만 참고 (단방향)
  - Cross-Attention
- 출력 : 다음 단어 확률 분포
- 특징 : 텍스트 생성에 강함

# 05. RAG

## 1. LLM을 가르치는 두 가지 방법

<img width="1046" height="449" alt="image" src="https://github.com/user-attachments/assets/4d0e2594-11c7-4996-92b6-5cad33f3f810" />

## 2. RAG  시스템 구성 요소
<img width="708" height="364" alt="image" src="https://github.com/user-attachments/assets/c1b64d20-f089-4759-9092-702c8b5ae9d6" />

- 지식기반을 담고 있는 외부 문서
- Vector DB: 외부 문서를 저장함
- Embedding Model : 텍스트를 벡터로 변환
- LLM : 검색된 문서를 반영해 답변 생성

## 3. RAG 시스템 작동 단계
<img width="609" height="337" alt="image" src="https://github.com/user-attachments/assets/9c5c194d-e680-46b8-aa3a-b4c444a6ac3e" />

### 1. 지식 기반 생성 ( = 외부 데이터를 저장하는 과정 )
- 데이터 로드 -> 적절한 크기로 청킹 -> 임베딩 벡터로 표현 -> Vector DB에 저장
  - 청킹 : 여러 정보를 의미 있는 작은 덩어리(청크)로 묶어 기억하거나 처리하는 인지적 방법
  
### 2. 연관 문서 검색
- 사용자의 질문을 임베딩 벡터로 변환 -> Vector DB 에서 유사한 문서를 검색함

### 3. 답변 생성
- 검색된 문서를 기반으로 원래의 질문과 함께 LLM에 입력하여 답변을 생성
