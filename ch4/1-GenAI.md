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

### 3) Curse of Dimensionality (차원의 저주)
<img width="446" height="420" alt="image" src="https://github.com/user-attachments/assets/c75d8fc1-deb2-4aa4-91bb-a603d91095bb" />

: 데이터 차원이 높아질수록 공간이 기하급수적으로 커짐 -> 같은 밀도를 유지하려면 필요한 데이터 양도 기하급수적으로 증가함

#### 문제점 
- 데이터가 희소해지고 거리 기반 알고리즘이 무의미해짐

### 4) Manifold hypothesis (매니폴드 가설)

#### 가설 : 고차원 데이터는 실제로는 저차원 매니폴드 위에 놓여 있다
- 고차원 공간에서 데이터는 희소해 보이지만
- 저차원 매니폴드로 사상하면 의미 있는 구조가 밀집됨 01. Generative Model

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

### 3) Curse of Dimensionality (차원의 저주)
<img width="446" height="420" alt="image" src="https://github.com/user-attachments/assets/c75d8fc1-deb2-4aa4-91bb-a603d91095bb" />

: 데이터 차원이 높아질수록 공간이 기하급수적으로 커짐 -> 같은 밀도를 유지하려면 필요한 데이터 양도 기하급수적으로 증가함

#### 문제점 
- 데이터가 희소해지고 거리 기반 알고리즘이 무의미해짐

### 4) Manifold hypothesis (매니폴드 가설)
<img width="606" height="223" alt="image" src="https://github.com/user-attachments/assets/c10aed18-0feb-4ee0-b361-4b7a86d0fb9a" />

#### 가설 : 고차원 데이터는 실제로는 저차원 매니폴드 위에 놓여 있다
- 고차원 공간에서 데이터는 희소해 보이지만
- 저차원 매니폴드로 사상하면 의미 있는 구조가 밀집됨

#### 의미
- 데이터 분석과 학습을 효율저긍로 하기 위해서는 저차원 매니폴드 구조를 학습해야함
- Ex. 얼굴 이미지 -> 수천 차원 픽셀 공간이지만 실제로는 표정, 각도, 조명 같은 몇 개 요인으로 설명가능

### 5) Discovering most important features (매니폴드 위에서 중요한 특징을 발견하는 과정)
<img width="789" height="312" alt="image" src="https://github.com/user-attachments/assets/6f807752-157a-4f0f-8573-8a244647534b" />

1. 핵심 아이디어
- 고차원 데이터 표현 : 데이터가 매니폴드 위에 잘 표현되면 그 안에서 데이터의 핵심 특징을 뽑아낼 수 있음
- 좌표 조정 : 매니폴드 공간에서 좌표를 조금씩 움직이면 원본 데이터ㅗㄷ 그에 맞게 자연스럽게 변형됨

2. 그림 설명
- 왼쪽 그림 : 매니폴드 위의 좌표를 이동하면 회전, 두께 변화 같은 의미 있는 특징 변화가 생김
- 오른쪽 그림
  - InfoGAN  latent variable 을 조정하면 글자두께, 회전같은 중요한 특징이 바뀜
  - VAE : latent spsace에서 축 하나를 바꾸면 숫자 크기가 자연스럽게 달라짐

3. 의미
- 매니폴드 학습을 통해서 데이터의 본질적 특징을 찾아낼 수 있음
- 이는 단순한 차원 축소를 넘어, 데이터 생성, 변환, 해석에도 활용됨
- GenAI 모델들이 잠재 차원에서 스타일 변환, 속성 조정 등을 할 수 있는 기반이 바로 이 개념
  
### 6) Reasonable Distance Metric

1. 아이디어
- 고차원 공간에서는 같은 유클리드 거리라도 실제 데이터의 의미적 차이를 잘 반영하지 못한다.
- 따라서 단순히 좌표 차이를 계산한 유클리드 거리는 데이터 의미와 동떨어질 수 있음
  -> 의미가 없는 거리
- 해결책 : 데이터를 매니폴드 위에 올려서 구부러진 실제 구조를 따라가는 거리를 써야함

2. 그림 해석
<img width="515" height="194" alt="image" src="https://github.com/user-attachments/assets/5b934245-288b-4f82-84b8-e65908925116" />

- 나선 구조
  - 두 점 A, B는 고차원 유클리드 공간에서는 가까워 보이지만 실제 매니폴드 위에서는 멀리 떨어져 있음
    -> 단순 유클리드 거리 대신 매니폴드의 구조를 따라간 거리가 합리적임
- 골프 자세 예시
  <img width="490" height="267" alt="image" src="https://github.com/user-attachments/assets/1ca5e2a1-1246-424c-8bc7-6754cde8b947" />

  - Interpolation in high dimension : 픽셀 공간에서 단순 보간 -> 중간 이미지가 부자연스러움
 
  <img width="516" height="273" alt="image" src="https://github.com/user-attachments/assets/61e706c8-7211-47b6-8dcd-cc21e410652a" />

  - Interpolation in manifold : 매니폴드 위에서 보간 -> 자연스러운 동작 변화

3. 의미
- 데이터 간 거리 측정은 매니폴드 기반이어야 의미가 있다
  - 고차원에서의 직선 거리는 실제 의미 반영 못함
  - 매니폴드 상의 거리는 데이터의 본질적 차이를 반영함

 # 04. VAE

 ## 1. Autoencoder

 ### 1) Dimensionality Reduction (차원축소)
 - Linear (선형기법)
   - PCA
   - LDA
  - Non-Linear (비선형 기법)
    - Autoencoders
    - t-SNE
    - Isomap
    - LLE
    - -> 복잡하고 곡선적인 매니폴드 구조를 반영
  > Auroencoder는 이 중 비선형 차원 축소 기법으로 분류됨

### 2) Aurodencoder 개념
- 입력 데이터를 압축(Encoding)했다가 다시 복원(Decoding)하는 신경망구조
- 데이터를 단순하게 복사하는 게 아니라 압축/복원 과정에서 중욯나 특징을 학습

### 3) 그림 설명
<img width="302" height="248" alt="image" src="https://github.com/user-attachments/assets/2ce1a23c-bd8a-4a24-9fb5-d9f75aff071a" />

<img width="323" height="355" alt="image" src="https://github.com/user-attachments/assets/a61458b1-11fc-49fe-b5b8-6073bc74f16c" />

- Input -> Bottleneck Layer -> output
- Encoding : 입력 데이터를 작은 latent vector z로 압축
- Decoding : z를 다시 원래 데이터 형태로 복원
- Bottleneck(병목 현상)이 있기 때문에 모델은 데이터의 핵심 특징만 남기고 불필요한 부분은 버리도록 학습함

#### Bottleneck : 병목현상
- 전체 네트워크를 통과 할 수 있는 정보의 양을 제한하여 입력 데이터의 학습된 압축을 이끌어 내는 역할

### 4) 의미
- 오토인코더는 단순 차원 축소 도구보다 더 복잡한 데이터 분포 (비선형 구조)를 잘 표현할 수 있음
- 데이터 전처리, 노이즈 제거, 특징 추출, 생성 모델 기반으로 자주 활용됨

### 5) 구조
<img width="334" height="357" alt="image" src="https://github.com/user-attachments/assets/d983f0a2-3829-4789-a323-49bb458181f9" />

- x -> Encoder h() -> 잠재 표현 z -> Decoder g() -> 출력 y
- 목적 : 입력과 출력이 최대한 비슷하도록
- 손실함수
<img width="206" height="77" alt="image" src="https://github.com/user-attachments/assets/5de89ab2-89d5-4bae-a55d-37caaa6aea7f" />

-> 입력과 복원된 출력 간의 차이를 최소화하도록 학습

### 6) Encoder 관점
- 역할 : 입력 데이터를 최소한의 정보로 압축
- Training DB의 패턴을 학습해서 중요한 특징만 latent vector z에 담음

### 7) Decoder 관점
- 역할 : Encoder가 만든 잠재 벡터 z를 받아서 손실을 최소화하는 방향으로 원래 데이터 복원
- 압축된 표현을 다시 펼처서 가능한 한 원래와 유사한 데이터를 만듦

### 8) AE(Autoencoder)
- 입력 데이터를 압축 -> 다시 복원 (매니폴드 러닝)
- 구조 : Encoder -> Decoder
- 특징 : 단순히 입력 x를 자기 자신으로 복원하는 것이 목표 -> 데이터 압축 및 특징 학습에 초점

### 9) VAE (Variational Autoencoder)
- 데이터의 생성
- Decoder(출력 생성)을 잘 학습시키기 위해 Encoder에서 분포를 학습
- Encoder가 단일 벡터를 내는 게 아니라 평균 벡터 + 분산 벡터를 출력 -> 잠재 공간을 분포로 모델링
- Decoder는 이 분포에서 샘플링한 z로부터 데이터를 생성

### 10) AE vs VAE 핵심 차이
- AE : 단순 압축/복원
