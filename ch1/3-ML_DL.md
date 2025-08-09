<img width="268" height="298" alt="image" src="https://github.com/user-attachments/assets/b5332117-8ce0-41d3-8fec-2d8c1bfabc37" /># 01. INTRODUCTION

## 1) 인공지능
인간의 학습능력, 추론능력, 지각 능력을 인공적으로 구현시키는 컴퓨터 과학기술
- 사고능력
- 문제 해결
- 학습 능력

<img width="520" height="345" alt="image" src="https://github.com/user-attachments/assets/533a3521-9646-48a7-8a6a-2fc26be63b6d" />

## 2) 머신러닝 vs 딥러닝

공통점

- 데이터 기반 학습
- 최적화 알고리즘 사용
- 반복 학습을 통한 성능 향상
- 일반적인 파이프라인
  -> 데이터 준비 및 이해 → EDA 및 전처리 → 피처 엔지니어링 → 모델링 → 하이퍼파라미터 튜닝 → 평가 및 피드백

# 02. ML : 머신러닝

머신러닝의 목적

- 머신러닝 모델은 데이터를 통해 학습하며, 핵심은 가중치 행렬을 최적화하는 과정
- 모델은 예측 결과와 실제 값 사이의 오차(손실)을 계산
- 오차를 줄이기 위해서 손실함수의 기울기를 계산하고 가중치 행렬의 값을 조금씩 갱신하는 과정 반복

> 가중치 행렬
- 입력 특성에 부여하는 중요도의 집합 (행렬 형태)
<img width="743" height="244" alt="image" src="https://github.com/user-attachments/assets/dd57a880-9317-4048-a8bd-6ca4497941e0" />

> 머신러닝 파이프라인

데이터준비 및 이해 → EDA 및 전처리 → 피쳐 엔지니어링 → 모델링 → 하이퍼파라미터 튜닝 → 평가 및 피드백 (필요시 EDA 및 전처리 과정으로 돌아감)

* 피드백 루프를 통한 모델 개선


## 1. 데이터 준비 및 이해

A.  도메인 이해 → EX) 금융 제조 마케팅 의료

- 데이터 출처
- 비즈니스/업무 흐름 파악

B. 기본 통계량 확인

- 평균/중앙값/분산/최소/최대

C. 메타데이터 검토

- 컬럼 설명, 단위, 생성 규칙

## 2. EDA 및 전처리

EDA :  탐색적 데이터 분석

전처리 :  데이터를 분석 및 처리에 적합한 형태로 만드는 과정

 분포 탐색 → 히스토그램, 박스플롯으로 분포 확인

상관관계 분석 → 히트맵으로 변수 연관성 파악

이상치 및 결측치 처리 → 도메인 지식으로 제거 및 대체

## 3. 피쳐 엔지니어링

피처 엔지니어링 : 머신러닝 모델의 성능을 향상시키기 위해서 원본 데이터를 분석하고 가공해 유용한 특징을 만드는 과정

EX) 컬럼 DROP,  파생변수 생성, 스케일링 및 인코딩

## 4. 모델링
: 전처리 된 데이터를 기반으로 알고리즘을 선택 및 학습시켜서 예측 함수를 만드는 과정

→ 주어진 문제 (분류, 회귀, 클러스터링 등 ) 에 최적화 된 모델 파라미터 (가중치) 찾기

* 모델링 역시  가중치 행렬을 찾기 위한 과정 !
<img width="1037" height="229" alt="image" src="https://github.com/user-attachments/assets/dceb8509-8474-488f-8e73-906312fc704f" />

## 5. 하이퍼파라미터 튜닝

하이퍼파라미터 : 모델 구조나 학습 알고리즘에 외부에서 설정하는 값

EX) 학습률, 트리깊이, 은닉층 개수

튜닝의 필요성 : 잘못 설정시 과소적합 및 과적합 초래

→ 최적 파라미터로 모델 성능 및 일반화 능력 극대화
<img width="597" height="350" alt="image" src="https://github.com/user-attachments/assets/ce9fa46b-30b3-4efc-b000-6f9135d4bb88" />

<img width="1200" height="602" alt="image" src="https://github.com/user-attachments/assets/91c04bc3-c1c2-4abd-8d77-d570ed4b1206" />

### 1) 그리드서치

- 사용자가 지정한 값들의 격자에 따라서 가능한 모든 조합을 일괄 탐색하며 최적의 설정을 찾아내는 방식
- 장점 : 설정된 공간 내에서 최적 조합 보장 (전수조사)
- 단점 : 조합 수가 증가하면 연사 비용이 기하급수적으로 증가

### 2) 랜덤서치

- 전체 가능한 파라미터 공간에서 무작위로 일부 조합을 샘플링해서 실험하는 방법
- 장점 : 소수의 시도만으로도 준수한 성능을 확보할 수 있어, 제한된 시간 안에 좋은 결과를 얻을 수 있음
- 단점 : 운에따라서 최적의 하이퍼파라미터 조합을 놓칠 수 있음

### 3) 베이지안 최적화

- 사전정보를 바탕으로 최적 하이퍼파라미터 값을 확률적으로 추정하며 탐색
- 그리드서치나 랜덤서치보다 최적 하이퍼파라미터를 더 빠르고 효율적으로 찾을 수 있음

* 구성요소
  -  확률 모형 :  과거 실험 데이터를 바탕으로 아직 실험하지 않은 지점의 성능을 확률적으로 예측하는 모델
     <img width="228" height="34" alt="image" src="https://github.com/user-attachments/assets/382ac9b4-e1c6-431c-a4b4-065568f38ba7" />
  -  획득 함수 : 확률 모델의 예측을 바탕으로 다음 실험할 가장 유망한 하이퍼파라미터 조합을 결정하는 함수
     <img width="330" height="44" alt="image" src="https://github.com/user-attachments/assets/6f0acbc0-1332-4b2f-a3ab-2117e0328a05" />

1. 관측 : 몇 개의 하이퍼파라미터 조합에 대해 실제 모델 성능 측정
2. 모델링 : 관측된 데이터를 바탕으로 확률 모델을 학습해 전체 탐색 공간에 대한 예측 평균과 불확실성 파악
3. 결정 : 획득 함수를 사용해 모델의 예측과 불확실성을 모두 고려하여 다음으로 실험할 가장 효율적인 지점을 결정
→ 결정된 지점에서 실험을 수행하고 결과를 다시 반영하여 1~3단계 반복
→ 추정 함수가 실제 목적 함수에 근사하게 되고, 이 함수에서 최종 최적 값을 찾을 수 있음

장점

- 적은 시도 횟수로 효율적인 최적화 가능

단점

- 최적화 할 하이퍼파라미터의 수가 매우 많아지면 효율성 감소 + 계산 비용 증가

<img width="788" height="795" alt="image" src="https://github.com/user-attachments/assets/c898c6f9-e05c-43e8-b32f-94a697110933" />

## 6. 평가 및 피드백  

예측 결과 : 모델의 예측 결과 생성

성능 평가 : 예측 성능 측정 및 분석

재학습/튜닝 : 전처리 혹은 하이퍼파라미터 조정

개선점 파악 : 모델 개선 포인트 식별

### 1) 과대적합

- 너무 복잡한 모델 → 훈련데이터의 노이즈까지 학습
- 학습 에러가 낮고 검증 에러가 급증함

→ 일반화 필요함

### 2) 과소적합

- 너무 단순한 모델 → 중요한 패턴 학습을 못함
- 학습과 검증 에러 모두 높음
→ 모델링이 잘못됨
<img width="789" height="337" alt="image" src="https://github.com/user-attachments/assets/9f99fd82-6817-4e81-9bfe-67430466e9d8" />

* 적절한 복잡도를 가진 모델을 선택해야 과도한 단순화와 과도한 복잡화 모두를 피하고, 최적의 예측 성능을 얻을 수 있음

### 3) 편향

- 모델 예측 평균과 실제값 차이

### 4) 분산

- 학습 시마다 예측값 변동성

### 5) 불가피 오차

- 데이터 자체의 잡음 (noise)

### 6) 분산과 편향의 트레이드오프

- 모델이 복잡할수록 분산이 높고 편향은 낮아짐
- 과하게 단순한 모델은 과소적합, 과하게 복잡한 모델은 과대적합 초래

→ 좋은 모델은 이 둘의 균형을 맞춰서 예측 오류를 최소화하는 지점을 찾는 것이 중요함
<img width="647" height="275" alt="image" src="https://github.com/user-attachments/assets/8e92c251-6c05-4363-8e4b-7d7af9d4d3c2" />


# 06. 손실함수 & 평가지표

## 1. 손실함수
모델의 예측값과 실제값 간 차이를 수치화하는 함수  
- 모델 평가 : 손실 함수의 값이 작을수록 모델의 예측이 실제 값에 가깝다는 것을 의미함
- 학습 목표 설정 : 모델의 목표는 손실 함수의 값을 최소화 하는 것 
→ 가중치를 조정하며 손실 함수 값을 줄여나감
회귀용 손실함수 : MSE, MAE 등
분류용 손실함수 : Cross-Entropy, Hinge Loss 등
→ 손실함수를 최소화 하기 위해서 적절한 옵티마이저 선택 필요함

### 1) MSE(Mean Squared Error)
- 실제값과 예측값의 차이를 제곱한 뒤 전체 샘플 수로 나눈 평균

<img width="341" height="97" alt="image" src="https://github.com/user-attachments/assets/ed7375ef-23c1-4ff2-977c-66f6713534a1" />

- 주로 회귀 문제에서 사용하며 연속적인 숫자 값을 예측할 때 적합함
- 예측 오차의 크기를 제곱해 손실 측정
- 항상 0 이상의 값, 0에 가까울수록 예측이 정확 (차이가 거의 없다는 뜻임)
- 미분이 가능해 경사 하강법 기반 최적화에 용이함
- 이상치에 민감하게 반응할 수 있음 ( 오차 제곱 때문에)

### 2 )Cross_Entropy
- 예측된 확률 분포가 실제 확률 분포와 얼마나 다른지 측정 분포 간의 거리를 나타냄

<img width="642" height="98" alt="image" src="https://github.com/user-attachments/assets/f438a93f-195c-4d29-810b-56252a9233b4" />

- 분류 문제, 특히 모델의 출력이 확률 분포일 때 사용함
- 모델이 정답 클래스에 낮은 확률을 부여하거나 오답 클래스에 높은 확률을 부여할수록 큰 손실을 반환
- 모델이 올바른 클래스에 대해 높은 확률을 예측하면 손실이 작아지고, 잘못된 클래스에 높은 확률을 예측하면 손실이 커짐

### 혼동행렬
- 분류 모델의 예측 결과와 실제 값을 교차표 형태로 정리한 행렬
- TP, TN, FP, FN 값을 한눈에 볼 수 있음
- TP : 실제 음성을 음성으로 예측
- FP : 실제 음성을 양성으로 잘못 예측 = 제 1종 오류
- FN : 실제 양성을 음성으로 잘못 예측 = 제 2종 오류
- FP : 실제 양성을 양성으로 예측
<img width="634" height="281" alt="image" src="https://github.com/user-attachments/assets/818e9b1e-fca6-4e64-b2e6-14f286439f7e" />

## 2. 평가 지표
<img width="852" height="578" alt="image" src="https://github.com/user-attachments/assets/d7292806-e2a8-4666-aaf2-a6331abc76c2" />

### ROC 커브

: 분류 임계값을 변화시키며, 민감도와 1-특이도의 관계를 시각화한 곡선

- 임계값을 여러 값으로 바꿔가며 모델의 전반적인 분류 능력을 평가할 때
- 모델의 전체적인 성능을 비교하고 싶을때
- 클래스 불균형이 심하지 않은 이진 분류 문제에서 모델 선택 기준으로 활용할 때
  <img width="407" height="347" alt="image" src="https://github.com/user-attachments/assets/c106d3b6-3ace-4a68-b70f-c8d3ab47a841" />

# 04. DEEP LEARNING

## 1. Deep Learning Basic

### 1) ANN (Artificial Neural network)
- 입력층, 은닉층, 출력층으로 구성된 모든 신경망 구조
- 뉴런(노드)들이 서로 연결되어서 정보를 전달하고 처리함
- 은닉층 개수, 연결 방식, 구조에 상관없이 가장 포괄적인 개념
  <img width="323" height="286" alt="image" src="https://github.com/user-attachments/assets/01f39e4f-79ca-408a-9d70-1484fc56c5b3" />


### 2) DNN (Deep Neural Network)
- 은닉층이 2개이상인 ANN뉴런 (노드) 들이 서로 연결되어 정보를 전달하고 처리함
- 보통 Fully Connected (FC) Layer 중심으로 구성됨 → 각 층의 모든 뉴런이 다음 층의 모든 뉴런과 연결됨
<img width="491" height="299" alt="image" src="https://github.com/user-attachments/assets/1e4f0710-1613-4c6f-bec8-bb5db539e1a7" />


### 3) Deep Learning Basic
- DNN을 포함한 다양한 심층 구조를 가진 신경망 전체를 의미함
- 딥러닝의 ‘딥’ = 여러 층으로 구성된 심층 신경망을 통해서 표현을 학습함
→ 신경망은 퍼셉트론이라는 일종의 인공 뉴런으로 구성됨

### 4) 퍼셉트론 
- 여러 신호를 받아서 하나의 신호를 출력 = 사람의 뉴런이 정보를 전달하는 방식과 유사함
<img width="1180" height="263" alt="image" src="https://github.com/user-attachments/assets/5f030871-c4b3-4c94-8cab-a607d6e9b246" />

## 2. 딥러닝 작동 방법
목표 : 모델의 예측값이 실제 정답에 더 가까워지도록 퍼셉트론의 가중치 값을 찾는것

### 1) Feed Forward
- 입력값이 신경망의 가중치와 은닉층을 거쳐 출력값을 생성하는 과정

### 2) Back propagation
- 출력층에서 입력층 방향으로 오차를 계산해 경사 하강법을 통해 가중치를 업데이트하는 과정
-> 예측이 틀린 정도를 바탕으로 어디서 잘못됐는지 계산하고, 가중치를 조금씩 조정해서 다음번에는 더 정확한 예측을 하도록 학습시킴
<img width="768" height="253" alt="image" src="https://github.com/user-attachments/assets/8ec6206a-937a-444e-ab99-41748b6d3223" />

### 3) multilayer Perceptron (MLP)
- 가장 기본적인 형태의 MLP는 모든 입력 노드와 출력 노드가 서로 연결된 완전 연결층 
-> fully-connected layer로 구성됨
<img width="268" height="298" alt="image" src="https://github.com/user-attachments/assets/21390d70-66b6-446f-a0aa-d84a53d92f89" />

### 4) FC layer의 한계 = DNN의 한계
- 입력 데이터를 반드시 1차원 벡터로 변환 해야함 → 이미지 입력을 사용할 때 이웃한 픽셀 간의 관계를 고려하지 않아서 공간 정보가 손실 된다.
<img width="465" height="293" alt="image" src="https://github.com/user-attachments/assets/d1285376-9930-4a5b-bc3f-932be5872ac6" />

## 3. CNN
- 합성곱층(Convolution) → 풀링층(Pooling) → 완전연결층(FC) 구성
- 공간 정보를 유지하며 특징 추출

### 1) Convolution Layer
: 정의된 수용 영역 (커널, 필터)을 이용해 입력 이미지에서 국소적인 특징 추출

- 직사각형 수용 영역이 이미지를 스캔하면서 공간적 특징을 뽑아냄
- 이미지의 2차원 구조와 공간정보를 유지 (FC layer한계 극복)
- 합성곱 필터가 일정 영역을 슬라이딩 → 픽셀들의 상대적 위치와 주변 관계를 반영 가능

->  단순 벡터가 아니라 공간 구조를 반영한 특성 맵을 만들어서 이미지의 중요한 정보를 학습

<img width="448" height="262" alt="image" src="https://github.com/user-attachments/assets/e943442a-f622-482a-8b9a-ce018c0ddac7" />

합성곱층 하이퍼파라미터 = (filter 개수, 크기, stride, padding)

1. stride : 커널(필터)이 이미지를 스캔하며 이동하는 픽셀 수 
2. padding : 원래 이미지 주변에 값을 추가해서 이미지 크기를 유지함

 작동방법

- 합성곱 필터는 스트라이드 값에 따라 이미지를 이동
- 필터가 위치한 각 지점에서 필터와 입력의 겹치는 부분끼리 원소별 곱 계산 → 그 값을 모두 더함 → 하나의 출력 값

<img width="603" height="370" alt="image" src="https://github.com/user-attachments/assets/a6c5f954-f6f5-468b-98bd-a46e797ba6a7" />

<img width="487" height="261" alt="image" src="https://github.com/user-attachments/assets/e9dd1df4-92ac-4137-b9eb-8ca295bf4707" />

->출력되는 특성 맵의 채널 사이즈가 커진다

<img width="572" height="475" alt="image" src="https://github.com/user-attachments/assets/5becafdd-cacb-429c-bbab-46ca629fb607" />

### 2) Pooling Layer
- 특성 맵을 더 작은 크기로 압축하는 단계

<img width="448" height="208" alt="image" src="https://github.com/user-attachments/assets/58f78206-1dda-45b3-9d1b-6b31223cb253" />

### 3) FC Layer
- 완전 연결 레이어에 입력하기 위해 특성맵을 1차원 벡터로 변환함
<img width="573" height="203" alt="image" src="https://github.com/user-attachments/assets/f7eb36f5-4718-4c9b-96ef-b194b46cfa74" />

### 4) Activation Function
- 각각의 convolution layer 와 Fully-connected Layer 다음에 적용됨 (비선형성 추가 → 출력값과 예측값 생성 )


## 4. RNN
: 시간의 흐름에 따라 변화하는 연속적인 시퀀스 데이터를 잘 처리할 수 있음

- 입력을 받아들이면서 이전 입력에서 얻은 정보를 기억하고 현재 입력을 처리할 때 기억 활용
- 현재 입력을 처리한 결과는 다음 입력을 위해서 내부 상태에 반영

<img width="576" height="350" alt="image" src="https://github.com/user-attachments/assets/12ae08a0-17a4-436a-bc8b-5267f32b2917" />

### 1) RNN 의 유형

<img width="820" height="447" alt="image" src="https://github.com/user-attachments/assets/60195238-75aa-43fd-b727-9e794c64302a" />


## 5. Normalization

### 1) Batch Normalization

- Epoch : 학습 데이터 전체를 한 번 학습하는 것
- Batch : Gradient를 구하는 단위

<img width="334" height="150" alt="image" src="https://github.com/user-attachments/assets/4a86e390-77fb-4ea7-b1b9-aa1d23a54b00" />

<img width="617" height="289" alt="image" src="https://github.com/user-attachments/assets/2c0c04e6-6c2b-46ce-bf92-1cd38bfb472c" />

- 입력 값이 FC와 활성화 함수를 거치며 연산 전/후에 데이터 간 분포가 달라질 수 있다
- 이와 유사하게 Batch 단위로 학습을 하게 되면 Batch 단위 간 데이터 분포의 차이가 발생
- 즉 Batch별로 데이터가 상이하게 되는 것 → 모델이 데이터를 일관되지 않게 이해하게 됨

<img width="541" height="263" alt="image" src="https://github.com/user-attachments/assets/d1c410ef-8dd9-4d5a-a1e0-c3ddcc2d2e14" />

- Batch Normalization은 학습 과정에서 각 배치 단위 별 다양한 분포를 가진 데이터를 각 배치별로 평균과 분산을 이용해 정규화
- FC → Batchnorm → Activation function

<img width="459" height="113" alt="image" src="https://github.com/user-attachments/assets/a72e6bb0-49ab-4e80-a2ae-2f340b76669b" />

- γ : 스케일링 정도
- β : bias (이동정도)
- γ, β 를 모델이 학습해서, 각 뉴런이 가장 안정적으로 계산할 수 있는 데이터 분포를 스스로 찾아가도록 도움
- 구체적으로는 정규화를 거친 후 ReLU를 적용하면 음수 부분이 0으로 처리됨
    → 이를 방지하기 위해서 적당하게 스케일을 조정하고 이동시킴

Training 단계에서 Batch Normalization

- 배치 단위 별로 평균과 분산을 계산

Test 단계에서 Batch Normalization

- 배치 단위로 평균 및 분산을 구하기가 어려워 학습 단계에서 배치 단위의 평균 및 분산을 저장해 놓고 테스트 시에는 저장한 것을 사용

- 학습 단계에서는 각 배치의 평균과 분산을 계산해 지속적으로 이동평균으로 저장
- 테스트 단계에서는 이 저장된 이동평균과 분산 사용

### 2) Layer Normalization
- Batch normalization과 방식은 같지만  γ, β  값이 다르다
- 배치 단위의 평균과 분산 사용 X
- 개별 데이터에 들어있는 feature의 평균과 분산을 사용
- 배치 단위가 아니기 때문에 training 과 test 동일하게 진행
<img width="591" height="240" alt="image" src="https://github.com/user-attachments/assets/b33bd3f9-8dda-4aa6-9dfc-0d96df06b51d" />

1.Layer Normalization

- 개별 데이터 포인트들로 정규화 진행
- 주로 RNN, Transformer에서 사용

2. Batch Normalization

- 채널 별로 정규화 진행
- 주로 CNN에서 사용


## 6. Optimizer
- 손실 최소화를 위해 파라미터를 업데이트하는 알고리즘
- 목표 : 손실 함수 기울기를 기반으로 최적의 파라미터 조합을 탐색
<img width="768" height="449" alt="image" src="https://github.com/user-attachments/assets/b795a889-23c1-4d59-83a4-251c51b4892e" />

### 1) 경사하강법 (Gradient Descent)

: 손실함수를 최소화하기 위해 사용되는 최적화 알고리즘 → 모델 파라미터를 반복적으로 조금식 조정해 나가는 방식
<img width="445" height="149" alt="image" src="https://github.com/user-attachments/assets/a08226f9-c13f-4efa-8dce-f4a1e27fe5e6" />

### 2) SGD (Stochastic Gradient Descent)

: 전체 데이터가 아닌 한 개 의 샘플을 이용해 매 반복마다 파라미터를 업데이트하는 기법

장점 

- 데이터 셋이 크더라도 업데이트가 빠름

단점

- 업데이트가 샘플마다 달라 진동이 심함
- mini-batch 단위로 업데이트하면 mini-batch gradient descent

<img width="494" height="350" alt="image" src="https://github.com/user-attachments/assets/34abfdef-079e-49d4-af8b-2f3773a4ee61" />

### 3. Adam (Adaptive Moment Estimation)

: 모멘텀과 적응적 학습률을 결합해서 빠르고 안정적으로 파라미터를 없데이트하는 최적화 알고리즘

- 이전까지의 기울기를 기억해서 현재 업데이트에 반영 → 관성처럼 작용해서 변동이 심한 방향엔 덜 반응하고 일관된 방향엔 더 강하게 움직이게 함 = 모멘텀
- 각 파라미터가 얼마나 자주, 크게 변화했는지를 바탕으로, 학습률을 자동조정 = WMSprop

<img width="455" height="197" alt="image" src="https://github.com/user-attachments/assets/5bd196b5-aa9b-4aa5-a707-2c555828b897" />

장점

- 학습이 안정적이고 빠름
- 복잡한 딥러닝 모델에서도 좋은 성능 결과
- 다른 옵티마이저들보다 하이퍼파라미터 튜닝이 상대적으로 쉬움
