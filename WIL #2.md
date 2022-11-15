# WIL #2

### 논문 리딩

[A survey on sentiment analysis methods, applications, and challenges](https://link.springer.com/article/10.1007/s10462-022-10144-1)

<br/> 

**감성분석 수준**

<img width="171" alt="image" src="https://user-images.githubusercontent.com/83004338/201917406-ce00eefd-c156-49c3-a441-1effe311bf3e.png">

- Document level
- Sentence level
- Phrase level
- Aspect level
  >Primary attention to all the aspects used in the sentence and assigns polarity to all the aspects after which an aggregate sentiment has calculated for the whole sentence< 

<br/>

**Feature**

- Pragmatic features: 단어가 적용되는 맥락 중시
- Emoji: 긍정/부정적 이모지를 통한 어조 전달
- Punctuation marks: 긍정/부정의 어조 강조
- Slang

<br/>

**방법론**

1. Feature extraction
- pre-process(주로 문장부호 등 삭제) -> tokenization -> grammatical tagging ->
- 감정 분석에서는 주로 형용사가 많이 이용됨
- 부정 단어 및 중립 단어 --> 이 부분에서 모델의 성능이 주로 결정되는 듯함


<br/>

****


<br/>

---

### 프로젝트 관련 고민 정리

- "일기"의 기준
  - SNS (인스타, 트위터, 네이버 블로그 등)
  - 다이어리 어플
    - 채널에 따라 분량, 어조, 형식 등 다양한 측면에서 차이점이 있을 것 같다
    - 한 줄짜리부터 일주일치 분량을 한 번에 다 적기도 할 것
    - 일기를 쓰는 간격, 일기를 쓸 때의 감정 상태 등이 사람마다 모두 다를 것...

- 수집 및 활용
  - 네이버 주간일기 해시태그 기준으로 수집해도 되지 않을까 -> 그래도 되나
