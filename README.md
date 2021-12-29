<p align="center"><img src="./img/legalinsight_logo.png"></p>

# Pretrained Korean Language Model (Law)
한국어 법률분야 및 신문 corpus로 pre-train한 사전학습모델(BERT-Base, BERT-Small) 학습결과 입니다.

법률분야 단어가 추가된 vocab과 법률분야 corpus를 학습해 일반 한국어 및 법률분야 NLP TASK의 성능을 비교하였습니다.  

|   |H=128|H=256|H=512|H=768|
|---|:---:|:---:|:---:|:---:|
| **L=2**  |[2/128]|[2/256]|[2/512]|[2/768]|
| **L=4**  |[4/128]|[4/256]|[**4/512 (BERT-Small)**]|[4/768]|
| **L=6**  |[6/128]|[6/256]|[6/512]|[6/768]|
| **L=8**  |[8/128]|[8/256]|[8/512]|[8/768]|
| **L=10** |[10/128]|[10/256]|[10/512]|[10/768]|
| **L=12** |[12/128]|[12/256]|[12/512]|[**12/768 (BERT-Base)**]|

참조 : https://github.com/google-research/bert/blob/master/README.md 



# Pretrained Corpus

