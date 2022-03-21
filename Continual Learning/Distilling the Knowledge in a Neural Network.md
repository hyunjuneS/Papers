## 논문명 : Distilling the Knowledge in a neural Network
## KEY IDEA : Ensemble 된 복잡한 모델의 지식을 single neural network 로 전달할 수 있다!
- 추가적으로 새로운 Ensemble 모델에 대해서 제시함 ( 모델이 잘 구분하지 못했던 모델에 대한 해결책 )

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

## Two Objective Function ( 두 목적함수의 가중평균을 사용하는것이 좋은것을 밝혔다고 한다. )
- First Objective Function : Soft Target 과의 Cross Entropy 사용 ( 단, cumbersome model 에서 만든 동일한 T 사용 )
- Second Objective Function : Correct Lable 과 Cross Entropy 사용
