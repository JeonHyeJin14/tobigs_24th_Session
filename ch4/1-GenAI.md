# 01. Generative Model

## 1. 정의 
<img width="376" height="393" alt="image" src="https://github.com/user-attachments/assets/7ac45c3e-2a95-490d-96c9-e49a93873611" />

- 데이터를 단순하게 분류/회귀 하는 것이 아니라 데이터 분포를 학습해서 새로운 샘플을 생성할 수 있는 모델

## 2. Discriminative vs Generative
<img width="536" height="322" alt="image" src="https://github.com/user-attachments/assets/a216fb60-03e7-4dd8-9fd3-b0df7a80285c" />

- Discriminative model : 주어진 입력 x에 대해 라벨 y를 예측한다
- Generative model : 입력 데이터 자체의 분포를 모델링

# 02. Pixel RNN, Pixel CNN

## 1. 배경 
- 이미지를 만들 때 한 번에 전체 그림을 생성하는 대신에 픽셀 하나하나 순서대로 예측하면서 생성
<img width="353" height="98" alt="image" src="https://github.com/user-attachments/assets/31fe1389-dc29-4e3e-8054-df301ac0fe00" />

- 각 픽셀을 조건부 확률로 모델링 -> 이전 픽셀들을 기반으로 현재 픽셀의 분포를 모델링
  
## 2. Pixel RNN
<img width="262" height="249" alt="image" src="https://github.com/user-attachments/assets/fb862409-b1a9-419b-8914-f711bc0b2277" />

- RNN/LSTM 으로 구현
- 픽셀을 한 줄씩, 순서대로 에측하기 때문에 정확하지만 속도가 너무 느리다는 단점 존재

## 3. Pixel FNN
<img width="293" height="226" alt="image" src="https://github.com/user-attachments/assets/c07411fd-653d-460b-ab60-05ef82107f05" />

- CNN 기반 접근 -> 병렬 연산 가능
- Masked Convolution 기법 사용 -> 현재 픽셀이 미래 픽셀을 보지 않도록 제한


  #### Mascked Convolution : 필터가 참조하는 픽셀 중 현재 픽셀 이후의 정보는 가려서 접근할 수 없게 만든다.
  - 일반 Convolution의 문제 : 합성곱은 한 번에 커널을 적용하면서 양 옆과 위아래 픽셀을 전부 참조
      - 하지만 PixelCNN에서 아직 생성되지 않은 오른쪽이나 아래쪽 픽셀은 미래 정보에 해당됨,
        만약 이 정보를 그대로 쓰면 모델이 정답을 미리 엿본 셈이 되어서 Autoregressive특성이 깨지고 학습이 부정확

  - 해결책: 합성곱 커널에 마스크를 씌워서 미래 픽셀은 보지 못하게 함
    -> 오직 과거 정보만 사용해 현재 픽셀을 예측 할 수 있음
    -> PixelCNN이 처음에 설정한 Autoregressive구조 (픽셀을 순차적으로 생성)는 유지됨


  ## 4. 장점과 한계점
  ### 장점
  - 이미지 분포를 아주 정밀하게 학습할 수 있음
  - likelihood 계산 가능 -> 확률적으로 얼마나 그럴듯한 이미지인지 평가 가능

  ### 한계
  - 여전히 샘플링 속도가 느림 -> 픽셀 단위로 하나하나 생성해야 하기 때문
  - 멀리 떨어진 픽셀 간의 관계를 반영하기 어려움 -> 실제 응용에는 비효율적
 
  # 03. MANIFOLD

  ## 1. 정의
  <img width="527" height="306" alt="image" src="https://github.com/user-attachments/assets/55a4aa1e-e803-43a4-a92a-70950065d47e" />

- 데이터는 고차원 공간에 뿌려져 있지만 사실상 그 안의 저차원 곡면(매니폴드) 위에 놓여있음
- 즉, 실제 데이터는 전체 공간에 아무렇게나 퍼져 있는 게 아니라 특정 구조를 따라 존재한다는 가정

## 2. Manifold Learning 활용

### 1) Data Cmopression (데이터 압축)
- 고차원 데이터를 저차원 매니폴드에 매핑해서 불필요한 차원을 줄임

### 2) Data Visualization
- 고차원 데이터를 2D/3D 매니폴드로 줄여서 사람이 직관적으로 볼 수 있게 함
- 예 : t-SNE, UMAP

### 3) Curse of Dimensionality 극복
