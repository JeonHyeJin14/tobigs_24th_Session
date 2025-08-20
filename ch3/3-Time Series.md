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
- AR(자기회귀)와 MA(이동평균)
