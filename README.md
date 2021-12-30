<p align="center"><img src="./img/legalinsight_logo.png" width=300px></p>

# Pretrained Korean Language Model (Law)
한국어 법률분야 및 신문 corpus로 pre-train한 사전학습모델(BERT-Base, BERT-Small) 학습결과 입니다.

법률분야 단어가 추가된 vocab구축 후 법률분야 및 신문 corpus를 학습해 일반 한국어 및 법률분야 NLP TASK의 성능 테스트하였습니다.  

|   |H=128|H=256|H=512|H=768|
|---|:---:|:---:|:---:|:---:|
| **L=2**  |[2/128]|[2/256]|[2/512]|[2/768]|
| **L=4**  |[4/128]|[4/256]|[**4/512 (BERT-Small)**]|[4/768]|
| **L=6**  |[6/128]|[6/256]|[6/512]|[6/768]|
| **L=8**  |[8/128]|[8/256]|[8/512]|[8/768]|
| **L=10** |[10/128]|[10/256]|[10/512]|[10/768]|
| **L=12** |[12/128]|[12/256]|[12/512]|[**12/768 (BERT-Base)**]|

참조 : https://github.com/google-research/bert/blob/master/README.md 


|                               | KorQuAD1.0 (F1/EM) | ETRI law mrc (F1/EM) | KLUE NER(F1) | KMOU NER(F1) | KorNLI(acc) | 계약서추천 데이터셋(F1) |
|:-----------------------------:|:------------------:|:--------------------:|:------------:|:------------:|:-----------:|:---------------------:|
|       BERT (Small Size)       |    -               |    -                 |  -           |  -           |   -         |  76.6                 |
|       BERT (Base Size)        |    92.00/83.36     |    91.52/79.85       |  91.78       |  91.65       |  78.4       |  78.9                 |

*dev set 기준 성능

* KorQuAD1.0, ETRI law mrc는 huggingface의 BertForQuestionAnswering으로 학습하였습니다.
* KLUE NER, KMOU NER는 huggingface의 BertForTokenClassification으로 학습하였습니다.
* KorNLI, 계약서추천 데이터셋은 huggingface의 BertForSequenceClassification으로 학습하였습니다.
* 계약서추천 sample dataset은 sample폴더에 업로드 하였습니다.

참조 : https://github.com/huggingface/transformers/tree/master/examples/pytorch

# Pretrained Corpus

