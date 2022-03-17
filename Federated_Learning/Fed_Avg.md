# 논문명 : Communication-Efecet Learning of Deep Networks from Decentralized Data

## Fed Avg : combines local SGD on each client with a server that performs model averaging.
## Federated Learning 특징
- 실제상황의 real-data를 학습하는것이 보편적으로 공개된 data를 학습하는것보다 나음 
- 모델 학습을 위해 데이터센터에 기록하지 않는것이 좋음
- 사용자들에 의해 지도학습을 위한 label 이 생겨날 수 있음.
  
## Federated Optimization 
- Non-IID : 각 client별 가지고있는 데이터의 분포가 서로 다를 수 있다.
- Unbalanced : 특정 client가 다른 client에 비해 더 많은 비중을 차지할 수 있다.
- Massively distributed : client별 데이터보다 client가 더 많을 수 있다.
- Limited Communication : 모바일 기기가 오프라인, 느려지거나, 과도하게 연결이 많이될 수 있다.

## Goal : Using additional computation in order to decrease the number of rounds of communication needed to train a model.
- increased parallelism : computation 동일한 client를 늘려서, 전체 additional computation 증가로 할것인가?
- increased computation of each client : 개별 clinet의 computation 을 늘려서, 전체 additional computation 증가로 할것인가?
- 실제 사용할때는, client를 늘리는것에 큰 비용이 들지않아, 먼저 client를 늘려보고 계산량을 늘려본다. 

## Fed SGD vs Fed Avg
- Fed SGD ( parameter : C ) <br/>
: 임의 선택된 client, client 별 모든 데이터 가 batch로 계산되어( batch = ∞) , 1번 계산하여 1번 업데이트 ( epoch = 1 ) <br/>
- Fed Avg ( parameter : C , B , E ) <br/>
: 임의 선택된 client, client 별 batch 크기 선정( batch 선정 ) , n 번 계산하여 1번 업데이트 ( epoch 선정 ) <br/>
<br/>
- if B == ∞  and E ==1 : <br/>
           Fed SGD = Fed Avg


## Fed Avg's key parameters
- C : the fraction of clients that perform computation on each round ( ex. C = 0.1 , 0.2 ,  0.5 ... ) 
- E : Epoch
- B : local minibatch size ( for client updates ) 

## Weight Initialization 
- 모델 w , w' 의 가중치를 동일하게 초기화시켜주어야 효과가 좋다.
- <img width="332" alt="스크린샷 2022-03-14 오후 6 23 09" src="https://user-images.githubusercontent.com/98244339/158142908-013f5033-0003-40a6-a599-b0ebf7863618.png">

## Algorithm
- <img width="757" alt="스크린샷 2022-03-15 오전 9 03 16" src="https://user-images.githubusercontent.com/98244339/158280397-a23a2abb-ba1b-44a3-ab07-a0f59df5a354.png">

## Effect of increased parallelism ( Controls the amount of multi-client parallelism )
- c 에 따라서 client 숫자 변경, client 10 이상으로는 크게 변동없어 이후 실험에서는 C = 0.1. 고정
- <img width="770" alt="스크린샷 2022-03-15 오전 9 11 56" src="https://user-images.githubusercontent.com/98244339/158281167-9753f85d-2385-4bb8-a702-c923243ed39e.png">

## Increasing computation per client ( u : round & client 당 업데이트 횟수 )
- <img width="601" alt="스크린샷 2022-03-15 오전 10 22 38" src="https://user-images.githubusercontent.com/98244339/158287452-f6c44d6d-1f6e-421c-985c-019accb5f4cc.png">

## Regularization benefit
- communication rounds 를 줄이는것 뿐만아니라, Dropout의 효과로도 Fed Avg는 training loss도 줄인다.
- <img width="558" alt="스크린샷 2022-03-15 오전 11 03 07" src="https://user-images.githubusercontent.com/98244339/158291235-53494108-303c-4497-9681-aa2ba89ebc80.png">

## Local Datasets Epoch & TrainLoss
- Local Datasets의 epoch 가 많아지면, FedAvg 는 plateau ? diverge ? ( 정체되거나 갈라진다? ) , 여튼 안좋다
- 수렴의 후반단계에서는 Decaying learning rate와 같이, local computation을 줄이는것이 좋다. (Batch size를 크게하거나 or Epoch를 줄이는것)
- <img width="643" alt="스크린샷 2022-03-15 오전 11 21 12" src="https://user-images.githubusercontent.com/98244339/158293081-38861e6b-06c3-417f-a7e2-4a0a7a31b56d.png">
- mnist cnn 에서는 E가 커짐에 따라 의미있는 변화가 없지만, language model 에서는 의미있는 변화가 있음 ( 아무래도 language model 은 non-iid가 자연스레 들어가있는것 때문이 아닐까..? ) 
- ![IMG_1EAE24575F9A-1](https://user-images.githubusercontent.com/98244339/158294267-bf9639ee-de07-4490-b641-e298b4b4966d.jpeg)


