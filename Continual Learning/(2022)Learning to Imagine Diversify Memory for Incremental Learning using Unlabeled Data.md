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
- 기존 feature extractor를 f1,f2로 나누고 / feature generator를 f1,f2 사이에 넣는다.
- new task를 학습할때는, generate는 freeze 되고 / exemplar의 다양한 counterparts(exemplar와 unlabeled data를 f1에 통과시키고 합친것)를 generate한다. 
![image](https://user-images.githubusercontent.com/98244339/167745786-e3b5d2c5-7bde-4e26-9346-e4a95256aaf0.png)

## Learning of Feature Generator
### Before Learning Method..
- Exemplar와 Unlabeled data를 첫번째 feature map(f1)을 통과시키고 합친 후, feature generator(G_c) 통과시켜, feature map(h_mix) 생성한다.
- feature generator는 2가지 특징 ( exemplar와 semantic information & exemplar-unlabeled data 간 augmenting )

- Exemplar : ![image](https://user-images.githubusercontent.com/98244339/167746820-8ac38923-7efc-4912-b8ff-f2993899d8b3.png)
- Unlabeled data : ![image](https://user-images.githubusercontent.com/98244339/167746880-53a025a7-7cd0-49f5-8309-edfd3ddc334a.png)
- Original data : ![image](https://user-images.githubusercontent.com/98244339/167748500-42fda64b-d06f-439f-b15d-caf57eea6015.png)
- ![image](https://user-images.githubusercontent.com/98244339/167747572-c1e86ce2-322f-45dd-bb84-e7f2f266d961.png)

### Semantic contrastive learning
- h_mix(generated feature) 에서 semantic information을 도출하기 위해서, Global Average Pooling(GAP)수행
- ![image](https://user-images.githubusercontent.com/98244339/167747875-8cd1e8b4-86ba-43e6-a7ce-a175e4a39283.png)
- h_mix(generated feature) 와 original data(bias가 생길 수 있는 exemplar대신 사용) 간 semantic information 이 적어지도록 학습 (SC)
- x_i^k 를 f1 통과시키고, GAP수행하여 v_i^k 생성
- ![image](https://user-images.githubusercontent.com/98244339/167748238-850e172c-b24a-45fb-95e9-7da018a712cc.png)

### Semantic-Decoupling contrastive learning
- cf.] gram matrix 는 주로 feature map에서 semantic-irrelevant information 을 encode하는데 사용된다.(channel간 관계가 encode됨) ( 8,12,23,24,31 번 논문 참조 )
- Unlabeled data를 적극활용하기 위해, semantic-information을 분리하고, gram matrix 를 사용하여 semantic-irrelevant information을 캔다.
- ![image](https://user-images.githubusercontent.com/98244339/167749419-7ab1d7a1-03b3-4d1e-b412-74bf34702a1b.png)
- ![image](https://user-images.githubusercontent.com/98244339/167749459-925a250e-1463-4358-8dc0-ebddfa57bdc9.png)


