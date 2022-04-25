## key idea : class imbalance를 해결하기 위해, validation set로 간단한 linear layer를 학습하여 문제를 해결하자. 

## class imbalance 란 ? 
- iCaRL 에서 제시한 exemplar를 가지고 있을때, 분류해야할 class가 많아지면, exemplar가 적어진다.
- 상대적으로 많은 수의 training data를 학습할때, 학습할 training data보다 exemplar 가 적어지는 상황

## 시작하기 앞서..
- 해당문제를 해결하기 앞서, 저자는 마지막 fully connected layer가 new classes에 편향되었다는 것을 발견하였다.
- 이와 관련한 실험은 아래와 같다.
- baseline (파랑) : 아무것도 하지 않았을때 accuracy가 감소하는 모습
- 녹색 : 모든 데이터를 네트워크에 제 학습했을 때 최고의 성능
- 주황색과 빨간색이 별 차이가 없는데, 주황색은 feature & fc 모두학습 / 빨간색은 feature freeze 후 fc만 따로 학습
- 오른쪽 그림은 80~100 마지막 학습한 클래스에 편향된 모습을 보여준다.
- ![image](https://user-images.githubusercontent.com/98244339/165013186-2e2c02c5-453a-4c43-8658-9ac817190a62.png)

## Main
- 크게 Step1 과 Step2 로 나뉠 수 있음. Step1에서는 마지막 FC이전까지 Distillation loss(old 클래스 분류용) / CrossEntropy loss(new 클래스 분류용) 로 학습한다.
- Step 2에서는 2parameter로 linear model을 학습한다.

- Step1 에서는 exemplar와 new data에서 train 데이터 ( 실험적으로 9:1(train 9 , val 1) 이 좋다고함 )로 학습
- Step2 에서는 exemplar와 new data에서 validation 데이터 로 학습/ Step2 단계에서 convoution과 FC 모두 freeze시키고 softmax crossentropy 사용하여 학습한다.

![image](https://user-images.githubusercontent.com/98244339/165014732-0959e5f0-8610-4fa6-b495-268778af136a.png)


## Experiment
![image](https://user-images.githubusercontent.com/98244339/165015772-4a152f7e-12b3-4450-97d3-c741b5986151.png)


