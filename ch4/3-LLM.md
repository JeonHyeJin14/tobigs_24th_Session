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
  - 
