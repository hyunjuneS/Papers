## key idea : class imblance 상황에서 발생하는 문제(Imbalanced Magnitudes,Deviation,Ambiguities) 문제 해결하기 위해 Cosine Normalization/Less forget constraint / Inter-class separation 사용하여 해결하자.

[class imbalance 로 인하여 class embedding layer(마지막 classifer layer / softmax 이전 score layer)가 편향되었다.( BiC에서도 실험적으로 밝힘 )] </br>
- Imbalanced Magnitudes :  class embdedding(classifier / softmax 이전) layer가 new classes에 큰 value/magnitude/weight 를 가지고 있다. --> Cosine normalization
- Deviation : Imbalanced Magnitudes를 cosine normalization으로 정규화시킨 후, Distillation loss (feature extractor - embedding 간 cosine similarity)를 사용하려고 하였다. 하지만, feautre extractor - embedding 으로 계산하는 cosine similarity가 발생하는 문제(180도 shift된 상황에서 같은 각도 유지)가 있다. --> Less forget constraint
- Ambiguities : class embdedding vector가 old class 와 new class 겹치게 존재하여 애매하다. --> Inter-class separation 
<img width="700" alt="image" src="https://user-images.githubusercontent.com/98244339/165193207-c45b10a8-4712-4872-b7fb-fe92accf4b57.png">

## Main structure & loss term
![IMG_A577E6FEF514-1](https://user-images.githubusercontent.com/98244339/165194054-84fe566e-18ed-48a6-ae32-fbb5656ea3b8.jpeg)

## Problem1. Imbalanced Magnitudes --> Cosine Normalization
- feature extractor를 거쳐 class embedding 후 softmax 상황에서, cosine similarity 를 통해 normalization 수행
- feature extractor 와 class embedding 을 -1~1 로 normalization 수행
- <img width="700" alt="image" src="https://user-images.githubusercontent.com/98244339/165194564-3c265883-90a9-442f-91a8-2d3a0ec75acf.png">
- <img width="700" alt="image" src="https://user-images.githubusercontent.com/98244339/165194666-d0333811-5fb6-4d8e-9dfa-e1556a83e50c.png">

## Classification loss ( Lce )
- crossentropy loss 사용
- <img width="700" alt="image" src="https://user-images.githubusercontent.com/98244339/165194780-d9a45af2-0abf-4e6c-bb5c-63c3519bdab7.png">

## Problem2. Deviation --> Less-Forget Constraint ( Ldis )
- Cosine Normalization 을 통해 softmax이전 weight가 -1~1로 normalization 되었다.
- 이를 통해 Distillation loss는 아래와 같이 정리될 수 있다. ( class embedding - feature extractor 간 각도가 유지되도록 ) 
- <img width="700" alt="image" src="https://user-images.githubusercontent.com/98244339/165195194-f0e3868d-9788-47c5-be80-4f0323c3a8dd.png">
- 하지만, 아래의 그림과 같이 feature extracotr - class embedding 간 각도는 180도 반전이 되어도 같다. ( 다른 상황에서 loss term 이 작아질 수 있음 )
- <img width="700" alt="image" src="https://user-images.githubusercontent.com/98244339/165195317-2f0a5f41-22e3-4898-9401-97ce03fba6ce.png">
- 따라서, 어차피 -1~1로 정규화 되어있으므로, feature extractor간 각도만 유지되도록 loss term을 만든다.
- <img width="700" alt="image" src="https://user-images.githubusercontent.com/98244339/165195350-8e47263d-91a2-4bb6-8ef2-68a9337ca04d.png">





