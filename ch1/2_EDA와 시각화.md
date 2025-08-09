# 01. INTRODUCTION

## 1. 데이터 사이언스
데이터를 수집 및 처리하고 분석 → 유용한 정보 추출 -> 현실의 문제 해결  

<img width="459" height="263" alt="image" src="https://github.com/user-attachments/assets/1e235e66-da44-4772-8bfd-749c3aefd371" />


# 02. EDA(탐색적 데이터 분석) 소개

EDA : 데이터를 수집, 정제 후의 초기 데이터분석 단계

1. 잠재적 문제 발견
2. 데이터의 다양한 패턴 발견
3. 자료수집을 위한 기반 마련
4. 적절한 통계 도구 제시


## 1. EDA 대상
1. 일변량 : 변수 1개로 이루어진 데이터 → 데이터를 설명하고 패턴을 찾는 것이 목적  
   <img width="347" height="98" alt="image" src="https://github.com/user-attachments/assets/df52108f-e9f1-4316-8cd6-66a608b60689" />


2. 다변량 : 변수 여러 개로 이루어진 데이터 → 변수 간 관계 파악 목적  
   <img width="360" height="108" alt="image" src="https://github.com/user-attachments/assets/3db049db-59d2-48bd-a418-d0028af70105" />
)

## 2. EDA 종류
1. 시각화 : 차트나 그림을 이용해 데이터를 파악하는 방법
- 데이터를 한눈에 파악하고 대략적인 형태 파악

2. 비시각화 : 그래픽적인 요소를 사용하지 않고 주로 Summary Statistics (요약통계)사용
- 정확한 값을 파악하기에 좋음

## 3. EDA의 단계
1. 전체적 데이터 분석  
   - 분석 목적 정의  
   - 데이터 오류·누락 확인  
   - 분포 확인 및 이상 원인 분석  

2. 데이터 개별 속성값 관찰  
   - 전체 추세 파악  
   - 요약통계 지표 활용  
   - 시각화  

3. 속성 간 관계 분석  
   - 패턴 파악  
   - 그래프 시각화  
   - 상관계수 계산  

4. 이상치 및 결측치 탐지  
   - 결측치 확인  
   - 이상치 탐지 및 조치 계획  


## 4. 상관 분석
두 변수간의 선형적 관계를 측정하고 분석  
→ 변수 간 연관성 및 관계의 방향·강도 수치화

1. 피어슨 상관계수
- 공분산을 각 변수의 표준편차로 나누어 계산 → 범위 : -1 ~ 1
- 완전한 음의 상관관계 = -1
- 선형적 상관관계가 전혀없음 = 0
- 완전한 양의 상관관계 = 1
- 연속형 변수에 적합, 데이터가 정규분포를 따를 때 사용함
<img width="323" height="84" alt="image" src="https://github.com/user-attachments/assets/6ab38b3c-6523-43c5-8416-4477241214cc" />

2. 상관분석의 시각화
- corr() 메소드 사용

3. 1. 상관분석의 목적
- 두 변수의 관계파악
- 변수 간 상관 관계 있음


# 03. 이상치 및 결측치 처리

## 1. 이상치 탐지 방법

### 1) 시각적 방법
- 박스플롯, 산점도 그래프 활용  
  <img width="215" height="173" alt="image" src="https://github.com/user-attachments/assets/6f4d0077-9e23-4cd2-a8ac-853aa0561038" />

### 2) 통계적 방법
- Z-score 사용 : 데이터의 분포가 정규 분포를 이루는 경우 데이터의 표준 편차를 활용해 이상치를 탐지할 수 있음
- 데이터가 평균으로부터 얼마의 표준편차만큼 벗어나 있는지를 의미함.
- 보통 절댓값을 기준으로 3을 초과하면 이상치로 분류
 <img width="148" height="63" alt="image" src="https://github.com/user-attachments/assets/dea0c6cf-abcb-426b-8191-5bb84fc7a157" />

- IQR : Q3 - Q1 범위를 이용해 극단값 탐지 -> 정규분포를 이루지 않을 때 활용 가능
- MIN = Q1 - (1.5 × IQR)  
- MAX = Q3 + (1.5 × IQR)

MIN/MAX 값을 벗어나는 데이터의 경우 이상치로 간주


## 2. 이상치 처리 방법
1. 삭제 – 오류 데이터 제거  
2. 대체 – 다른 값으로 치환  
3. 변환 – 스케일링, 로그 변환 등  
4. 별도 처리 – 새로운 특징으로 활용  


## 3. 결측치 유형

결측치 : 데이터 수집 과정에서 특정 값이 누락되어 값이 비어있는 상태 = MISSING DATA

### 1) 완전 무작위 결측 (MCAR)
- 결측치가 다른 변수들과 상관관계가 없는 경우
### 2) 무작위 결측 (MAR)
- 특정 변수와 관련되어 누락 → 변수들의 상관관계를 알 수 없는 경우
### 3) 비무작위 결측 (NMAR)
- 누락된 변수 값이  누락된 이유와 관련이 있는 경우


## 4. 결측치 처리 방법
### 1) 삭제하기 : 결측치를 가진 행이나 열을 전체 삭제  

- 결측치가 데이터 전체에서 차지한ㄴ 비중이 작고 , 삭제해도 분석에 큰 영향을 주지않을 경우에 적합
- 데이터 손실이 발생할 수 있기 때문에 주의 필요

### 2. 대체하기 : 결측치를 다른 깨끗한 값으로 교체

- 단순 대체 : 평균, 중앙값, 최빈값으로 결측치를 대체
- 예측기반 대체 : 회귀 모델, 딥러닝 등을 사용하여 결측치를 예측한 후 대체
- 특수처리 : 새로운 범주를 추가해 결측치를 처리 / 결측치를 ‘unkown’또는 별도의 카테고리로 처리  

# 04. FEATURE ENGINEERING

FEATURE ENGNEERING : 모델의 성능을 높이기 위해서 원본 데이터를 가공하거나 새로운 변수를 생성하는 과정

**핵심 메소드**
1. groupby – 그룹별 통계 계산  
   <img width="330" height="191" alt="image" src="https://github.com/user-attachments/assets/04feab38-af26-42a1-97ab-4700d8834386" />

2. pivot_table – 데이터 피벗 구조 변환  
   <img width="552" height="232" alt="image" src="https://github.com/user-attachments/assets/c9d2c4a1-d7dc-4683-8473-bfb214b54c60" />

   <img width="215" height="173" alt="image" src="https://github.com/user-attachments/assets/9315a428-76cb-4ab7-9f9e-037fb9d6a6d9" />

