## Key Idea : Partially Labeled data 사용하여, GAN & Classifier 동시 학습하는 deep Online Replay with Discriminator Consistency (ORDisCo) framework를 Semi-supervised Continual Learning 분야에 제안
### ORDisCo 를 위한 2가지 방법론
1. GAN에서 생성된 데이터가 실시간으로 Classifier에 들어간다.
2. Unlabeled data의 정보를 잃지 않기위해, Discriminator 를 안정화한다.

## 서론
#### 기존에 Few-Shot Continual Learning & Unsupervised Continual Learning과는 다르게, new-class만 학습하는 것이아닌, new-class 학습과 old-class 를 위한 instance도 같이 학습한다.
- Unsupervised memory buffer(UMB) 를 사용함에도 Supervised memory buffer(SMB) 을 사용하는 것만큼 성능 향상을 보이지 못함
- 즉, Semi-supervised Continual Learning의 scenario 의 문제점은 Unlabeled data를 제대로 이용하지 못하는데에 있다.
- 아래 그림은 MT Classifier(Mean Tree 라는 Semi-supervised learning 방법론중 하나)를 사용하여 여러 Continual Learning 전략을 비교 한것. </br>
![image](https://user-images.githubusercontent.com/98244339/169953153-c0db46de-a13e-4896-8c4d-6cad0bfcfd50.png)

## Method
- A 단계를 통해 i-batch 에서 학습하고, i+1 batch 학습할때, Unlabeled information 을 잃지 않기위해 B단계 진행 
### Classifier & Discriminator & Generator Training on the Incremental Semi-supervised data ( A )
##### Classifier(C)
- Classifier 역할 : Classification & Generate pseudo-label for GAN(D,G) </br>
- (2) term : Supervised loss (cross-entropy)
- (3) term : Unsupervised loss (consistency-regularization) / (Mean Teacher... 을 읽어봐야 자세한 term 알수 있을듯..) </br>
![image](https://user-images.githubusercontent.com/98244339/169957057-f6b6c6e2-0250-4bb9-b78d-8eb15ff17e54.png)

##### Discriminator(D)
- Discriminator 역할 : Training data(data-label) vs Fake data(Generated data - pseudo label) 구별
- 첫번째 term : Labeled training data 의 GAN loss
- 두번째 term : Generated data 의 GAN loss
- 세번째 term : pseudo label & unlabeled batch loss</br>
![image](https://user-images.githubusercontent.com/98244339/169957905-481df3d0-e872-4ed2-9026-5608801d30b0.png)

##### Generator(G)
- GAN loss function</br>
![image](https://user-images.githubusercontent.com/98244339/169957994-be16f6bc-fee9-4bbf-9dac-b0b555536b0d.png)


### Mitigating catastrophic forgetting of the Unlabeled data ( B )
- Unlabeled data의 지식을 보존하기 위해서 두가지 전략 사용 ( online semi-supervised generative replay & stabilization of discrimination consistency )

##### Online semi-supervised generatvie replay
- 실시간으로 




