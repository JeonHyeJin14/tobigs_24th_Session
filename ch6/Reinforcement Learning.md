# 01. 강화학습
<img width="366" height="687" alt="image" src="https://github.com/user-attachments/assets/161c8837-3272-4766-8094-2be438f7cf75" />

- 에이전트 (행동 주체)가 어떤 환경에 놓여졌을 때, 에이전트는 환경의 상태를 관찰하고, 상태에 적합한 행동을 취함
-
- -> 환경의 상태가 변화하고 에이전트는 환경으로부터 보상을 받는 동시에 변화된 새로운 상태를 관찰하고, 다시 상태에 적합한 행동을 취함
-
- - 목표 : 에이전트가 얻은 보상의 총합을 극대화하는 행동 패턴을 익히는 것

## 1. 구성요소
1. 에이전트 : 문제 상황에서 학습 혹은 행동의 주체가 되는 시스템
2. 환경 : 에이전트가 상호작용하는 외부 세계
3. 상태 : 에이전트가 환경을 관찰한 결과
4. 행동 : 환경을 관찰한 에이전트의 선택
5. 보상 : 에이전트의 행동에 대한 피드백 혹은 평가 값
6. 정책 : 상태에 따른 에이전트의 행동 원리

# 02. 마르코프 결정 과정

## 1. 마르코프 결정 과정 (MDP)
- 현재 상태와 행동에 따라서 미래 상태와 보상이 결정되는 의사결정 과정
- 목표 : 에이전트가 보상을 최대화하는 최적 정책을 찾는 것
- 마르코프 성질 : 다음 상태는 오직 현재 상태와 행동에만 의존함

## 2. 구성 요소

### 1) 정책 : 에이전트가 행동을 결정하는 방식
<img width="363" height="640" alt="image" src="https://github.com/user-attachments/assets/83aea025-a061-4263-a256-cdc96da6fca1" />

- 결정적 정책 : 에이전트가 상태를 매개변수로 입력을 받을 경우 반드시 행동 a를 수행하는 정책
- 확률적 정책 : 에이전트가 상태를 매개변수로 입력 받을 경우 일정 확률로 행동 a를 수행하는 정책

### 2)  상태 전이 : 현재 상태에서 행동을 했을 때 다음 상태로 넘어가는 현상
<img width="385" height="711" alt="image" src="https://github.com/user-attachments/assets/5ee2faf6-cd14-4891-925d-5b5587fd8700" />

- 상태 전이 함수 : 상태와 행동을 입력하ㄴ면 다음 상태를 출력하는 함수
- 상태 전이 확률 : 상태와 행동 등 두 조건이 주어졌을 때 다음 상태로 전이될 확률

### 4) 보상 함수 : 특정 상태에서 행동 후 얻는 보상 값
<img width="379" height="686" alt="image" src="https://github.com/user-attachments/assets/f44dac2c-effc-40a0-a3d9-e8cf9475cc70" />

## 3. 개념
### 1) 수익 : 앞으로 받을 보상의 합
<img width="455" height="73" alt="image" src="https://github.com/user-attachments/assets/8e14509b-9bad-49a4-9481-de97e35a84cb" />

### 2) 할인율
- 지속적 과제에서 수익이 무한대가 되지 않도록 방지하는 가중치
- 가까운 미래의 보상을 더 중요하게 여기도록 유도하는 가중치
- 0에서 1 사이의 실수로 설정

<img width="538" height="406" alt="image" src="https://github.com/user-attachments/assets/effae43c-4d0c-470f-9a39-198a59af24d5" />

<img width="566" height="284" alt="image" src="https://github.com/user-attachments/assets/b7c7b088-ae02-4704-8a76-bfccabfd3ff7" />

### 3) 상태 가치 함수 : 상태 s에서 시작했을 때 얻을 수 있는 기대 보상
<img width="430" height="264" alt="image" src="https://github.com/user-attachments/assets/90e7da07-48ae-48b7-95bc-88239b671d5f" />

<img width="386" height="335" alt="image" src="https://github.com/user-attachments/assets/2aa3a5b9-8e33-42d3-9f46-ca3b08d6c04a" />

### 4) 최적 상태 가치 함수 : 가장 큰 보상을 주는 최적 정책에 따른 가치
- MDP에서는 최적 정책이 최소 하나는 존재함
- 최적 정책은 결정적 정책 = 각 상태에서의 행동이 유일하게 결정됨

## 4. 그리드 월드 (Grid World)
- 격자 안에서 에이전트가 움직이며 보상을 얻는 문제
- 사과 -> +1 보상, 폭탄 -> -1 보상
- 에이전트가 어떤 정책을 따라야 최종적으로 가장 많은 보상을 얻을 수 있는지 학습
- 정책 비교 : 여러 정책 중 가장 상태 가치 함수가 높은 정책이 최적의 정책

# 02. 벨만 방정식
: 상태 s의 상태 가치 함수와 다음에 취할 수 있는 상태의 상태 가치 함수의 관계를 나타내는 수식 -> 모든 상태와 모든 정책에 대해 성립함

## 1. 상태가치 함수에 대한 벨만 방정식
- V(s) = '지금 상태 s에서 시작해 앞으로 받을 즉시 보상 + (할인된) 미래 보상의 기댓값'
- 미래 보상은 한 번 앞을 내다보고 " 다음 상태의 가치 V(다음 상태)"로 묶어서 계산한다
-> 이것이 벨만 식의 핵심 아이디어 (자기참조/재귀)
\[
\boxed{\,V_\pi(s)=\sum_a \pi(a|s)\sum_{s'} p(s'|s,a)\,[\,r(s,a,s')+\gamma V_\pi(s')\,]\,}
\]

## 2. 행동 가치 함수에 대한 벨만 방정식
### 행동 가치 함수
<img width="423" height="338" alt="image" src="https://github.com/user-attachments/assets/4ea3224d-9b21-4f76-b699-384df6f0c892" />

- 시간 t일때 상태 s에서 행동 a를 취하고 시간 t+1부터는 정책에 따라 행동을 결정할 때 얻을 수 있는 기대수익
- 상태 가치 함수 + 행동 a(조건) = 행동 가치 함수
