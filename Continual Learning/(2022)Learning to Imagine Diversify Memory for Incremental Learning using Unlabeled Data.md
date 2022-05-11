## Key Idea : Exemplar 에서 semantic information(의미적으로 유사한 정보) & Unlabeled Data에서 semantic-irrelevant information(관련없지만 상상하고 탐험할 수 있는 정보)로 feautre generator 를 학습 시켜, feature extractor 중간에 넣는다. 

## Unlabeled data에서 imagine하는 motivation(a) & Method Picture
![image](https://user-images.githubusercontent.com/98244339/167744094-a1166c51-6427-4a2b-877c-188635fdd2a4.png)

## Introduction
- 기존에 exemplar를 생성하고, 학습했던 데이터를 버리기 전에 feature generator(class별 각각 feature generator 소유)학습한다.
- 새로운 task가 오면, feature generator를 freeze 하고, generator 에서 sample 생성. ( 단지, 이전에 학습했던 class를 잊지 않기 위해서, 학습할때만 사용 )
- Inference할때는, featrue generator를 버리고, vanilla deep model만 필요하다.
[Learning Method]</br>
1. Semantic Contrastive Learning(SC) : generated 된 sample들이 Original data와 의미적으로 유사하도록 학습
2. Semantic-decoupling Contrastive Learning(SDC) : gemerated된 sample들과 Unlabled data간 ( generated된 smapled 이 다양하도록.. )

## Learning Framework
- 
![image](https://user-images.githubusercontent.com/98244339/167745786-e3b5d2c5-7bde-4e26-9346-e4a95256aaf0.png)




