## Key Idea1 : new class가 들어왔을때, feature extractor 구조는 변하지 않고, classification(class embedding)layer 만 추가한다. 이후 distillation & cross-entropy loss 사용

## Key Idea2 : train 시에 data augmentation 을 사용하고, class imbalance 를 고려하여 exemplar를 통한 fine-tuning을 해준다.


## Main Structure
<img width="700" alt="image" src="https://user-images.githubusercontent.com/98244339/165653255-762f51a6-2dd8-464c-84b6-873a102fd3ea.png">

- Step1 . exemplar 와 new class 데이터 합치기
- Step2 . Train 과정으로, 상단에 classification + distillation 합쳐서 loss 구성 ( old class는 distillation & classification / new class는 classification만)
- <img width="400" alt="image" src="https://user-images.githubusercontent.com/98244339/165652410-c3e2aee2-bb26-4ebe-8934-bccdf84e8a6b.png">
- Step3 . old class 의 exemplar 크기와 같게, new class 를 줄여 fine-tuning ( new class를 줄일때 대표이미지는 포함되도록, herding selection 사용 )
- Step4 . representative memory updating   
