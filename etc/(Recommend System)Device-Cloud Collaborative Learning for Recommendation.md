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


