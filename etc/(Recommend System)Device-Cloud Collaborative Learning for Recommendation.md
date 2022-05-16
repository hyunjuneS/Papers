### 추천시스템 과제
## KeyIdea : Device에서는 Meta-Patch Learning & Cloud에서는 mode-over-models distillation(MoMoDistill) 를 통한 Device-Cloud Collaborative Learning(DCCL) 제안

### 서론 
- 모바일 기기의 computing 능력이 향상되면서, 모바일 에서의 지능서비스로 확장되고 있다. device(모바일)에서 추천시스템을 적용한 다양한 방법이 있으며, 두가지 분류로 구분될 수 있다. 
- 전자 : On-device Inference 관점에서, pre-trained model 을 device에 옮겨 추론만 진행. ( cloud model )
- 후자 : On-device Learning 관점에서, device trainng된것을 합쳐서 centralized model 생성. ( device model )
- 전자(On-device Inference) 의 문제점: Centralized cloud model 은 보통 long-tailed sample을 무시하는 경향이 있다. ( 추천시스템에서 long-tailed & non-iid(device간 비균일성) 특성을 고려하지 않을 수 없다. )
- 후자(On-device Learning) 의 문제점 : device 별로 training 은 local optimization 에 빠질 수 있다.
- 저자의 의도 : device modeling 과 cloud modeling 을 jointly 이점 활용 

### Contribution 
- Device 와 Cloud 의 Collborative Learning Framework 제안
- Metapatch ( 'device' 개인화에 대한 sparsity 문제 고려 ) & MoMoDistill ( 모델간 Distillation 을 통한 'cloud' model 향상 )을 통한 DCCL 구현
- SOTA 모델들과의 비교에서 Outperform & 다양한 분석 ( long-tailed 유저들에서의 이점 & cloud-device 간 상호작용 내부 loop )

### DCCL Simple Framework
![image](https://user-images.githubusercontent.com/98244339/168507530-2eb7e374-cae0-4372-a4be-dd081032c9e5.png)

## DCCL Model
### MetaPatch for On-device Personlization
- 이전 몇몇 paper 에서, patch Learning을 통한 network finetning이 견줄 수 있는 성능을 보였다.
- 상기 연구에 착안하여, device 개인화를 위해 cloud model f에 patch model(Different Network Architecture) 을 삽입</br>
![image](https://user-images.githubusercontent.com/98244339/168508402-4b159eb6-25b3-4a5d-b80b-600f349efbb9.png)</br>
- 하지만, 여러 patch들이 상대적으로 커서 sparse한 local-data에 fit되지 않아, MetaPatch 방법론을 적용한다.
- MetaPatch는 metaLearning의 일환으로, 학습될 parameter를 줄이기위해 global paramter를 공유하는것이다. 
- 각 patch 의 parameter를 ![image](https://user-images.githubusercontent.com/98244339/168508851-5d4fe728-5739-4697-b40f-c28efa2d8c45.png) 로 표시
- 각 patch를 global shared parameter(device에서 freeze & cloud에서 Learning) 와 tunable parameter(metapatch parameter)로 분리가능하다. </br>
![image](https://user-images.githubusercontent.com/98244339/168509130-cd265332-36e3-476b-bcfd-b5081f2e84db.png)</br>
- 분리후, metapatch parameter 를 cross-entropy loss를 통해 학습한다.
- global shared parameter 의 학습과정은 MoMoDistill 에서 설명한다.</br>
![image](https://user-images.githubusercontent.com/98244339/168509647-5fab6385-ab3d-492f-aabd-aa2958581a91.png)</br>
![image](https://user-images.githubusercontent.com/98244339/168509997-8e2fd154-b2ce-481e-8fd9-43f7d03081f7.png)</br>


### MoMoDistill to Enhance the Cloud Modeling
- 기존에는 "model-over-data" 형식으로, device에 새로운 training data가 수집될때, 이전 model에 incremental learing 하는 방식.</br>
- W_f는 cloud netwrok parameter로, device modeling 과는 독립적이다. 기존식은 아래와 같다.
![image](https://user-images.githubusercontent.com/98244339/168510527-7ecc4001-e311-4ee5-ad33-dcbafb359832.png)

- 하지만, local 데이터를 학습할때, device에서 개인화를 하는것이 cloud에서의 학습보다 좋을 것이다.
- 이에(device model 의 가이드가 cloud modling 에 의미있는 도움을 줄것) 기반하여, "model-over-model" 방식을 제안한다.
- "model-over-model"방식은 [data를 통한 학습 & device model에서 기존지식 합성]을 동시에 진행한다. 
- 따라서, 모든 device model 에서 distillation loss가 추가된 term 사용한다.
![image](https://user-images.githubusercontent.com/98244339/168516345-77e53c6d-0e48-4c86-90a3-90c6d269b918.png)

![image](https://user-images.githubusercontent.com/98244339/168524053-c048e791-6bc0-428d-aeca-6cb98f952f7e.png)

### Global Shared Parameter Learning
- 앞선 Global Shared parameter 를 학습하는 과정에서, 상단 W_f 와 의미적으로 달라 local optimal 에 빠지게되어, 두단계로 나누어 진행한다.
- step1에서는 상단W_f를 optimization 하고, step2에서 학습된 cloud model(f)를 가지고 Global shared parameter 를 distill한다.
- cold-start issue 와 모든 device에서 metapatch의 이질적인 특성을 고려하여 보조 인코더를 사용한다.
- 보조 인코더는 기존 데이터 & device 별 user profile feature(eg age,gender .. ) & metapatch 를 조합하여 정의한다.
- 기존 metapatch parameter 대신 보조 인코더를 사용하여 패치를 정의하고, 첫단계에서 학습한 cloud 모델과 결합하여 proxy device model f(hat) 만든다. 
- 보조 인코더와 global shared parameter 에 대해 디바이스에서, f(hat) 과 실제 device model f 간 knowledge distill 수행.
![image](https://user-images.githubusercontent.com/98244339/168522457-55a132b9-5dc6-45a7-b5bc-205b9a7c4234.png)





