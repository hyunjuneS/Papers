## Key Idea : 이전에 학습된 network에서 현재 task와 관련있는 부분만 update (selectively retrain) / 필요한 경우에 따라 network를 확장 (expanding capacity)

## Main Structure
![image](https://user-images.githubusercontent.com/98244339/167327580-1829256c-f016-4930-983c-9c38d3f88ba1.png)

## DEN 의 Algorithm
- 초기(t=1)에는 L1 Regularization 사용해서 weight의 sparisity 를 만든다. </br>
[ Main Algorithm ] </br>
- ![image](https://user-images.githubusercontent.com/98244339/167328299-b117b81c-46db-4621-b432-b81d7f2b891d.png)


[ Algorithm : Selective Retraining ] </br>
- sparse한 model에 새로운 task를 적용하기 전에, 최상위 hidden units만 사용해서 sparse linear model(subnetwork) 을 찾는다. (Eq.3)
- 그 후, selected subnetwork S를 학습한다.(Eq.3) (L2 Regularization)
- ![image](https://user-images.githubusercontent.com/98244339/167331121-a23d5884-6415-47b2-9058-5c6439003b64.png)


[ Algorithm : Dynamic Network Exapnsion ] </br>
- Selective Retraining 과정 이후, loss가 threshold 보다 클때, Dynamic network Expansion 한다.
- network 를 확장하고자 할때, 몇개의 노드를 추가할지 결정하기 위해 group sparse regularizaion 사용한다. (Eq.5)
![image](https://user-images.githubusercontent.com/98244339/167332464-71ebad79-db74-4c45-a3cf-e9389a751848.png)


[ Algorithm : Network split and Duplication ] </br>
- 이전 network 의 weight와, 새로운 network 의 weight가 차이를 적게하기 위해, L2 distance 사용
- weight간 L2 Distacne 값이 threshold 보다 크다면, weight를 2개 copy 하여, 재학습
- copy할때는 현재 task t에 대해서 기록해놓은 다음, inference 시에 참조하여 사용한다.
![image](https://user-images.githubusercontent.com/98244339/167333454-88e6db25-3a52-4308-adac-fda79aadf9aa.png)






