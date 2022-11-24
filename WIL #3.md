# WIL #3

## 1. Model Research

1.1. mBERT

![image](https://user-images.githubusercontent.com/83004338/203674070-672656a8-0cfa-4a40-b528-306cf3004485.png)

BERT는 2개의 새로운 사전학습 목표(MLM, NSP)를 사용하는 언어 표현 모델로, NLI 등의 영역에서 사용되어 왔다. 1-2개의 문장 또는 구문을 input으로 받고, 두 문장을 연속으로 결합하고 첫 번째 토큰(CLS)의 hidden states를 가져와 문장 쌍을 분류한다. 텍스트를 양방향(앞뒤)로 확인하여 자연어를 처리하는 모델로, 기존 NLP 모델이 단방향(왼쪽 → 오른쪽)이었던 데 반해 BERT는 이 순서를 양방향으로 보기 때문에 다른 모델에 비해 매우 높은 정확도를 나타낸다. 

- 마스킹된 언어 모델링(MLM): 문장을 선택하면 모델이 입력 단어의 15%를 임의로 마스킹한 다음 마스킹된 전체 문장을 모델을 통해 실행하고 마스킹된 단어를 예측해야 한다. 일반적으로 단어를 하나씩 차례로 보는 기존 순환 신경망(RNN) 또는 미래 토큰을 내부적으로 마스킹하는 GPT와 같은 자동 회귀 모델과 다른데, 이를 통해 모델은 문장의 양방향 표현을 학습할 수 있다. 
- 다음 문장 예측(NSP): 모델은 사전 훈련 중에 두 개의 마스킹된 문장을 입력으로 연결한다. 원본 텍스트에서 서로 옆에 있던 문장에 해당하기도, 아니기도... 모델은 두 문장이 서로를 따르고 있는지 여부를 예측해야 한다.

mBERT는 BERT와 함께 출시되어 현재 104개의 언어를 지원하는데, 본질적으로 모든 언어의 공유된 어휘를 위키피디아 콘텐츠로 학습한 모델이다. 위키피디아의 콘텐츠 불균형을 해결하기 위해 적은 언어는 오버샘플링되고 많은 언어는 언더샘플링된다. 또한 공백이 없는 중국어, 일본어 간지 및 한국어 한자와 같은 언어는 모든 문자 주위에 CJK 유니코드 블록이 추가된다.

파이토치에서 사용하기 ↓↓↓
```
from transformers import BertTokenizer, BertModel
tokenizer = BertTokenizer.from_pretrained('bert-base-multilingual-cased')
model = BertModel.from_pretrained("bert-base-multilingual-cased")
text = "Replace me by any text you'd like."
encoded_input = tokenizer(text, return_tensors='pt')
output = model(**encoded_input)
```

출처: 
1) [huggingface](https://huggingface.co/bert-base-multilingual-cased)
2) [google researtch github](https://github.com/google-research/bert/blob/master/multilingual.md)

<br/>

1.2. KoBERT

KoBERT는 기존 BERT의 한국어 성능 한계를 극복하기 위해 개발되었다. 위키피디아나 뉴스 등에서 수집한 수백만 개의 한국어 문장으로 이루어진 대규모말뭉치(corpus)를 학습하였으며, 한국어의 불규칙한 언어 변화의 특성을 반영하기 위해 데이터 기반 토큰화(Tokenization) 기법을 적용하여 기존 대비 27%의 토큰만으로 2.6% 이상의 성능 향상을 이끌어 냈다. 대량의 데이터를 빠른시간에 학습하기 위해 링 리듀스(ring-reduce) 기반 분산 학습 기술을 사용하여, 십억 개 이상의 문장을 다수의 머신에서 빠르게 학습한다. 

학습환경

```
predefined_args = {
        'attention_cell': 'multi_head',
        'num_layers': 12,
        'units': 768,
        'hidden_size': 3072,
        'max_length': 512,
        'num_heads': 12,
        'scaled': True,
        'dropout': 0.1,
        'use_residual': True,
        'embed_size': 768,
        'embed_dropout': 0.1,
        'token_type_vocab_size': 2,
        'word_embed': None,
    }
```

파이토치에서 사용하기
```
>>> import torch
>>> from kobert import get_pytorch_kobert_model
>>> input_ids = torch.LongTensor([[31, 51, 99], [15, 5, 0]])
>>> input_mask = torch.LongTensor([[1, 1, 1], [1, 1, 0]])
>>> token_type_ids = torch.LongTensor([[0, 0, 1], [0, 1, 0]])
>>> model, vocab  = get_pytorch_kobert_model()
>>> sequence_output, pooled_output = model(input_ids, input_mask, token_type_ids)
>>> pooled_output.shape
torch.Size([2, 768])
>>> vocab
Vocab(size=8002, unk="[UNK]", reserved="['[MASK]', '[SEP]', '[CLS]']")
>>> # Last Encoding Layer
>>> sequence_output[0]
tensor([[-0.2461,  0.2428,  0.2590,  ..., -0.4861, -0.0731,  0.0756],
        [-0.2478,  0.2420,  0.2552,  ..., -0.4877, -0.0727,  0.0754],
        [-0.2472,  0.2420,  0.2561,  ..., -0.4874, -0.0733,  0.0765]],
       grad_fn=<SelectBackward>)
```


출처:
1) [SKT Brain](https://sktelecom.github.io/project/kobert/)
2) [SKT Brain Github](https://github.com/SKTBrain/KoBERT)


<br/>

1.3. RoBERTa

(추가 예정)

<br/>


## 2. 데이터셋 수집 (작성 중)

2.1. Chrome Driver 경로 문제 발생
