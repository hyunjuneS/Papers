## Key Idea1 : new class가 들어왔을때, feature extractor 구조는 변하지 않고, classification(class embedding)layer 만 추가한다. 이후 distillation & cross-entropy loss 사용
## Key Idea2 : train 시에 data augmentation 을 사용하고, class imbalance 를 고려하여 exemplar를 통한 fine-tuning을 해준다.
