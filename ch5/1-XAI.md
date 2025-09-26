# 01. What's XAI?
: 인간이 딥러닝 모델의 의사결정 과정을이해하고 신뢰할 있도록 하는 설명 가능한 인공지능 기술
- 인공지능이 왜 그런 결정을 내렸는지, 그 이유와 근거를 사람이 이해할 수 있도록 설명해주는 기술

## 1. INterpretability (해석 가능성)
- 모델 자체의 동작 방식을 이해하는 것을 의미함
 <img width="571" height="237" alt="image" src="https://github.com/user-attachments/assets/6132d09f-dbe7-42c2-bda6-7a90dee81fd2" />

- 선형 회귀처럼 전통적인 머신러닝 모델은 구조가 단순해서 해석하기 쉽지만 딥러닝 모델은 구조가 복잡해 해석하기 어려움
<img width="388" height="233" alt="image" src="https://github.com/user-attachments/assets/1982fbc9-0de5-4628-b1d9-4c6e26383a64" />

## 2. Explanation (설명)
- 모델이 내놓은 결과에 대한 이유를 설명하는 것
- XAI 방법론들은 이 설명을 제공하는 데 중점을 둔다.

# 02. Why XAI is important ?

## 1. AI Black Box Problem
: 인공지능 모델이 어떤 입력을 받아서 어떻게 처리해서 출력을 내놓는지 그 과정을 알 수 없는 현상
- 복잡한 딥러닝 모델은 수많은 계층과 복잡한 연결망으로 이루어져 있어서, 블랙박스처럼 그 내부에서 무슨 일이 일어나는지 이해하기가 매우 어려움
- 모델에 데이터를 넣고 결과만 볼 수 있을 뿐 어떻게? 그런 결과가 나왔는지 그 이유를 명확히 알기 힘들다.

### 문제점
1. 신뢰성부족 : 의료 진단이나 자율주행차처럼 중요한 분야에서 AI가 잘못된 결정을 내렸을 때 그 원인을 파악하고 수정하기 어려움
2. 공정성 문제 : AI가 특정 인종이나 성별에 대해 차별적인 겨로가를 내놓았을 때 , 왜 그런 편향이 생겼는지 알 수 없어서 해결이 힘들다
3. 법적 책임 소재 : AI 시스템에 의해 사고가 발생했을 경우, 그 책임이 누구에게 있는지 따지기가 애매해짐

### XAI 중요성
1. 투명성 향상
   - AI가 어떻게 결정을 내렸는지 그 과정을 투명하게 공개하면, 모델을 더 깊이 이해하고 신뢰할 수 있게 됨
   - 의료나 금융처럼 삶에 직접적인 영향을 미치는 분야에서는 투명성이 필수적
  
2. AI 성능 향상
   - XAI는 단순히 결과를 설명하는 데 그치지 않음. 모델이 왜 틀린 결정을 내렸는지 그 원인을 파악할 수 있게 해줌
3. 실제 적용
   - 예를 들어서 규제 당국이 AI 시스템의 법규 준수 여부를 평가할 때 XAI를 통해 모델의 작동 방식을 확인하고 검증할 수 있음

### XAI의 작동방식
<img width="686" height="177" alt="image" src="https://github.com/user-attachments/assets/96bd8df9-7191-400a-ae0e-0f4960cc8664" />

#### 이 이미지는 강아지가 기타를 치는 사진을 인공지능이 분석한 결과

a 원본이미지 : 기타를 치는 강아지 사진이 있음

AI 모델은 이 사진을 보고 가장 가능성이 높은 세 가지 항목을 예측함
1. 일렉트릭 기타 = 32%의 확률
2. 어쿠스틱 기타 = 24%의 확률
3. 래브라도 = 21%의 확률

# 02.Taxonomies of XAI

## 1. Scope of explanation (설명의 범위) : Global vs Local

### 1) Global(모델 전체 관점)
: 모델이 전반적으로 어떤 규칙을 학습 했는지, 특징(변수)들이 평균적으로 예측에 어떻게 기여하는지 설명
- 장점 : 정책/감사/모델 거버넌스에 유용함, 전체 행동 이해
- 주의점 : 사호작용/비선형성이 강하면 단변수 시각화 (PDP)가 왜곡될 수 이씅ㅁ, 변수 상관이 있으면 해석에 주의해야함
- 활용 : 규제 보고, 모델 선택/튜닝 기준, 조직 내 설명 책임

### 2) Local(사례별 관점)
: 특정 입력 xi에 대해 왜 그런 예측이 나왔는지 설명함
- 장점: 사용자 피드백/오류 분석/개별 의사결정 근거 제공
- 노이즈/불안정성/기여도 합산의 의미에 민감함
- 활용 : 개별 대출 승인 사유, 의료 영상 판독 근거, 모델 디버깅

## 2. Methodology(방법론)

### 1) Gradient-based (기울기 기반)
: 예측이 입력 변화에 얼마나 민감한지 계산
- 장점 : 빠르고 딥러닝 모델에 적합함
- 단점 : 노이즈, 기준점 선택에 민감함

### 2) Perturvation-based (교란 기반)
: 입력을 가리거나 바꾸고 결과 변화를 측정함
- 장점 : 모델 불문, 직관적
- 단점 : 계산량이 많음 , 변수 상관에 민감함

## 3. Dependency (모델 의존성)

### 1) Model-agnostic (모델 무관)
: 입력과 출력만 있으면 적용 가능
- 장점 : 어떤 모델에도 사용 가능
- 단점 : 근사 오차, 계산 느림

### 2) Model-specific (모델 특화)
- 특정 모델 구조를 활용한 기법
- 장점 : 빠르고 정확함
- 단점 : 다른 모델에는 적용불가

## 4. Quick Guide (어떻게 선택할까?)
- 이미지 분류 (CNN) : Grad-CAM (로컬, Gradient) + SHAP (Global, Perturvation)
- 트리 모델 (GBM/XGBoost) : TreeSHAP(Model-specific, 빠르고 정확)
- 텍스트/Transformer : Integrated Gradients , Token-level SHAP
- 블랙박스 모델 : LIME, Kernel SHAP (Model-agnostic)

# 03.XAI methods

## 1. LIME (Local Interpretable Model-agnostic Explanations)

### 1) 아이디어
- 복잡한 모델의 개별 예측을 설명하는 방법
- 원래 모델 (f)는 블랙박스 -> 대신 단순한 해석 가능한 모델 (g)로 근사
- 데이터 포인트 주변을 샘플링해서 지역적으로 설명함

### 2) 목표
- 복잡한 결정 경계 대신에 단순한 선형 모델로 해석 가능하게 만들기
- ex )  '이 환자가 독감으로 분류된 이유는 기침 + 두통 - 피로없음 때문'

### 3) 방법
1. 관심 있는 데이터 포인트 주변에서 샘플 생성
2. 원래 모델 f로 예측
3. 근처 샘플일수록 높은 가중치 부여함
4. 단순한 모델 g를  학습 -> 설명 모델

### 4) 수식
<img width="399" height="73" alt="image" src="https://github.com/user-attachments/assets/7b8c0b70-6295-4b12-b51d-3663fce6b17d" />

- f : 원래 모델
- g : 해석 가능한 모델 (선형)
 - πx : x 주변 데이터에 가중치  
- Ω(g) : 너무 복잡해지지 않도록 규제

 -> 핵심 : 복잡성과 해석력은 Trade off

### 5) 장점 및 한계
장점

- 모델 불문
- 개별 예측을 직관적으로 설명함

한계점
- 지역적 근사라서 불안정할 수 있음
- 샘플링 방법에 따라서 설명이 달라질 수 있음

## 2. SHAP (SHapley Additive exPlanations)

### 1) 배경
- 여러 XAI 방법들 중에서 언제 어떤 걸 써야하는지 불명확함
- SHAP은 이를 게임이론 기반으로 정리한 통일된 접근법

### 2) 핵심 아이디어
1. Shapley Value (Game Theory)
<img width="594" height="132" alt="image" src="https://github.com/user-attachments/assets/c39f7285-3d4a-43f5-a777-5fd94e774c93" />

   - 각 특징이 예측에 얼마나 기여했는지를 공정하게 분배함
   - 모든 가능한 조합에서 해당 특징이 추가될 때의 기여도를 평균함

2. Additive Feature Attribution
<img width="626" height="119" alt="image" src="https://github.com/user-attachments/assets/bee6a8ca-16fa-43c9-98c7-f5ddc1755b8d" />

   - 최종 예측을 모든 특징 기여도의 합으로 표현
   - 단순하고 직관적인 선형 구조

### 3) 장점
- 일관성 : 모델이 특정 feature에 더 의존할수록 SHAP 값도 커짐
- 지역 + 전역 설명 가능 :
  - 개별 샘플 : 어떤 feature가 결과에 영향을 줬는지
  - 전체 데이터 : 전역적으로 중요한 feature는 무엇인지

### 4) 계산 복잡도
- 기본 Shapley 계산 -> 현실적으로 불가능함
- 근사 방법이 필요
 - **Kernel SHAP** (샘플링 기반)  
 - **Tree SHAP** (트리 모델에 최적화, 빠름)  
 - **Deep SHAP** (딥러닝 모델용)  

### 5) 시각화 예시
<img width="413" height="288" alt="image" src="https://github.com/user-attachments/assets/9e0c2855-602f-4ac6-913a-e28bfe4ae763" />

## 3.Grad-CAM (Gradient-weighted Class Activation Mapping)

### 1) 배경 (CAM)
- CAM (Class Activation Mapping) : CNN이 어떤 영역을 보고 분류했는지 시각화함
- 방식 : 마지막 Convolution Layer -> GAP -> FC ->Softmax
- 한계 : 특정 구조에서만 가능함 -> Object Detection 등에는 사용 어려움

### 2) Grad-CAM 아이디어
<img width="456" height="303" alt="image" src="https://github.com/user-attachments/assets/1a43aa6e-dc34-454d-9648-c647efac7ac6" />

- Gadient 활용 : 특정 클레스에 대한 예측 점수가 feature map에 얼마나 민감한지
- 마지막 Convolution Layer의 feature map + Gradient -> 가중치 맵 생성
- ReLU 적용해서 class-specific heatmap 생성

### 3) 핵심 수식
<img width="444" height="147" alt="image" src="https://github.com/user-attachments/assets/fb178c31-2a8f-4cae-b68f-21c33b7a1fec" />

### 4) 장점
- 어떤 CNN 구조에도 적용 가능 (CAM 보다 범용적)
- 분류, Detection, Captioning등 다양한 비전 task 지원
- class-specific 영역 시각화 가능

### 5) 한계점
- 해상도 낮음
- pixel-level 정확도 부족

## 4. TCAV (Testing with Concept Activation Vectors)
<img width="1004" height="487" alt="image" src="https://github.com/user-attachments/assets/2cd7a6ca-2cc9-4d5c-9d88-05d5bfa8869f" />

### 1) 아이디어
- TCAV는 모델이 사용자 정의 개념에 얼마나 의존하는지 측정하는 방법
- ex ) "줄무늬(stripes)" 또는 "색(color)" 개념이 이미지 분류 결과에 얼마나 영향을 미쳤는가?

### 2) 방법
1. Concept 데이터와 Random 데이터 준비
2. 모델의 중간 계층 (activation) 추출
3. 선형 분류기 (Linear model)을 학습 시켜서 개념 vs 가짜를 구분 -> Concept Activation Vector (CAV)얻음
4. CAV 방향과 클래스 예측 점수의 gradient 내적 -> 해당 개념이 예측에 기여했는지 측정

### 3) 수식
<img width="1090" height="551" alt="image" src="https://github.com/user-attachments/assets/3b6606ac-99b5-46f2-a023-dc46469b49d1" />

- TCAV 점수: 데이터 중 몇 %가 개념 v에 양의 기여를 받았는지 
- 해석 : "클래스 k를 예측할 때 개념 v가 얼마나 자주 긍정적 영향을 주는가?"

### 4) 장점
- 사용자 친화적 : 도메인 지식을 직접 반영이 가능하다
- 해석이 직관적임
- 전통적인 feature importance와 달리 고차원 개념 단위 설명 제공
