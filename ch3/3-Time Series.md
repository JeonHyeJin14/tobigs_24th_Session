# 01. 시계열 분석

## 1. 시계열 데이터란? 
<img width="334" height="193" alt="image" src="https://github.com/user-attachments/assets/9d405f48-7325-4a9c-a280-a6337f175293" />

- 시간의 흐름에 따라 순차적으로 기록된 데이터로 각 관측값이 특정 시점에 연결
- 일정한 시간 간격으로 수집되며 의존적 패턴을 분석
- 필요성 : 과거 패턴을 이해하고 미래를 예측하거나 이상 현상을 탐지 하는데 필수적 -> 정확한 의사결정, 자원 최적화, 리스크 관리가 가능

## 2. 시계열 데이터 특징

<img width="716" height="229" alt="image" src="https://github.com/user-attachments/assets/855b6a23-8320-441a-92f4-47cff14baa0a" />

## 3. 시계열 데이터 구성요소
1. 계절 변동 : 일정한 주기로 반복되는 변동, 외부 요인에 의해 발생하는 특성
2. 순환 변동 : 수년 단위로 반복되는 장기적인 상승과 하락 변동으로 경기 변동이나 주기 변동을 의미 , 계절 변동으로는 설명되지 않으며 주기가 길어지고 규칙성이 덜함
3. 불규칙 변동 : 규칙성이 없는 변동 -> 많을수록 시계열 예측의 신뢰성이 낮아지는 경향
4. 추세 변동 : 시간의 흐름에 따른 장기적인 변화 경향으로 지속적인 일정한 움직임을 의미, 단기간 자료에서는 파악이 어려워짐


# 02. 정상성

## 1. 정상성이란?
<img width="342" height="248" alt="image" src="https://github.com/user-attachments/assets/dacd8794-347b-4756-85d4-b93a56ac8ff2" />

- 시계열 데이터의 통계적 성질이 시간이 지나도 변하지 않는 상태
- 어느 시점에서 관측해도 확률적 특성이 일정하게 유지되는 성질

1. 평균이 일정해 시간이 지나도 값의 중심이 변하지 않는 상태
2. 분산이 일정해 변동폭이 시간에 따라 변하지 않는 상태
3. 두 시점 간의 공분산이 시점이 아니라 시차에만 의존하는 상태
- 시간이 흘러도 데이터의 패턴과 변동 특성이 변하지 않는 확률 과정

## 2. 시각적으로 저상성 파악하기
<img width="440" height="325" alt="image" src="https://github.com/user-attachments/assets/392ced4e-68e5-4d4d-8d6e-d0c1dd84e41f" />


<img width="410" height="297" alt="image" src="https://github.com/user-attachments/assets/7dee6268-bfd3-425a-bbdc-a88f6e50af53" />

## 3. ADF 검정 (Augmented Dickey-Fuller Test)

### 1) 목적
- 시계열 데이터에 단위근이 존재하는지 검정 -> 정상성 여부 판단
- 단위근 있음 = 비정상성(추세나 확률적 경향 존재)
- 단위근 없음 = 정상성 (평균과 분산이 일정, 예측 가능성 증가)

### 2) 단위근
- 시계열 자기회귀식에서 시차 1의 계수 = 1인경우
- 단위근이 있음 = 현재 값이 과거 값에 100%의존 = 충격의 영향이 영구 지속
- 평균 , 분산이 시가넹 따라 변하고 충격이 누적되어 정상성 없음

### 3) 가설설정
- 귀무가설 : 단위근 존재
- 대립가설 : 단위근 없음

### 4) 회귀식 기반 단위근 검정
<img width="328" height="70" alt="image" src="https://github.com/user-attachments/assets/f5debea7-d073-4a6c-bbec-5e7d18392e5c" />

### 5) 판단 기준
<img width="400" height="96" alt="image" src="https://github.com/user-attachments/assets/9312b6a5-82ce-4fb5-8a40-f6f8cc4ee2de" />


# 03. 통계적 시계열 예측 모델

## 1. AR 모델 
<img width="483" height="231" alt="image" src="https://github.com/user-attachments/assets/012597ea-de57-4e19-964b-b6492df26dab" />

- 자기 상관성을 시계열 모형으로 구성한 것으로 변수의 과거 관측값의 선형 결합을 통해서 변수의 미래값을 예측하는 모델
- 이전의 관측값이 이후의 관측값에 영향을 준다는 아이디어에 기반 = "과거의 값이 현재의 값에 영향을 준다"
- 파라미터 값으로는 p를 이용해 AR(p)의 형태로 나타냄

## 2. MA 모델
<img width="467" height="220" alt="image" src="https://github.com/user-attachments/assets/6b1a0e57-6c4f-446d-bfb8-0f9dd43ef086" />

- 시계열의 현재 값을 과거 시점들의 오차항의 선형 결합으로 표현하는 모델 = "현재 값은 과거 예측이 틀린 정도의 누적효과로 설명된다"
- AR 모델이 과거 값을 이용하는 반면에 MA모델은 과거 예측 오차를 이용함 
- 파라미터 값으로는 Q를 이용해서 MA(q)

## 3. Causal Convolution
<img width="371" height="269" alt="image" src="https://github.com/user-attachments/assets/29deb1ce-c8be-4280-8177-575d775a6347" />

- 시점 t의 출력은 현재 시점 t와 그 이전 시점의 입력 데이터만 사용
- 미래 시점의 데이터가 현재 예측에 영향을 주지 않도록 설계 -> 인과성 보장
- 시계열 예측 모델에서 자주 쓰임 (미래 정보 누설 방지)

### 특징
1. 출력 길이 = 입력 길이
   - 1D Fully-Convolution Network 사용
   - 길이 유지를 위해서 커널사이즈 -1만큼 zero padding사용
   - dilation적용시 receptive field (참조구간)이 커널사이즈-1 * dilation factor로 확장됨

2. 시간 인과성 유지
   - 시점 t의 출력은 오직 현재와 과거 데이터만 사용
   - 미래 데이터 참조 금지 -> 데이터 누설 방지
    
3. 구조적 특징
   - 일반 합성곱과 다르게 과거로만 receptive field 확장
   - 여러 층을 쌓으면 더 긴 과거 정보까지 활용가능
   - dilation convolution을 함께 쓰면 적은 층으로도 장기 의존성 확보

## 3. ARMA 모델
<img width="548" height="150" alt="image" src="https://github.com/user-attachments/assets/881a45fc-a226-4da4-9876-a5d8c95a2086" />

- AR(자기회귀)와 MA(이동평균) 모델을 결합한 시게열 모델
- 데이터의 자기상관 구조 (AR)와 오차항 구조 (MA)를 동시에 반영할 수 있음
- 보통 정상성을 만족하는 시게열 데이터에 적용

## 4. ARIMA 모델
<img width="403" height="158" alt="image" src="https://github.com/user-attachments/assets/9075a9d0-0c4b-473b-a89a-140166c0c753" />

- ARMA 모델에서 d차 차분을 추가적으로 적용시킨 모델
- 정상성 시게열 뿐 아니라 비정상 시계열도 차분을 통해 적용 가능
- ARIMA(p, d, q) : d차 차분한 데이터에 AR(p) 모뎧오가 MA(q)모형을 합친 모델

> 차분 : 시계열의 현재 값에서 이전 값을 빼는 것
- 목적 : 추세나 계절성 같은 장기 패턴을 제거해 평균과 분산이 일정한 정상 시계열로 변환

## 5. SRIMA 모델
- ARIMA에 계절성 요소를 추가한 모델
- 비계절성 부분 = (p, d, q) -> ARIMA와 동일
- 계절성 부분 = (P, D, Q, m) -> m : 계절 주기, D : 계절 차분 횟수
<img width="493" height="159" alt="image" src="https://github.com/user-attachments/assets/055a5d24-7322-
493d-88bd-a454af437bda" />


# 04. 딥러닝 기반 시계열 예측 모델

## 1. RNN
<img width="493" height="159" alt="image" src="https://github.com/user-attachments/assets/5326963d-e2bb-4792-9101-ac0602fe02cd" />

### 기본구조
- 순환 구조 : 이전 시간 단계의 정보를 은닉 상태로 저장해 다음 단계 입력에 활용하는 신경망 구조
- 일반적인 Feedforward Neural Network와 달리 시간 순서를 반영할 수 있음

### 특징
- 시계열/순차 데이터 처리 : 시간의 흐름에 따라 발생하는 데이터에 적합하며, 이전 맥락을 반영한 예측가능
- 기억의 한계 : 시퀀스가 길어지면 과거 정보가 희석되어 초기 입력의 영향이 사라지는 장기 의존성 문제
- 훈련방식 : 시간에 따른 역전파를 이용해 가중치를 업데이트하며 학습 과정에 기울기 소실 문제 발생가능

## 2. LSTM
<img width="349" height="232" alt="image" src="https://github.com/user-attachments/assets/6fd31dfa-15dd-4317-b130-06125d6f61de" />

### 핵심개념
- 셀 상태 : 정보가 길게 흘러갈 수 있는 경로, 불필요한 정보는 지우고 필요한 정보는 유지
- 게이트 구조 : 정보를 조정하는 장치, 세 가지 게이트(입력, 망각, 출력)를 통해 어떤 정보를 기억/삭제/출력할지 결정

### 구조
1. 망각 게이트
   - 불필요한 옛정보를 지워서 기억 유지 한계를 극복하는 역할
2. 입력 게이트
   - 현재 들어온 중요 정보를 선택적으로 장기 메모리에 추가하는 역할
3. 출력 게이트
   - 다음 단계로 얼마나 정보를 내보낼지 결정해 필요한 부분만 전달하는 역할
> 긴 시간 간격의 패턴도 학습 가능하며 언어 모델링, 시계열 예측등 다양한 분야에서 사용


## 3. GRU 
<img width="323" height="229" alt="image" src="https://github.com/user-attachments/assets/3f209be9-bc6f-4af6-a2f2-8e68d1be7d3f" />

### 등장배경
- LSTM과 마찬가지로 RNN의 장기 의존성 문제를 해결하기 위해 제안됨
- LSTM을 단순화 한 형태

### 핵심구조
- LSTM의 3개의 게이트 대신 2개 게이트만 사용함
1. 업데이트 게이트
   - 이전 은닉 상태 정보를 얼마나 유지할지 현재 입력으로 얼마나 업데이트할지를 결정 -> LSTM의 입력게이트 + 망각 게이트 역할을 동시에 수행

2. 리셋 게이트
   - 불필요한 과거 정보를 제거하고, 새로운 입력과 얼마나 결합할지를 조절 -> 과거 정보 반영 정도를 제어함

## 4. TCN

### 등장배경
1. 순환신경망(RNN) 한계 극복
   - RNN, LSTM, GRU는 시계열/순차 데이터 처리에 강점이 있지만 병렬 처리 불가하고 장기 의존성 학습이 어려움, 기울기 소실/폭주 문제 존재
   - 특히 긴 시퀀스에서 정보가 뒤로 갈수록 손실되기 쉽고 학습 속도 느림
2. CNN의 장점 활용
   - CNN은 병렬 연산이 가능하고 GPU 최적화가 잘 되고 있어서 빠른 학습과 효율적 파라미터 공유가 가능함

### 주요개념 
1. Caussal convolution
   - 현재 시점의 출력이 현재 시점과 과거 입력만 사용하도록 설계
   - 미래 데이터를 참조하지 않아 예측 모델의 시간 인과성 보장
2. Fully Convolution Structure
   - 전 구간이 합성곱 계층으로만 구성 -> 병렬 연산 가능 -> RNN 대비 학습 속도 빠름
3. Dilated Convolution
   - 합성곱 필터 적용시 입력 사이에 간격을 두어 receptive field(참조 가능한 시점 범위)를 확장
   - 깊이가 얕아도 멀리 있는 과거 정보를 효율적으로 참조가능
4. Residual Connection
   - 깊은 네트워크에서도 학습 안정성을 높이고 기울기 소실 방지
   - 입력과 출력을 직접 연결해 정보 손실을 최소화

## 5. Dilated Convolution
- 필터 사이에 간격을 둬서 한 번에 더 넓은 범위의 입력을 보는 방식

### Receptive Field
- 필터가 한 번에 참고할 수 있는 입력 데이터의 범위

### Dilated Convolution 원리
<img width="534" height="173" alt="image" src="https://github.com/user-attachments/assets/d64347d6-2e8d-4760-9b21-89ef159873c7" />

- 입력 데이터 사이에 간격을 두고 필터를 적용
  ex) dilation=2이면 시점 1 -> 시점 3 -> 시점 5 처럼 건너뛰며 참조
- 이렇게 하면 필터 크기를 늘리지 않고도 멀리 떨어진 과거 데이터까지 한 번에 참조 가능
- Layer를 깊에 쌓을수록 Receptive Field가 지수적으로 증가
- 장점 : 먼 과거 정보 반영가능, 연산량 증가 최소화

## 6. Residual Connection
<img width="253" height="39" alt="image" src="https://github.com/user-attachments/assets/82e10cd0-eaab-4534-9dc4-5890ade7b9f0" />

- 네트워크의 입력값 x를 중간 계층을 거친 변환 결과 F(x)와 더해서 출력하는 구조
- TCN은 Receptive Field 확보를 위해서 layer를 깊게 쌓음 -> 깊을수록 기울이 소실/폭주 문제 발생
- REsidual Connection은 이 경로를 직접 연결해서 정보와 gradient 손실 방지
- 복잡한 변환이 필요 없는 경우에 신호가 거의 그대로 전달되어 불필요한 왜곡 방지
- 최적화가 쉬워지고 학습 초기에도 손실이 빠르게 줄어든다.

## 7. TCN의 장점
### 1) 병렬 처리 간으
   - RNN과 달리 순차 연산이 아니라 전체 시퀀스를 동시에 처리 -> 학습 속도가 향상됨
### 2) 장기 의존성 학습 우수
   - Dilated Convolution을 통해 Receptive Field를 지수적으로 확장 -> 먼 과거 정보도 반영 가능
### 3) 기울기 소실 완화
   - Residual Connection 으로 깊은 네트워크에서도 안정적 학습 가능
### 4) 출력 길이 = 입력 길이
   - 1D FCN 구조로 입력과 동일한 길이의 출력 생성 -> 시계열 예측에 직관적 적용가능

## 8. LTSF-Linear 등장배경
### 1) 기존 모델의 문제
   - LTSF 과제는 시간 순차성 보존이 핵심이며, 이는 추세, 주기성 패턴예측에 직접적 영향을 미침
   - Transformer는 위치 인코딩으로 순서를 표현하지만 이후 Multi-Head Self-Attention을 거치며 시간 정보가 일부 손실됨
   - NLP에서는 단어 순서가 일부 바뀌어도 의미가 유지되지만, 시게열 수치 데이터는 순서 손실이 큰 성능저하를 유발

### 2) LTSF-Linear 제안
- 단일 선형 레이어 기반으로 시간 순차성을 그대로 보존하며 장기 추세 주기성 특징을 단순하고 안정적으로 추출

## 9. Linear
<img width="464" height="280" alt="image" src="https://github.com/user-attachments/assets/af487256-192f-45c9-9348-6251f1b3f484" />

- 구조 : 가장 단순한 형태의 LTSF-Linear로 은닉층이나 활성함수 없이 입력 시계열을 하나의 완전 연결 선형레이어에 통과시켜 바로 출력 시계열 변환
- 각 미래 시점의 예측값이 모든 입력 시점 데이터의 선형 조합으로 계산
- 학습을 통해 얻어진 가중치들을 사용해 각 입력값에 가중치를 곱해 더함으로써 하나의 미래 예측값을 산출하는 방식
- 특징 : 단순한 선형 회귀 모델이지만 반복적인 예측 없이 한번에 미래를 내다보기 때문에 오차 누적이 없고 과거의 추세나 주기적 패턴을 가중치에 반영해 예측

## 10. DLinear
<img width="537" height="171" alt="image" src="https://github.com/user-attachments/assets/0e7fbaec-3e25-4cfa-8e0a-8a534b2f0d34" />

- 입력 시계열을 두 가지 구성요소로 분해하여 처리하는 모델
  1. 추세 : 전반적으로 길게 변하는 흐름 -> 이동 평균 필터를 사용해서 긴 흐름 (추세)를 뽑아냄
  2. 계절과 주기성 : 일정한 주기로 반복되는 패턴 -> 원래 시계열에서 이 추세를 제거하면 남는 건 주기적인 변동 (계절성)

### 모델 구조
  - 각 성분을 따로 예측
  1. Trend Linear Layer : 추세 성분만 입력 받아 미래 추세 예측
  2. Seasonal Linear Layer : 계절 성분만 입력 받아 미래 계절 패터 예측
  - 마지막에 두 결과를 합쳐서 최종 예측을 만듦
 
### 이유
- 일반 딥러닝 모델은 시계열의 복잡한 패턴을 한 번에 다 배우려다보니 비효율적이고 과적합 위험도 있음
- DLinear는 복잡한 걸 단순화 -> 추세는 추세대로, 계절성은 계절성대로 나눠서 선형 모델로 처리하니 훨씬 가볍고 안정적

## 11. LTSF-Linear 장점
1. 시간 순서 및 장기 패턴 보존
   - 원본 시계열의 순차 구조를 그대로 활용 -> 시간 정보 손실 없음
   - 추제 , 주기성 등 장기 패턴을 안정적으로 포착
   - 입력 길이가 길어져도 시간적 패턴 유지
2. 모델 구조의 단순성
   - 단 하나의 선형 계측, 비선형 활성화 함수 없음
   - 파라미터 수 적고 해석이 쉬움
3. 높은 연산 효율
   - 1~2번의 행렬 곱 연산으로 예측 가능 -> 계산 비뵹이 낮음
   - 메모리 사용량 적고 처리 속도 빠름
   - 긴시계열, 실시간 예측에도 유리함
  
# 전체 흐름 요약

- RNN → LSTM/GRU: 순차 데이터 학습 가능하지만 느리고 장기 의존성 한계.

- TCN: CNN 구조로 병렬 처리 및 장기 의존성 해결.

-ㅠTransformer 응용: NLP에서 강력했지만 시계열에서는 시간 정보 손실 문제.

- LTSF-Linear/DLinear: 단순 선형 접근으로 시간 순서 보존 + 추세/주기성 분리 → 효율적이고 안정적인 장기 시계열 예측 가능.
