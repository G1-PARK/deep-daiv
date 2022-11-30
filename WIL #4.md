# WIL #4 RoBERTa

## RoBERTa

[**Robustly Optimized BERT Pretraining approach**](https://arxiv.org/abs/1907.11692)

2018년 Google이 발표한 자연어처리 모델 BERT의 hyperparameters를 조정하여 성능을 높이는 방법

BERT-large와 아키텍처 및 데이터셋이 동일하게 구성되었으며, 논문은 주로 hyperparameters 변경 후 성능확인을 반복하는 실험 내용으로 구성

<br/>

**| 실험 내용**

**1. Dynamic Masking**

기존 BERT의 경우 static mask - 학습 시작 전 전처리 과정에서 마스킹을 한 번만 하고 고정하는 MLM(masked language model)방식. --> 매 학습 단계에서 같은 mask를 보게 됨.

RoBERTa의 경우 매 epoch마다 다른 mask를 적용하는 dynamic masking 방식 사용. 학습 중 동일한 mask는 4번만 보게 되므로 큰 데이터셋을 다루는 데 용이함. --> 학습 시간은 증가, but 메모리 절약 가능. static masking보다 높은 성능을 보여 줌.

**2. Input Format & NSP(next sentence prediction)**

BERT - 두 개의 문장을 이어붙인 input과 NSP loss를 pre-training 과정에 포함

RoBERTa - NSP 방식 x, token(< 512)을 최대한 이어붙여 input의 token 수를 최대한으로 늘림(full-sentences) --> NSP 방식을 채택하지 않은 경우 더 높은 성능.

**3. Large Batch**

전체 step 수를 유지하면서 batch size와 epoch 수 조정 --> 같은 step 수여도 batch size가 클수록 높은 성능을 보임.

**4. Tokenizer**

BERT - 전처리 이후 30K 크기의 character-level BPE tokenizer 사용

RoBERTa - 전처리 없이 50K 크기의 byte-level BPE tokenizer 사용 (GPT-2)

**5. More Data**

데이터 크기가 커질수록 성능도 향상 --> 총 160GB의 데이터 수집, 16GB로 pre-trained한 BERT-large보다 높은 성능을 보임. 학습 시간이 길수록 성능 향상.

<br>

**| 실험 결과**

상기 내용으로 모델 pre-train 후 GLuE, SQuAD, RACE 데이터로 성능 확인

**GLuE**

single-task on dev의 경우 전부 SOTA 달성

Ensembles on test의 경우 9개 영역 중 4개 영역 SOTA 달성

<img width="476" alt="image" src="https://user-images.githubusercontent.com/83004338/204744796-32347287-7b15-4650-8511-f650c577dc00.png">

**SQuAD**

data augmentation이 이루어지지 않은 경우 SOTA 달성 

<img width="234" alt="image" src="https://user-images.githubusercontent.com/83004338/204744863-9cafef1e-71f4-4770-8421-e4142a40bec2.png">

**RACE**

전부 SOTA 달성

<img width="235" alt="image" src="https://user-images.githubusercontent.com/83004338/204745241-a488b15c-8f87-4c0c-af92-07b9c4cf8566.png">

