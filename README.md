<p align="center"><img src="./img/legalinsight_logo.png" width=300px></p>

# Pretrained Korean Language Model (Law)
한국어 법률분야 및 신문 corpus로 pre-train한 사전학습모델(BERT-Base, BERT-Small) 학습결과 입니다.

법률분야 단어가 추가된 vocab구축 후 법률분야 및 신문 corpus를 학습해 일반 한국어 및 법률분야 NLP TASK의 성능 테스트하였습니다.  

|   |H=128|H=256|H=512|H=768|
|---|:---:|:---:|:---:|:---:|
| **L=4**  |[4/128]|[4/256]|[**4/512 (BERT-Small)**]|[4/768]|
| **L=12** |[12/128]|[12/256]|[12/512]|[**12/768 (BERT-Base)**]|

참조 : https://github.com/google-research/bert/blob/master/README.md 


|                               | KorQuAD1.0 (F1/EM) | ETRI law mrc (F1/EM) | KLUE NER(F1) | KMOU NER(F1) | KorNLI(acc) | 계약서추천 데이터셋(F1) | 개인정보NER 데이터셋(F1) |
|:-----------------------------:|:------------------:|:--------------------:|:------------:|:------------:|:-----------:|:---------------------:|:-----------------------:|
|       BERT (Small Size)       |    87.97/77.78     |    87.62/73.55       |  89.18       |  89.15       |  73.0       |  76.6                 |  71.45                  |
|       BERT (Base Size)        |    92.00/83.36     |    91.52/79.85       |  91.78       |  91.65       |  78.4       |  79.5                 |  72.79                  |

*dev set 기준 성능

* 계약서추천, 계약서 분류, 개인정보NER 데이터셋은 NIA R&D사업(계약서 자동작성 서비스, 계약서 RISK 분석, 개인정보침해평가)으로 자체 제작한 데이터셋 입니다.
* sample dataset은 sample 폴더에 업로드 했습니다.

참조 : https://github.com/huggingface/transformers/tree/master/examples/pytorch

# Pretrained Model Detail
* Small : 법률, 법령, 조약, 판례, 국회회의록, 신문 (3GB, txt기준)
* Base : 법률, 판례, 국회회의록, 신문 (10GB, txt기준)

* Masking Strategy: Whole word Masking
* Additional Task: NSP (Base Model의 경우, 제목과 기사내용을 sequence A와 sequence B로 하여 추가로 학습)
```
Sentence A: 한국 축구, 왜 중국에 농락당했나
Sentence B: 아무리 유럽파가 빠졌다고 하지만 그래도 A 매치였는데 중국에 0-3으로 졌다 ... 이것이 월드컵을 120일밖에 남겨놓지 않은 한국 축구대표팀 수비의 현주소였다. 이래도 대회가 임박한 것이 아니라는 사실에 위안을 삼아야 할까?
Label: IsNextSentence
```

* Optimizer: Adam Optimizer
* Scheduler: LinearWarmup
* Mixed-Precision : fp16
* Hyper-parameters

| Hyper-parameter       | Small Model | Base Model        |
|:----------------------|:------------|:------------------|
| Number of layers      | 12          | 12                |
| Hidden Size           | 256         | 768               |
| FFN inner hidden size | 1024        | 3076              |
| Mask percent          | 15          | 15                |
| Learning Rate         | 0.0001      | 0.0001            |
| Warmup Proportion     | 0.05        | 0.1               |
| Attention Dropout     | 0.1         | 0.1               |
| Dropout               | 0.1         | 0.1               |
| Batch Size            | 128         | 128               |
| Train Steps           | 1M          | 300k              |

# Tokenization

3가지 단계로 tokenization을 진행했으며 아래와 같습니다. 

1.  **Text normalization**: 특수문자 및 외국어, 한자 중 일부는 nomarlizing
```
input text : 식품의약품안전처는 혈중농도 최저 0.205ng/㎖(3일)부터 최고 1.216ng/㎖(8일) 범위 내에서
normalizing 후 : 식품의약품안전처는 혈중농도 최저 0.205ng/ml(3일)부터 최고 1.216ng/ml(8일) 범위 내에서
```

2.  **Morph splitting**: 한글, 영어, 숫자를 제외한 문자는 split했으며, mecab의 morphs를 통해 형태소 단위로 split
```
input text : 식품의약품안전처는 혈중농도 최저 0.205ng/ml(3일)부터 최고 1.216ng/ml(8일) 범위 내에서
splitting 후 : 식품의약품안전처 는 혈중 농도 최저 0 . 205 ng / ml ( 3 일 ) 부터 최고 1 . 216 ng / ml ( 8 일 ) 범위 내 에서
```

3.  **WordPiece tokenization**: split한 token별로 WordPiece tokenizing
```
input text : 식품의약품안전처 는 혈중 농도 최저 0 . 205 ng / ml ( 3 일 ) 부터 최고 1 . 216 ng / ml ( 8 일 ) 범위 내 에서
tokenizing 후 : 식품 ##의약품 ##안전 ##처 는 혈중 농도 최저 0 . 20 ##5 ng / ml ( 3 일 ) 부터 최고 1 . 21 ##6 ng / ml ( 8 일 ) 범위 내 에서
```
