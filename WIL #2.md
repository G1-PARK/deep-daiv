# WIL #2

## 1. 논문 리딩

감성분석과 관련하여, 기본 방법론과 적용을 다룬 기초 논문을 읽었습니다.

[A survey on sentiment analysis methods, applications, and challenges](https://link.springer.com/article/10.1007/s10462-022-10144-1)

<br/> 

<img width="171" alt="image" src="https://user-images.githubusercontent.com/83004338/201917406-ce00eefd-c156-49c3-a441-1effe311bf3e.png">

먼저, 감성분석의 level은 Document level, Sentence level, Phrase level, Aspect level로 구분됩니다. 

이 중 Phrase level은 사용되는 용어에 의한 성별, 연령, 사회적 지위, 성격 등 인구통계학적 구분이 필요한 경우 주로 사용됩니다. Aspect level에서는 문장 내의 모든 aspect에 대해 감정 polarity를 부여한 후 전체 문장에 대한 감성분석을 실시합니다.

<br/>

**방법론**

(추후 별도 )

<br/>

## 2. 감성분석 실습

[네이버 영화 리뷰 감성 분석(Google Colab)](https://colab.research.google.com/drive/1HHl27vdHOnN5Qu38fcQ904p_WshnvJ1k?usp=sharing)

[참고 링크: 딥러닝을 이용한 자연어 처리 입문](https://wikidocs.net/44249)

<br/>

## 3. 프로젝트 관련 고민

일기 내용 감성분석을 통한 감정 리포트를 제작한다고 하면, 먼저 대상으로서의 "일기"의 기준을 고려해 보아야 할 것입니다.

다이어리에 적는 손글씨 데이터셋은 수집도 어렵고 이미지 분석도 병행해야 하기 때문에 우선은
  - SNS (인스타, 트위터, 네이버 블로그 등)
  - 다이어리 어플 

등의 출처를 생각해 볼 수 있겠습니다. 그 중에서 네이버 블로그의 경우 **주간일기 해시태그**를 통해 주차별로 일기를 수집할 수 있지 않을까 싶습니다. 하지만 활용이 가능한지는 고민...

위에서 말한 각 채널들은 성격이 뚜렷한 편이라, 채널에 따라 분량, 어조, 형식 등 다양한 측면에서 차이점이 있을 것 같습니다. 따라서 수집 채널을 통일하거나, 수집 채널별 감성분석을 실시해 보는 것도 좋을 것 같습니다. 분량도 마찬가지로, 채널 및 기록의 성격에 따라 한 줄짜리부터 일주일치 분량을 한 번에 다 적기도 하는 등 매우 다양한 양상을 보일 것입니다. 일기를 쓰는 간격, 쓸 때의 감정 상태 등이 사람마다 모두 다를 것이므로 이런 부분에 대한 고민이 더 필요할 듯...

감성분석 관련해서 이것저것 실습해 봐도 좋겠네요
