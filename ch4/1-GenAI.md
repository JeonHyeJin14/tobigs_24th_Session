# 00. 서론

## 1. 추천 시스템 필요성
- 정보 과잉 문제 해결
- 사용자 경험 향상
- 기업의 서비스 매출증가

##2. 실생활 속 추천 시스템
- 사용자의 시청 및 청취 이력을 바탕으로 영화, 동영상, 음악 추천
- 사용자가 좋아할 만한 친구나 페이지 추천
- 고객의 구매 이력과 검색 이력을 바탕으로 제품 추천

# 01. 추천시스템 기본 개념

## 1. 추천시스템이란?
- 사용자가 관심을 가질만한 콘텐츠를 추천하는 기계학습의 한 방법으로 사용자의 선호도 및 과거 행동을 토대로 사용자의 관심과 흥미를 가질만한 콘텐츠를 제공하는 것

## 2. 문제 정의
### 1) Ranking Problem : 여러 아이템 중 어떤 순서로 제시해야 할지를 결정하는 문제
ex. 유튜브에서 동영상 추천 순서 결정 -> 사용자가 클릭할 확률이 높은 순으로 동영상 나열

### 2) Prediction Problem : 사용자가 특정 아이템에 대해서 어떤 선호도를 보일지 예측하는 문제
ex. 넷플릭스에서 사용자가 영화 A를 별점 1~5점 중 몇 점으로 평가할지 예측
-> 사용자가 이 영화에 4점 이상 줄 가능성이 높다

### 3) 데이터 유형
- 명시적 피드백 : 사용자가 선호도를 직접적으로 표현한 데이터 -> 평점, 좋아요/싫어요, 리뷰, 구독
  - 장점 : 사용자의 취향이 정확하게 반영됨
  - 단점 : 데이터 자체를 얻기가 어려움
 
- 암시적 피드백 : 사용자가 간접적으로 표현된 선호도, 취향을 나타내는 데이터 -> 사용자 행동 로그 데이터, 검색 기록, 클릭기록, 방문 페이지, 구매 내역
  - 장점 : 데이터 얻기가 쉬움
  - 단점 : 사용자의 선호도를 직접적으로 알기 어려움
 
# 02. 추천 시스템 평가지표

## 1. Precision and Recall
<img width="673" height="326" alt="image" src="https://github.com/user-attachments/assets/b6ea2813-dea0-476c-a07b-fb53c370bfec" />

- Precision@K : 내가 추천한 아이템 k개 중에 실제 사용자가 관심있는 아이템의 비율
- Recall@K : 사용자가 관심있는 모든 아이템 중에서 내가 추천한 아이템 K개가 얼마나 포함되는지 비율

<img width="1119" height="187" alt="image" src="https://github.com/user-attachments/assets/f6d02563-4f57-407a-8b5e-a4f0d481d2ba" />

- Precision@5 = 3/5 = 0.6
- Recall@5 = 3/6 = 0.5

> Precision과 Recall의 Trade-off : 모두 최댓값이 될수는 없음

<img width="637" height="138" alt="image" src="https://github.com/user-attachments/assets/caf7e2ba-e33b-4fc0-8308-66a250ca3373" />


##2. MAP 

### 1) AP : 순서대로 추천된 아이템을 보면서 사용자가 좋아하는 아이템이 나올 때마다 그때의 Precision값을 누적해서 평균 낸 값
<img width="545" height="68" alt="image" src="https://github.com/user-attachments/assets/1b08bd04-2105-4865-b11c-80a5729e668c" />

- m : 추천된 아이템 K개 중에 사용자가 실제로 좋아하는 아이템의 수
- i : 추천된 아이템 리스트의 순서 (랭킹)
- rel (i) : relevance를 나타내는 값 -> i 번째 아이템이 사용자가 좋아하는 아이템인지를 나타냄
  - 1이면 좋아하는 아이템, 0이면 좋아하지 않는 아이템
- Precision@i : i번째 아이템까지 고려했을 때의 Precision 값


### 2) MAP : 모든 사용자에 대해서 각각 AP@K의 값을 계산 한 수에 그 값들을 모두 더해서 사용자 수로 나눈 평균
<img width="428" height="58" alt="image" src="https://github.com/user-attachments/assets/318ab0a7-7e0f-4345-a3ef-5bf4a5856e98" />

- |U| : 전체 사용자의 수

> AP@K : 한 명의 사용자에 대한 추천 시스템의 순위별 정확도
> MAP@K : 모든 사용자에 대한 추천 시스템의 평균적인 순위별 정확도

<img width="925" height="418" alt="image" src="https://github.com/user-attachments/assets/281df498-763f-4464-9277-4cb0592399e6" />

### 3) NDCG 
<img width="855" height="176" alt="image" src="https://github.com/user-attachments/assets/00a66d6c-ddcc-40aa-a83c-0db441a17373" />

1. CG : 추천된 상위 K개의 아이템들에 대한 관련성 점수를 단순하게 모두 더한 값
  - 한계 : 추천 순서를 고려하지 않음 -> 추천 시스템에서는 관련성 높은 아이템이 앞쪽에 위치하는 것이 더 중요함

2. DCG : CG의 한계를 극복하기 위해서 순서에 따른 할인 개념을 도입한 것
  - 분모에 log2(i+1)항이 추가됨 -> 순서가 커질수록 관련성 점수에 곱해지는 가중치가 작아짐
  - 추천 순서의 중요성을 반영하고 있지만 추천 리스트의 길이나 추천 아이템의 총 관련성 값에 따라 점수가 달라지기 때문에 모델 간 절대적인 비교가 어렵다는 한계가 있음

<img width="1011" height="253" alt="image" src="https://github.com/user-attachments/assets/b1911eaa-7a74-4e58-8f03-b240bad8a2bf" />

3. NDCG : DCG의 한계를 보완하기 위해서 정규화를 거친 것 -> DCG 값을 가장 이상적인 추천 순서로 얻을 수 있는 IDCH로 나눈 값
   
   - IDCG는 추천 가능한 모든 아이템 중 가장 관련성 높은 아이템들을 K개 뽑아서 순서대로 나열했을 때의 DCG
   - NDCG는 항상 0~1의 값, 1에 가까울수록 이상적인 추천

<img width="736" height="505" alt="image" src="https://github.com/user-attachments/assets/8c7d1607-ff22-4ebb-ad9b-eed47f5e8687" />


## 4. MAE and RMSE 
<img width="591" height="237" alt="image" src="https://github.com/user-attachments/assets/fe3785b6-f3d5-4cb6-a23c-fdcde500793b" />

### 1) MAE : 정답 평점과 예측 평점 간의 절대 오차에 대해 평균 낸 것

<img width="421" height="57" alt="image" src="https://github.com/user-attachments/assets/16a061c5-17e8-4051-97f8-5e50de287946" />

- r_ui : 사용자가 아이템에 실제로 매긴 정답 평점
- hat_r_ui : 모델이 예측한 예측 평점
- hat_R : 예측된 평점의 총 개수
- 수식은 모든 예측에 대해 정답과 예측의 차이를 계산하고 이 차이들의 평균을 구함
- MAE는 직관적으로 이해하기쉬움 -> 예측 평점이 정답 평점과 평균적으로 얼마나 차이가 나는지 보여줌
- 모든 오차에 대해서 동일한 가중치를 부여하기 때문에 이상치의 영향을 적게 받음

### 2) RMSE : 오차 제곱의 평균을 내고 루트를 취함
<img width="479" height="78" alt="image" src="https://github.com/user-attachments/assets/502a0cc2-c6ef-42a8-b953-d62e1efad105" />

- MAE와 마찬가지로 r_ui는 정답 평점 , hat_r_ui는 예측평점
- RMSE는 오차를 제곱해서 합산한 후에 평균을 내고, 다시 제곱근을 취함
- RMSE는 큰 오차에 더 가중치를 부여하는 특징 -> 오차를 제곱하는 과정에서 1보다 큰 오차는 더 커지고, 1보다 작은 오차는 더 작아짐
  - 예측이 크게 벗어난 경우 RMSE 값이 급격하게 커지게됩 -> 예측 오류가 클 때 더 민감하게 반응해야 하는 경우에 유용함
 
  ### 3) MAE vs RMSE
  - MAE : 모든 오차를 동일하게 중요하게 취급 , 이상치에 덜 민감함
  - RMSE : 큰 오차에 더 큰 페널티 부여 , 이상치에 민감함
 

# 03. 추천시스템 주요기법

<img width="591" height="237" alt="image" src="https://github.com/user-attachments/assets/4f3e878d-1fbc-49fc-8d18-6802f797e8e2" />

## 1. 콘텐츠 기반 필터링 
: 사용자가 과거에 선호했던 아이템과 유사한 특징 (콘텐츠)를 가진 다른 아이템을 추천하는 방식
<img width="621" height="414" alt="image" src="https://github.com/user-attachments/assets/88d13e46-0d37-4a9b-8207-e07dc78a4b09" />

1. 사용자가 과거에 만족한 아이템 확인
2. 사용자가 좋아했던 아이템과 비슷한 아이템을 선정
3. 선정된 아이템을 사용자에게 추천함

- 과적합 문제 : 사용자가 특정 장르나 특징의 아이템만 계속 소비하게 되어서 다양한 아이템을 경험할 기회가 줄어들 수 있음
- 콜드 스타트 문제 : 새로운 사용자에게는 과거 이력이 없으므로 추천을 하기 어렵다는 한계

### 1) 콘텐츠 기반 필터링 구조
<img width="1147" height="489" alt="image" src="https://github.com/user-attachments/assets/e7d5be23-fcc8-4320-9391-aef7e5fea6e6" />

> 세 가지 핵심 컴포넌트

1. 콘텐츠 분석 : 비정형 데이터로부터 아이템의 특징을 추출하고 구조화하는 역할
  - 영화의 경우 제목, 장르, 출연 배우, 감독, 줄거리 등의 텍스트 데이터를 분석해 각 아이템을 고유한 특징 벡터로 변환함
  - 이 과정은 NLP기술이나 이미지 분석 기술을 활용해 이루어짐
2. 유저 프로파일 파악 : 사용자의 선호도를 학습해 유저 프로파일을 생성
  - 사용자가 과거에 긍정적인 반응을 보인 아이템들의 특징을 분석해 사용자의 취향을 일반화함
  - ex. 사용자가 액션 영화를 많이 보았다면 해당 사용자의 프로파일에는 액션 장르에 대한 선호도가 반영됨 -> 사용자의 취향을 나타내는 벡터로 표현 가능
3. 유사 아이템 선택 : 생성된 유저 프로파일과 유사한 아이템을 찾아내어서 추천 리스트를 만듦
  - 유저 프로파일 벡터와 콘텐츠 분석을 통해 만들어진 모든 아이템의 특징 벡터를 비교해 유사도 점수 계산
  - 코사인 유사도 같은 지표가 주로 사용됨
  - 이 점수를 기반으로 가장 유사한 아이템들을 순위별로 정렬 -> 최종 추천 리스트 생성

### 2) 콘텐츠 기반 필터링 장단점

> 장점
- 다른 유저의 데이터가 필요하지 않다
- 추천할 수 있는 아이템의 범위가 넓다
- 추천하는 콘텐츠에 대한 근거를 제시할 수 있다

> 단점
- 적절한 feature를 찾기가 어렵다
- 새로운 유저를 위한 추천이 어렵다
- 사용자가 이미 알고 있는 유사한 콘텐츠만 반복 추천 할 수 있다.

## 2. 협업 필터링
<img width="574" height="394" alt="image" src="https://github.com/user-attachments/assets/3ff2e6a2-5ce5-4c2c-bfea-951bd6945fec" />

: 많은 사용자로부터 수집한 구매 패턴이나 평점을 기반으로 해 다른 사용자에게 콘텐츠 추천하는 방식

1. 사용자 간 유사도 파악
  - A와 B가 공통으로 시청하거나 긍정적인 평가를 내린 아이템을 찾음
2. 유사 사용자의 취향 분석
  - 만약 사용자 A와 B가 공통 아이템에 대해서 비슷한 선호를 보였다면 서로 비슷한 취향을 가졌다고 판단
3. 아이템 추천
  - 사용자 B가 아직 시청하지 않은 아이템 중 사용자 A가 좋아했던 아이템을 사용자 B에게 추천

- 아이템 특징 불필요 : 콘텐츠 기반 필터링과 달리 아이템의 내용이나 특징을 분석하지 않고 오직 사용자의 행동 데이터만을 이용0함
- 콜드 스타트 문제 : 새로운 사용자나 새로운 아이템에 대한 데이터가 부족할 때 추천이 어렵다는 한계

## 3. 기억 기반 필터링
<img width="871" height="443" alt="image" src="https://github.com/user-attachments/assets/1f294961-be48-482c-821e-a41de56c6325" />

종류 : 사용자 기반 협업 필터링, 아이템 기반 협업 필터링


## 4. 유사도
<img width="923" height="409" alt="image" src="https://github.com/user-attachments/assets/83accb5d-b71d-480f-b07d-9d66e2c911c7" />

- 자카드 유사도 : 두 아이템 집합의 공통 항목 비율로 유사도 측정
- 코사인 유사도 : 두 아이템 벡터의 각도를 이용해 방향이 얼마나 비슷한지 측정
- 유클리디안 거리 : 두 아이템 벡터 간의 직선 거리 측정
- 피어슨 상관계수 : 두 아이템에 대한 평점 경향의 상관관계 측정

## 5. 코사인 유사도
<img width="764" height="145" alt="image" src="https://github.com/user-attachments/assets/ece6281b-b49c-4f09-b8fd-015bbe4d4d3f" />

: 평점들을 벡터로 생각하고 2개의 각 벡터사이의 각도를 유사도라고 가정하는 방법

<img width="1077" height="202" alt="image" src="https://github.com/user-attachments/assets/2242deea-f6f9-44dc-93be-0e5a9b340216" />

1. 비슷한 아이템 찾기
   - 평점을 준 아이템 A와 다른 사람들이 평점을 준 아이템 B의 평점 패턴을 비교
   - 만약 아이템 A와 B를 모두 좋아한 사람들이 많다면 두 아이템은 비슷한 아이템이라고 판단
2. 평점 예측하기
   - 아직 보지 않은 아이템C에 대한 평점 예측
   - 아이템 C와 비슷한 다른 아이템들에 준 평점을 가져옴
   - 비슷한 정도 (유사도)를 가중치로 사용해서 아이템 C의 예상 평점 계산
3. 추천하기
   - 모든 아이템에 대한 예상 평점 계산
   - 예상 평점이 가장 높은 아이템을 추천함
  

 ## 5. 모델 기반 협업 필터링
 : 사용자-아이템 상호작용 데이터를 학습해서 잠재 요인을 추출하고 이를 이용해 새로운 평점 예측

 <img width="466" height="354" alt="image" src="https://github.com/user-attachments/assets/ff7afd81-5169-475b-97e4-f52424817b88" />

1. Latent Factor Model (잠재요인 모델)
: 사용자와 아이템의 특성을 잠재적인 차원으로 나타낼 수 있다고 가정

- 잠재요인 공간 : 이미지의 2차원 그래프처럼 사용자와 아이템을 특정 축에 따라 위치시킴
  - 예를 들어, X축은 '진지함(Serious) vs. 가벼움(Escapist)', Y축은 '남성 취향(Gleared toward males) vs. 여성 취향(Gleared toward females)'과 같은 잠재적인 특성을
- 작동 원리 : 이 공간에서 가까운 위치에 있는 사용자 - 아이템 쌍은 서로 취향이 일치한다고 본다.
  - 예를 들어, 'Braveheart'와 'Amadeus'는 진지한 영화이고, 'Dumb and Dumber'는 가벼운 코미디 영화이다.

2. 분류/회귀 방식 (Classification/Regression)
:  주어진 입력 x에 대해서 출력 y를 예측하는 일반적인 머신러닝 모델의 구조를 따른다.

-> 추천 시스템에서는 사용자와 아이템 정보를 입력받아서 사용자가 아이템에 매길 평점 예측하는데 사용됨

3. 최신 융합 모델 방식
: 두 가지 방식을 결합하거나 발전시킨 모델들 등장
  - Factorization Machine : 잠재 요인 모델과 분류/회귀 방식의 특징을 모두 가진 모델로, 여러 특징 간의 상호작용을 효과적으로 모델링 함
  - Neural Collaborative Filtering (NFC): 딥러닝을 활용해서 복잡한 사용자 - 아이템 상호작용을 모델링함으로써 기존의 잠재요인 모델을 확장한 방식
  - -> 사용자와 아이템 간의 복잡한 비선형 관계를 학습하는데 강력함

## 6. 행렬분해

<img width="731" height="314" alt="image" src="https://github.com/user-attachments/assets/cc258065-9ebe-43bd-bce4-7bea5b215e76" />


<img width="1212" height="456" alt="image" src="https://github.com/user-attachments/assets/f3f1d89d-594c-4ce9-b6f1-b9fef71fac76" />


<img width="1209" height="475" alt="image" src="https://github.com/user-attachments/assets/c4bd382a-4327-438f-8033-8179a69a4b17" />


>SVD : 어떤 행렬 A를 세 개의 행렬로 분해함 = 특이값 분해
>A : 원래 행렬 -> ex. 행은 사용자, 열은 아이템, 행렬의 값은 사용자가 아이템에 매긴 평점
>U : A 행렬의 열 공간에 대한 정규 직교 기저를 이루는 행렬 -> ex. 사용자의 잠재 요인을 나타낸다고 생각할 수 있음
> Σ 시그마 : 대각선에만 0이 아닌 값이 있는 직사각형 대각 행렬 . 대각선에 있는 값들은 특이값이라고 불리며 행렬 A의 중요한 정보를 담고 있음
  -> 이 값들이 클수록 해당 잠재 요인이 중요한 의미를 갖는다는 뜻
> V의 전치행렬 : A 행렬의 행 공간에 대한 정규 직교 ㄱ지ㅓ를 이루는 행렬의 전치이다. 아이템의 잠재 요인을 나타낸다고 볼 수 있음. 각 행 벡터는 right-singular vectors라고 불린다.
