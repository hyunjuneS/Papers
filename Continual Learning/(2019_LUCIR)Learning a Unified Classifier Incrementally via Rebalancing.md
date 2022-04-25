## key idea : class imblance 상황에서 발생하는 문제(Imbalanced Magnitudes,Deviation,Ambiguities) 문제 해결하기 위해 Cosine Normalization/Less forget constraint / Inter-class separation 사용하여 해결하자.

[class imbalance 로 인하여 class embedding layer(마지막 classifer layer / softmax 이전 score layer)가 편향되었다.( BiC에서도 실험적으로 밝힘 )] </br>
- Imbalanced Magnitudes :  class embdedding(classifier / softmax 이전) layer가 new classes에 큰 value/magnitude/weight 를 가지고 있다. --> Cosine normalization
- Deviation : Imbalanced Magnitudes를 cosine normalization으로 정규화시킨 후, Distillation loss (feature extractor - embedding 간 cosine similarity)를 사용하려고 하였다. 하지만, feautre extractor - embedding 으로 계산하는 cosine similarity가 발생하는 문제(180도 shift된 상황에서 같은 각도 유지)가 있다. --> Less forget constraint
- Ambiguities : class embdedding vector가 old class 와 new class 겹치게 존재하여 애매하다. --> Inter-class separation 


