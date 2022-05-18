## Key Idea : Unlabeled Data 활용 & Global Distillation 수행
- 쉽게 대량으로 구할 수 있는 Unlabeled Data를 confidence-based sampling method 를 활용하여 Sampling
- Global Distillation 을 단계에 걸쳐 진행</br>
![image](https://user-images.githubusercontent.com/98244339/168972782-e2f9969d-7ea4-4e09-aad0-f12830717998.png)

### Before Using Unlabeled Data..
- Intuition : Unlabeled Data가 previous task와 유사할 가능성이 있다.
- 하지만, 야생에서의 Unlabeled Data가 previous task와 항상 연관성이 있는것은 아니기에, 유용한 정보가 있는지 찾는것이 중요하다. 
- 이를위해 sampling 이 중요하고, 효율적인 sampling strategy를 위해, Out-Of-Distribution(OOD) sample 을 활용여 [confidence-calibrated model] 를 제안한다.
- OOD에서의 Unlabeled data를 활용하여야만 confidence-calibrated model을 만들 수 있다.

## Main Method
### Basic Learning objectives
![image](https://user-images.githubusercontent.com/98244339/168977937-e90b54c7-4800-4894-9aa8-d829c5788134.png)

## Method
### Claasification Loss </br>
![image](https://user-images.githubusercontent.com/98244339/168978319-3ae4051c-7a26-49b0-a672-472b5fe5c61a.png)</br>
### Global Distllation Loss : 이전모델(P) , Teacher model(C) , Ensemble (Q) 을 통해  Global Distillation 적용
- task간 knowledge distillation (local Distillation) 대신, Reference model 을 Global하게 Distillation 사용 (Unlabeled Data를 사용한다는 의미인가...)</br>
![image](https://user-images.githubusercontent.com/98244339/168979739-219a487b-92eb-4347-8c60-c2efa74b8e30.png)</br>
- 하지만 1번의 classification loss와 2번의 Distillation loss 만 사용하면, 현재 task에 대해서 잘 학습하지 못한다.
- 이를 해결하기위해 teacher model(C)를 현재 task에 만 학습시킨다.</br>
![image](https://user-images.githubusercontent.com/98244339/168980325-8d36248d-bcc6-4221-82ff-dade04ceae39.png)</br>
- 위식은 teacher model(C)를 학습시킨다는 의미로, 아래와 같이 classification loss를 현재 task의 데이터만 가지고 학습시킨다.
- ![image](https://user-images.githubusercontent.com/98244339/168980509-47dcc067-3cb5-403f-a5cd-3f6eef31aa90.png)

- 한편, Teacher model(C)은 현재task(t) 에서 classification, 이전모델(P)은 이전task(1~t-1)까지 classification 가능
- 이전task(1~t-1) 와 현재 task(t)를 구별하기 위한 조치가 필요하고, 두모델을 앙상블 하여 해결한다.</br>
![image](https://user-images.githubusercontent.com/98244339/168982045-4a392a40-7fea-44c1-9039-1bd88a4d94d5.png)</br>
- 앙상블을 적용한 모델에 Unlabeled Data만 사용하여, Distillation loss 사용 ( 첫 classfication 식에서 같은 범위로 사용이되었음 )</br>
![image](https://user-images.githubusercontent.com/98244339/168982463-2cbf4461-b8ad-4f25-a9d4-b42256cadef0.png)

- [Total Global Distillation Loss] </br>
![image](https://user-images.githubusercontent.com/98244339/168982679-3b332f13-060a-4971-a15a-e379dc6f9b85.png)

### Blanced fine-tuning
- classifier layer 의 bias를 막기위해 classifier만 fine-tuning 해준다. 
- fine-tuning할때 data weighting 한다.( 계산된 gradient를 scaling & weight를 normalize 한다.) </br>
![image](https://user-images.githubusercontent.com/98244339/168983664-c5eea75a-4084-4ead-9dd7-82fdedceed8f.png)




3. 
