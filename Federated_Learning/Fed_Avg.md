## 논문명 : Communication-Efecet Learning of Deep Networks from Decentralized Data

- Fed Avg : combines local SGD on each client with a server that performs model averaging.
- Federated Learning 특징
1. 실제상황의 real-data를 학습하는것이 보편적으로 공개된 data를 학습하는것보다 나음 </br>
2. 모델 학습을 위해 데이터센터에 기록하지 않는것이 좋음
3. 사용자들에 의해 지도학습을 위한 label 이 생겨날 수 있음.
  
- Federated Optimization 
1. Non-IID : 각 client별 가지고있는 데이터의 분포가 서로 다를 수 있다.
2. Unbalanced : 특정 client가 다른 client에 비해 더 많은 비중을 차지할 수 있다.
3. Massively distributed : client별 데이터보다 client가 더 많을 수 있다.
4. Limited Communication : 모바일 기기가 오프라인, 느려지거나, 과도하게 연결이 많이될 수 있다.
