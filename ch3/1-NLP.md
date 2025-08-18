# 01. INTRODECTION

<img width="688" height="194" alt="image" src="https://github.com/user-attachments/assets/a3a469d6-2e6c-4e77-9acb-0a3eb24f63c0" />

## 1. 자연어 (Natural Language)
- 일상생활에서 사용하는 보편적인 언어

## 2. 자연어처리 (Natural Language Processing)
- 컴퓨터가 자연어를 처리하는 일
- 구성요소
  1. NLU : 컴퓨터가 인간 언어를 이해하는 과정
  2. NLG : 컴퓨터가 인간 언어를 생성하는 과정

  ## 3. NLP의 주요 구성 요소
  - Tokenization : 문장을 단어/토큰 단위로 분리
  - Part-of-Speech Tagging : 품사 태깅
  - Entities : 개체명 인식 ( 사람, 장소, 조직 등)
  - Contextual Understanding : 문맥의 이해
  - Utterances : 발화 단위 분석
  - Sentiment Analysis : 감정 분석
  - Intents : 의도 파악
  - Dialogue Manager : 대화 흐름 관리
  - Machine Learning : 기계학습 기반 처리
 
  # 02. Text Preprocessing
  - 자연어 처리를 하기전에 텍스트 데이터를 분석 가능한 형태로 만들기 위한 전처리 과정

  ## 1. 토큰화 (Tokenization)
  - 문장을 의미있는 최소 단위로 분리함
  - 예시
    - 입력 : "자연어 처리는 재미있다."
    - 출력 : ["자연어", "처리", "는", "재미있다"]

    ## 2. 정제 (Cleaning)
    - 불필요한 문자나 기호를 제거하여 데이터 품질을 높이는 과정
    - 제거대상
      - 특수문자
      - HTML 태그
      - 공백
      - 잡음 데이터

    ## 3. 정규화 (Normalization)
    - 같은 의미를 가진 다양한 표현을 통일된 형태로 변환
    - 예시
      - 대소문자 변환
      - 숫자 단위 표기
      - 띄어쓰기 수정

    ## 4. 불용어 제거
    - 의미 전달에 기여도가 낮은 단어 -> 조사, 접속사, 빈도높은 관용적 단어 등
    - 예시 : "나는 오늘 학교에 간다" → ["오늘", "학교", "간다"]

    ## 5. 어간/표제어 추출
    - 단어의 다양한 활용형을 기본형으로 변환하여 의미를 통일함
    - 비교
      - Stemming : 단순히 어간을 자르는 방식 (`studies → studi`)
      - Lemmatization : 문맥과 품사를 고려한 변환 (`studies → study`)

    # 03. N-gram

    ## 1. N-gram 모델
    - 문장 소게서 연속된 N개의 단어 시퀀스를 보고, 다음 단어가 나올 확률
    - Chain Rule : 단어 시퀀스의 확률을 조건부 확률 곱으로 표현

    
예시: `"I like pizza"`  
<img width="505" height="121" alt="image" src="https://github.com/user-attachments/assets/083ab6a3-ffad-4eee-9909-a1bf8f927213" />


## 2. Markov Assumptioin (마르코프 가정)
- 다음 단어는 전체 과거 시퀀스가 아니라, 최근 n-1개의 단어에만 의존한다고 가정
<img width="287" height="35" alt="image" src="https://github.com/user-attachments/assets/c546a99f-06eb-4756-9575-5705671285b1" />


## 3. Bigram & N-gram 확률
### Bigram (2-gram) 가정
<img width="436" height="96" alt="image" src="https://github.com/user-attachments/assets/521c6809-e142-45e1-9642-d7fdd264263d" />


### 일반 N-gram 가정
<img width="301" height="48" alt="image" src="https://github.com/user-attachments/assets/6390bc5f-0a06-4312-b416-b98b3ab79beb" />


## 4. 확률 계산 (MLE)
- N-grma확률은 빈도수 기반으로 추정
<img width="206" height="107" alt="image" src="https://github.com/user-attachments/assets/0625fe0a-8092-4fc6-b0b0-9c4750a5cd07" />

## 5. 예시 (Bingram)
<img width="601" height="194" alt="image" src="https://github.com/user-attachments/assets/b1c7776c-9a31-4c90-8e59-b8ff346b659f" />


# 04. Word Embedding

## 1. Word Embedding
- 단어의 의미를 벡터 공간에서의 위치로 정의
- 의미가 비슷한 단어일수록 벡터 공간에서 가깝게 위치함

## 2. Word Embedding 종류
