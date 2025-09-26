# 01. What is MultiModal 

## 1. 멀티모달이란 ?
- 다양한 채널의 데이터를 동시에 받아서 학습/추론하는 AI
- 텍스트, 이미지, 음성 등 서로 다른 유형의 데이터가 연결되고 상호작용함
- 인간이 다양한 감각 (시각, 청삿, 언어 등)을 결합해서 세상을 이해하는 것과 유사함

## 2. 왜 필요한가 ?
- 실제 세상은 열 데이터 유형이 복합적으로 얽혀 있음
- 단일 모달리티 기반 시스템은 전체 상황 이해에 한계임
- 인간처럼 상황을 종합적으로 이해할 수 있는 모델 필요성 증가

## 3. 활용
1. Image Captioning
<img width="322" height="192" alt="image" src="https://github.com/user-attachments/assets/393752af-1b05-4f25-bea5-5a559cc687a2" />

- 입력 : 이미지
- 출력 : 이미지를 설명하는 문장 생성
- 예: 고양이+스케이트보드 → "A cat riding a skateboard"

2. Visual Question Answering (VQA)
<img width="324" height="126" alt="image" src="https://github.com/user-attachments/assets/97b79140-6cbb-4bb3-b88f-f7eeddcd1fff" />

- 입력 : 이미지 + 질문
- 출력 : 답변
- 사진 + "What is the mustache made of?" → "Bananas"

# 02. 6 challenges of MultiModal

## 1. Representation
<img width="676" height="224" alt="image" src="https://github.com/user-attachments/assets/0d286bf6-a277-48c5-8a75-ad3cb178fda1" />

- 각기 다른 모달리티 (텍스트, 이미지, 오디오등)을 모델이 이해할 수 있게 표현하고 통역
- 서로 다른 데이터는 차원/분포가 달라서 통합이 어려움
- 예: 텍스트(이산적) vs 이미지(연속적)

## 2. Alignment
<img width="753" height="253" alt="image" src="https://github.com/user-attachments/assets/90126482-969b-476f-91bf-89f746dd9064" />

- 서로 다른 모달리티 사이에서 같은 의미 단위를 맞추는 문제
- 예: "개(dog)"라는 단어 ↔ 개 이미지
- 기법:
  - Explicit alignment (grounding)  
  - Implicit alignment + representation  
  - Segmentation granularity
  
## 3. Reasoning
<img width="751" height="224" alt="image" src="https://github.com/user-attachments/assets/c6f64fb6-9614-47c6-b982-6cdfb3d826a4" />

- 다양한 모달리티에서 들어온 정보를 구조호 및 연결 한 후 추론 단계를 거쳐서 논리적인 판단이나 정답을 도출하는 과제
- 예: 우산을 쓴 사진 + 질문 "비가 오나요?" → 추론 후 답변
- External knowledge와 연결되어야 더 정확한 reasoning 가능

## 4. Generation
<img width="822" height="267" alt="image" src="https://github.com/user-attachments/assets/4075de28-a99a-4962-9185-a45cf863c91c" />

- 한 모달리티 정보를 바탕으로 다른 모달리티 생성
- 생성 결과가 자여느럽고 일관되며 의미 있어야 함
- 예: 이미지 → 설명 문장 생성 (Image Captioning)
- 유형: Summarization / Translation / Creation

## 5. Trasference
<img width="735" height="226" alt="image" src="https://github.com/user-attachments/assets/2aca0697-8853-460f-9abd-3ffe3f846e11" />

- 한 모달리티에서 학습한 지식을 다른 모달리티에 전이/활용 하는 문제
- 예 : 풍부한 이미지 데이터 → 텍스트 모달리티로 지식 전달
- 방식: Transfer / Co-learning / Model Induction

## 6. Quantification
<img width="906" height="228" alt="image" src="https://github.com/user-attachments/assets/47c341e4-1e2a-41a4-92cd-e9148a0c70ae" />

- 멀티모달 학습이 얼마나 기여 했는지 측정하는 문제
- 더 건고하고 신회할 수 있는 모델 구축을 위해서 필요함
- 예 : 각 모달리티가 성능에 기여하는 정도 분석

## 7. Representation 검정법 ; t-SNE
- t-SNE : 서로 다른 모달리티 벡터를 2D/3D로 축소시킴
- 같은 의미라면 서로 가까이 위치해야함

## 8. Alignment 검정법 
- Cross-modal Retrieval :
  - 텍스트 -> 이미지 검색
  - 이미지 -> 텍스트 검색
- cosine similarity , Euclidean distance로 유사도 측정
- 유사도가 높은 후보를 정렬 -> Top-K 평가

# 03. Learning Representation

## 1. Representation 유형
- Joint Representation : 여러 모달리티를 같은 공간에 임베딩함
- Coordinated Representation : 각 모달리티는 다른 공간에 임베딩 , 하지만 공통 의미 구조 유지
- Encoder-Decoder : 입력 모달리티를 임베딩 후 , 다른 모달리티를 생성함

## 2. Joint Representation
- 서로 다른 데이터를 하나의 공간에 융합함 -> 직관적인 의미 비교가 가능함
- 예시 : Additive, Tensor Fusion Network, MCB
- 장점 : 의미 비교 용이함, 모달리티 간 상호작용 강화
- 단점 : 정보 손실 가능, 학습 어려움

## 3. Joint Representation
- Additive : 각 모달리티 인코딩 결과를 더해서 (shared layer) 선형 결합
- Tensor Fusion Network (TFN) : 텐서 외적을 통해서 모든 상호작용 포착
- MCB (Multimodel Compact Bilinear Pooling) : TFN의 차원 폭발 문제를 해결함 , 효율적으로 근사

## 4. Coordinated Representation
- 서로 다른 공간에 임베딩하되, 공통된 의미 구조 유지
- 학습 기법 :
  - Cross-modal Ranking : 정답 쌍은 가깝게 , 오답 쌍은 멀게 학습함
  - Euclidean Distance : 서로 다른 모달리티 간 거리 최소화
- 장점 : 모달리티 특성 보존 , 학습 안정성
- 단점 : 직접 비교가 어려움, 연산 복잡도 증가

## 5. Encoder-Decoder
- 입력 모달리티 -> 임베딩 -> 다른 모달리티 생성
-  예시: 이미지 입력 → 텍스트 설명 생성 (Image Captioning)
- 손실 함수:
  - Loss_gen: 생성 문장의 단어별 조건부 확률 (log likelihood)
  - Loss_sem: 생성된 문장 벡터와 원본 의미 벡터 간 거리
