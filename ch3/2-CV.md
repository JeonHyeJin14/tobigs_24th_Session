# 01. CNN의 발전과정

## 1. LeNet-5
- 딥러닝 기반 CNN 구조의 시초
- MNIST 같은 간단한 데이터 셋에 최적화된 모델

### 1) 전통적 방식과 LeNet - 5
<img width="653" height="274" alt="image" src="https://github.com/user-attachments/assets/59acad35-d7f4-4463-a55a-cb5383f9c6e1" />

- 전통적 이미지 분류 방식
  - Hand-crafted feature extraction (사람이 직접 특징 설계)
  - Fully-connected layer 사용 시 파라미터 수 과다
  - 입력의 공간적 구조를 무시함

- LeNet - 5
  - Convolution layer : 자동으로 중요한 특징 추출
  - Pooling : 위치 변화에 강건, 연산량 감소
  - Weight Sharing : 하나의 필터를 이미지 전체에 적용 -> 파라미터 절감
  - Local Receptive Field : 인접한 픽셀 정보만 활용 -> 공간 구조 고려한 학습

### 2) LeNet-5 구조
<img width="394" height="253" alt="image" src="https://github.com/user-attachments/assets/8f409ddd-8526-4ab1-ba5a-7ef0a9bf26a9" />

1. 입력 : 32*32 흑백 이미지
2. C1 : 첫 번째 합성곱 (Convolution)
   - 커널 크기 : 5*5, 스트라이드1
   - 출력 크기 : 28*28*6 (6개의 특성 맵)
   - 특징 : 지역 수용야, weight sharing 적용
   - 활성화 함수 : tanh
3. S2 : 첫 번째 서브 샘플링
   - 풀링 크기 : 2*2, 스트라이드2
   - 출력 크기 : 14*14*6
   - 평균 풀링 + 학습 가능한 가중치와 바이어스 적용
   - 비선형 활성화 (tanh) 포함
4. C3 : 두 번째 합성곱
   - 커널 크기 : 5*5
   - 출력 크기 : 10*10*16 (16개의 특징맵)
   - 특징 : 이전 6개 맵과 부분 연결을 적용 ->파라미터 수 감소
5. S4 : 두 번째 서브샘플링
   - 풀링 크기 : 2*2, 스트라이드 2
   - 출력 크기 : 5*5*16
6. C4 : 세 번째 합성곱 (사실상 완전 연결)
   - 커널 크기 : 5*5, 입력 전체를 덮음
   - 출력 크기 : 1*1*120
   - 사실상 Fully-connected layer 와 동일하게 동작됨
7. F6 : 완전 연결 계층
   - 출력 노드 수 : 84
   - 활성화 : tanh
8. 출력
   - 클래스 수 : 10
  
> 서브샘플링 : 특징 맵을 작게 줄여주면서 위치 변화에 강건하게 만드는 과정이고, LeNet-5에서는 Average Pooling + 학습 가중치 형태로 구현됐습니다.

## 2. AlexNet
<img width="421" height="259" alt="image" src="https://github.com/user-attachments/assets/09359a10-d7db-4e0a-b2be-0c27e85ec7a3" />

- LeNet보다 규모가 훨씬 크고 깊은 구조
- ImagNet 같은 대규모 데이터 셋에 최적화된 모델
- 특징
1. 대규모 & 깊은 구조
  - LeNeta보다 훨씬 크고 깊은 네트워크
  - - 224*224*3 이미지 입력을 처리할 수 있도록 설계

2. 병렬 GPU 활용
   - Conv layer와 FC layer를 2개의 GPU에 분산 -> 학습 속도 크게 향상
    
3. ReLU 활성화 함수
   - 기존 tanh, sigmoid 대신 ReLU 사용 -> 기울기 소실 문제 완화 + 학습 속도 증가

- sigmoid : 출력이 (0,1) 구간 -> 입력이 크거나 작을 때 기울기가 0에 가까워짐
- tanh : 출력이 (-1,1) 구간, 중심화 되어서 sigmoid 보다 낫지만 입력이 커지면 역시 포화영역-> 기울기는 0에 가까워짐
- 문제점 : 깊은 네트워크에서는 역전파 중 연속적으로 0.1~0.01 같은 작은 값들이 곱해져서 기울기가 소실됨

> ReLU
- x>0인 영역에서 기울기 = 1 → 기울기 소실 문제 완화.
- 계산이 단순 (max(0,x)): 지수 연산(sigmoid, tanh)보다 훨씬 빠름 
- 양수 영역에서는 선형적이어서 gradient가 잘 전달됨.
- 단점 : 음수 입력에서는 항상 0
  
4. 과적합 방지
- Dropout : Fully connected layer에서 무작위로 뉴런을 끔 + 일반화 성능 향상
- Data Augmentation : 이미지 뒤집기, 크롭 등으로 학습 데이터 다양화

5.LRN
- 인접 뉴런의 출력을 정규화하여 일반화 성능 향상
- 현재는 BatchNorm, LayerNorm 등이 더 많이 사용됨


## 3. VGGNet
<img width="401" height="269" alt="image" src="https://github.com/user-attachments/assets/1a212e7b-f515-4fb3-a492-af123c368adc" />

### 핵심 아이디어
1. Small Filters (3*3)
   - 모든 합성곱을 작은 3*3 필터로 통일함
   - stride=1, padding=1을 사용해 출력 크기 유지
   - 여러개의 3*3 conv를 쌓으면 큰 receptive field 효과를 얻으면서도 파라미터 감소
     예: 7×7 conv 1개 ≈ 3×3 conv 3개 (더 많은 비선형성, 더 적은 파라미터)

3. Deeper Network
   - AlexNet (8-layer)보다 훨씬 깊음
   - 깊이를 늘려서 성능을 향상시킴
       
3. 파라미터 효율성
   - 통일 receptive field에 더 적은 파라미터를 사용함
   > receptive field : fillter가 한 번에 볼 수 있는 입력의 공간 영역
    
4. 반복적인 ReLU : 비선형성 강화, 표현력 증대

## 4. GoogLeNet
<img width="633" height="187" alt="image" src="https://github.com/user-attachments/assets/b0b557b5-9e51-4002-b078-1f49e2ea2048" />

- Inception module 이라는 서브 네트워크를 연속적으로 이어서 구성
- 큰 사이즈의 커널이 제공하는 장점은 수용하며 weight parameter수를 줄일 수 있는 네트워크

1. Inception module
   - 1×1, 3×3, 5×5 합성곱(conv) + 3×3 풀링(pooling)을 동시에 수행 -> 비선형성
   - 다양한 크기의 필터를 써서 여러 스케일의 특징을 한 번에 뽑아냄
2. 1×1 Convolution의 활용
   - 채널 수 줄이기 (차원 축소) -> 연산량과 파라미터 수 크게 감소
   - 채널 간 정보도 섞어주므로 표현력 증가
3. Global Average Pooling
   - 마지막에 완전 연결 layer대신 평균 풀링 사용
   - 파라미터 수 줄고, 과적합 위험 감소

## 5.Degradation
<img width="555" height="198" alt="image" src="https://github.com/user-attachments/assets/85219ad1-114f-4573-85de-89dd1207aed0" />

- VGGNet, GooLeNet 이후 더 깊은 네트워크에 대해 연구가 증가했지만 네트워크가 깊어질수록 성능이 저하됨
- 네트워크가 깊어질수록 vanishing gradient 문제가 발생해 제대로 최적의 loss 감소가 이루어지지 않음

## 6. vanishing gradient
<img width="661" height="228" alt="image" src="https://github.com/user-attachments/assets/f0dbe0a4-e321-44e7-979b-e1f4a7766d7e" />

- 네트워크가 깊어질수록 역전파 과정에서 gradient가 점점 작아져서 초반 층의 가중치가 제대로 업데이트되지 않는 문제
- 활성함수의 작은 기울기가 누적되어 기울기가 사라지는 현상

## 7. Residual Learning
<img width="597" height="259" alt="image" src="https://github.com/user-attachments/assets/63f88198-8961-434e-8f76-e98e614f6106" />

- 잔차를 최소화하는 학습 방법
- Gradient vanishing 현상 극복 가능
- 최소 loss 최적화를 더 빠르고 효율적으로 수행 가능

## 8. ResNet
<img width="317" height="272" alt="image" src="https://github.com/user-attachments/assets/234b0d1d-bb97-4296-ad50-1069457dca8f" />

- Residual block을 겹겹이 쌓은 형태
- 각 stage 내에서는 feature map size가 동일하나 다음 stage로 넘어갈때마다 feature map size 2배 감소, fillter개수 2배 증가

- 깊은 신경망 학습 : residual block 를 통해 깊은 네트워크 구조에서도 효과적인 학습 가능
- Vanishing Gradient 문제 해결 : 역전파 과정에서 gradient 흐름을 원활하게 유지함
- Degradation 문제 완화 : residual learning 을 통해 깊어진 네트워크에서도 성능 유지

## 9. UNet
- 이미지 내의 각 픽셀을 의미 있는 라벨로 분류하는 Semantic Segmentation
- 왼쪽에서 정보를 압축 (Encoding)하고 오른쪽에서 복원 (Decoding)하는 구조

- Skip connection : 인코더의 각 레이어 출력을 대응하는 디코더 레이어에 연결해 공간적 세부 정보를 보존함
- Contaracting path : 점진적으로 넒은 범위의 이미지 픽셀을 보며 문맥 정보를 추측
- Expanding path : 문맥 정보를 픽셀 위치 정보와 결합하여 local detail를 복원

# 02. Detection

## 1. Detection
<img width="539" height="212" alt="image" src="https://github.com/user-attachments/assets/07a1a034-fdc4-46f7-b935-155dc4f6deb2" />

- 이미지 또는 영상 내의 object 위치를 특정(localizing)하고 분류(classifying)하는 과정
- 특정 object를 찾아내고 해당 object의 bounding box를 제공하는 것이 목표

<img width="599" height="270" alt="image" src="https://github.com/user-attachments/assets/33c47755-8685-4789-a689-8495763e6e32" />

- 2-stage Detector : Regional Proposal (객체의 위치를 찾는 과정) 과 Classification (객체를 분류하는 과정)이 순차적으로 이루어짐
- 1-stage Detector : Regional Prosal 과 Classification이 동시에 이루어짐

## 2. YOLO
- 1-stage-detection 방법을 고안하여서 실시간으로 객체 감지를 간으하게 한 모델

<img width="367" height="275" alt="image" src="https://github.com/user-attachments/assets/832f8439-804d-44bc-ba6c-14ab20717aa4" />

- 전역적 이미지 처리 : 이미지 전체를 한 번만 살펴보고 객체의 위치와 종류를 동시에 예측
- 통합된 모델을 사용 : 이미지 분류와 바운딩 박스 회귀를 하나의 CNN 모델로 통합해 동시에 수행함
- 높은 검출 정확도 : 새로운 이미지에 대해서도 일관된 검출 정확도를 보여주며 overfitting이 상대적으로 적용

EX) 4*4 grid, cell 당 예측해야 하는 bounding box(bbox) 개수 =2, 총 클래스 20
<img width="720" height="277" alt="image" src="https://github.com/user-attachments/assets/f1f9eb42-af6c-4aff-ae7b-1b580babfa13" />

<img width="643" height="264" alt="image" src="https://github.com/user-attachments/assets/5771131c-773c-48e5-88b4-73cc3f6f67e8" />

<img width="665" height="281" alt="image" src="https://github.com/user-attachments/assets/c71e041f-5b77-45f4-8768-44d1df153fab" />

<img width="525" height="217" alt="image" src="https://github.com/user-attachments/assets/d4da5f67-e42a-4997-93e3-61c2a048d3fc" />

## 3. Focal Loss
- Background에 대한 Bounding Box의 비율이 객체 영역보다 압도적으로 높아, 학습 과정에서 class imbalance 문제가 발생할 수 있음
- class imbalance 문제로 인해 easy negative의 영향이 압도적으로 커지며 학습이 비효율적으로 진행됨
- 또한 모델이 hard posotove(실제 객체)를 detect 하고자 학습하지 않음

<img width="735" height="221" alt="image" src="https://github.com/user-attachments/assets/6c522de0-d139-47f9-92af-a2a6e346afdc" />

- y: y = 1 (foreground), y = 0 (background)
- p: 모델이 y = 1이라고 예측한 확률

<img width="537" height="247" alt="image" src="https://github.com/user-attachments/assets/f3a6cfa2-2f0f-4ed3-a184-44830a6bf713" />

## 4. Transformer
- 전체 입력 간의 관계를 한 번에 파악하여 병렬 처리와 장기 의존성 학습이 가능한 모델 구조
- self-attention : 메커니즘을 사용하여 각 입력 요소의 연관성을 학습

<img width="179" height="206" alt="image" src="https://github.com/user-attachments/assets/a25dbc60-cf27-
420f-8248-878b5a5d454e" />

- Self-attention : 문장 내 모든 단어 쌍 사이의 관계를 직접 계산하여 전체 문장의 의미를 이해함
- Multi-Head Attention :: 단일 self-attention 레이어를 여러 개 사용하는 기법으로, 모델이 다양한 위치의 패턴을 동시 학습
- Positional Encoding : 입력 시퀀스의 각 위치에 대한 정보를 추가로 인코딩하여 모델에 제공

## 5. Vision Transformer (VIT)
<img width="668" height="245" alt="image" src="https://github.com/user-attachments/assets/552bd0c6-b7e3-4c05-a6a5-ce08a731d7b1" />

- 자연어 처리 (NLP)에서 많이 사용되는 Transformer를 Vision Task를 적용한 모델
- 공간에 대한 bias가 없어서 많은 사전데이터 학습이 필요함

<img width="668" height="245" alt="image" src="https://github.com/user-attachments/assets/b046e0aa-5c24-42ee-8639-f81450e5e960" />

- Transformer : 순차적으로 transformer encoder 블록을 여러번 통과시켜 특성을 추출한다.
- Classfication token 추출 : transformernencoder의 최종 출력 중 Classfication token에 해당하는 벡터를 선택
- MLP Head & Softmax : 추출된 CLS 벡터에 분류 헤드를 적용하고, softmax로  최종 클래스 확률을 계산

- VIT는 CNN에 비해 Inductive bias가 상대적으로 낮은 모델
- Inductive bias : 모델이 자체적으로 가지고 있는 편견

<img width="748" height="238" alt="image" src="https://github.com/user-attachments/assets/0a0d688c-ec27-4ee1-838e-93d40a66550a" />


# 03. Vision Transformer

<img width="529" height="260" alt="image" src="https://github.com/user-attachments/assets/a11e2cef-490d-406f-a9ae-e00818e6ddc9" />
