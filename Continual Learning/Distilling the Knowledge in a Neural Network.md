## 논문명 : Distilling the Knowledge in a neural Network

## KEY IDEA : Soft Target을 활용하여, cumbersome model의 Knowledge 를 small model 로 전달하자.

## Topic 1 : Soft Target을 활용한 Distillation 기법으로, cumbersome model의 Knowledge를 small model 로 전달할 수 있다. 
## Topic 2 : Specialist 를 활용하는 새로운 Ensemble 방법론을 제시할것인데, 아주 효과가 좋다. ( Specialist 가 곧 small model )
## Topic 3 : Soft Target은 Overfitting 을 방지하는 효과도 있으며, Speciallist 를 활용한 Ensemble 기법에 제격이다.

# Topic 1
## Soft Target 
- 복잡한 모델의 마지막에 softmax를 활용해서 one-hot encoding 되어 나온 결과를 Hard Target 이라 칭함.
- Hard Target 의 경우 정보손실이 많아, softmax 이전에 실수값을 사용하는 Soft Target 을 사용할것을 추천
- Soft Target 의 cross-entropy가 높다면, Hard Target 보다 더많은 정보와 gradient간 편차가 적다. 
- 따라서, Soft Target 의 cross-entropy가 높다면, small Data & higher learning rate 사용 가능

## Distillation 
- 마지막 softmax에서 T(temperature) 을 사용하여, 적절한 Soft Target을 만들어 내는 것.
- if T==1 : 일반적인 softmax 함수와 같아짐
- if T is higher : exponential 의 입력값이 작아지므로, 결과증가. [즉 , 큰값이 더 커지는것을 방지하여, 부드러운 분포 만듬 ] 
- <img width="308" alt="스크린샷 2022-03-21 오전 11 27 39" src="https://user-images.githubusercontent.com/98244339/159197937-982eecd7-6b12-49cf-b09c-f81007dc88c9.png">

## Distillation 위한 Two Objective Function
- First Objective Function : Soft Target 과의 Cross Entropy 사용 ( 단, cumbersome model 에서 만든 동일한 T 사용 , T ↑)
- Second Objective Function : Correct Lable 과 Cross Entropy 사용 ( T == 1 )
- [Second Objective Function 에 더 적은 가중치 두는것이 나은것을 발견함 ]

# Topic 2 
## 새롭게 소개할 Ensemble 기법 : Specialist Model의 활용
- classification이 복잡한 모델을 train 할때, ( 1 Generalist model + Many Specialist model ) 로 만들자.
- Generalist model : 일반적인것들 classification / Speciallist model : 구분하기 어려운것들 classification (ex.버섯의 종류)
- Specialist 의 softmax 는 분류하고 싶지 않은것들을 dustbin class 로 만들자.
- Specialist는 특정한 class 에 치중되어 훈련하고, 나머지들은 dustbin class로 만들기 때문에 overfitting 의 가능성이 농후함 --> Topic 3 
- Specialist 는 general model 의 weight로 initialization 후, special data ,general data 반반 섞인 데이터로  training
- <img width="524" alt="스크린샷 2022-03-21 오후 4 47 15" src="https://user-images.githubusercontent.com/98244339/159221531-418f97bc-8c94-4c21-b063-397b69580c20.png">

# Topic 3
## Soft Targets as Regularizers
- JFT 의 3% 만 가지고 hard target으로만 학습하면, overfitting 의 결과 지만, soft target으로 학습하면 overfitting 안일어난다.
- <img width="493" alt="스크린샷 2022-03-21 오후 4 50 17" src="https://user-images.githubusercontent.com/98244339/159221842-71c0e82d-bb8c-41b6-90f5-cf75ae0b71a2.png">

