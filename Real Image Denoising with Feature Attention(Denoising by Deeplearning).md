## 해당 논문을 22-1 영상처리 수업의 과제로, Denoising by Deeplearning 관련 논문이다.

## Abstract
- Deep convolutional neural networks는 invariant noise가 포함된 이미지(synthetic-image) 에서는 잘 동작하지만, real-noisy image에서는 잘 동작하지 않는다. 
- 저자는 Denoising알고리즘의 실용성을 높이기 위해, residual(잔차)과 feature attention이라는 개념을 적용한 ‘RIDNet’을 제시한다.

## Introduction
- Image Denoising은 저차원의 필수적인 Vision task 중 하나이다. 
- 일반적으로 Denoising알고리즘으로 model-based와 learning-based로 분류된다. 
- model-based알고리즘은 계산적으로 비싸고, 많은 시간이 소요되며, variant noise를 직접적으로 줄이기 어렵다. 
- Learning-based알고리즘 또한 성능이 제한적이고 특정 noise수준에 맞춤형으로 작동한다.

- 즉, 실용적인 Denoising알고리즘은 efficient하고 flexible해야 하며, variant noise이던 invariant noise모두 다룰 수 있어야 하지만, 현재 SOTA알고리즘은 상기 목표를 만족시키지 못한다. 
- 우리는 efficient하며 synthetic-image, real-image모두 다룰 수 있는 CNN모델을 제시한다.


## Contributions
A.	현재 CNN기반 real image denoising알고리즘은 두 단계 모델이 필요하지만, 해당 모델은 오직 한 단계만 사용하여 SOTA결과를 제공한다.
B.	해당 모델은 Image Denoising분야에서 feature attention을 적용한 최초의 논문이다.
C.	해당 모델은 modular network를 제시하며, 모듈의 개수를 통해 성능을 향상시킬 수 있다.
D.	정량적 정성적으로 SOTA결과와 비교하기 위해 3개의 synthetic-image dataset과 4개의 real-image datasets으로 실험하였다.


## Related Works
- Image Denoising관련 많은 모델이 나와있고, 현재는 real-image Denoising에 많이 집중되어 있다[Reference 50,31,12]. 
- Reference [64,63,35]에서 제시한 알고리즘으로 CNN 모델링 가능성을 보았고, single-blind denoising을 학습하는 능력을 보여주었다. 
- 하지만, denoising performance는 아직 제한적이며 real-image에서 만족할 만한 수준에 오지 않았다.
- 최근 ‘CBDNet’ 은 real-image로 blind-denoising모델을 제시하였다. 
- ’CBDNet’또한 일반적인 real-image Denoising 분야와 비슷하게, noise estimation과 non-blind-denoising의 두 sub network로 구성되어 있다. 
- ‘CBDNet’은 synthetic-image noise와 real-image noise에 대해 학습하도록 설계되었으며, 결과 향상을 위한 수동개입이 필요하다. 
- 하지만 우리가 제시하는 모델은 end-to-end모델이며, sub-nets와 수동개입 없이 noise를 학습하고 결과를 만들어낸다.


## CNN Denoiser
Network Architecture
- 우리의 모델은 3가지(feature extraction, feature learning residual on the residual module, reconstruction)의 main modules을 갖는다. 
- Loss function으로는 L1 loss(식 4)를 사용하며, feature extraction과 reconstruction module은 reference[21,8]에서 제시한 모듈과 비슷하다.
A.	feature extraction: 하나의 convolutional layer로 구성 (식 1)
B.	feature learning residual on the residual module: 여러 EAM(Enhancement attention module) 구성 (식 2)
C.	reconstruction: 하나의 convolutional layer로 구성 (식 3)
![image](https://user-images.githubusercontent.com/98244339/161673448-e28b5e2f-9f4d-4b20-b840-74c6e78c41e6.png)
![image](https://user-images.githubusercontent.com/98244339/161673454-9201e1ed-1b56-4698-9d7e-d72a213fb5d0.png)
![image](https://user-images.githubusercontent.com/98244339/161673458-169f552f-5533-488b-8e6e-cbf337a09e3b.png)
![image](https://user-images.githubusercontent.com/98244339/161673462-437a0345-aaaa-4c01-abde-2c1677dca8d8.png)
![image](https://user-images.githubusercontent.com/98244339/161673465-bb20ab98-b4ac-42c4-b3c9-33dddf71f969.png)


## Feature learning Residual on the Residual
- Residual on the Residual structure는 denoising성능을 향상시키기 위해 더 깊은 네트워크를 만들 수 있지만, 저자가 제시하는 모델은 4개의 EAM module을 활용하였다. 
- EAM에 대하여 자세한 구성을 다루기에 앞서, 간략한 구조는 input feature를 학습, 압축, 가중치 강화로 나눌 수 있다.

- 먼저, input feature는 확장된 2개의 convolution으로 나뉘고 합쳐진 후에 또다른 convolution layer를 통과한다. 
- 그 후, 두개의 convolution residual block을 통과하여 feature가 학습된다. 
- 압축을 위해 세개의 ERB(Enhanced residual block) convolutional layer을 통과한다. ERB의 마지막 레이어에서 1*1 kernel을 통과하여 flatten시킨다. 
- 마지막 feature attention의 output에 EAM input을 추가한다.

- 저자는 EAM의 input에 이전 EAM의 output을 활용하여 모델을 깊게 만드는 것을 제시한다(식 5). 
- 또한, 연속적인 residual model의 성능이 좋지 않다는 결과를 바탕으로, 쌓인 module의 맨 마지막 output에 feature extractor module의 input을 추가하는 것을 제시한다(식 6). 
- 또한, noise가 제거된 이미지보다 noise를 학습하기 위해 network output에 input image를 추가하는 것을 제시한다. 
![image](https://user-images.githubusercontent.com/98244339/161673557-ef849cb1-d001-4d1c-8cb8-5e403fbcc19d.png)
![image](https://user-images.githubusercontent.com/98244339/161673564-b4758d9b-e514-455b-bd96-c4f24060ac4c.png)
![image](https://user-images.githubusercontent.com/98244339/161673566-995e5a78-e90a-4c41-9599-fb0e1365b458.png)


## Feature Attention
- Attention을 활용하기 위해 각 채널별로 attention을 어떻게 다르게 생성할지 고민해야 한다. 
- Convolutional layer는 local information만 활용하고 global information은 활용하지 못한다. 
- 먼저, 전체 이미지의 통계적 분석을 위해 global average pooling을 수행한다(식 7). 
- 그 후, global average pooling에서 생성된 channel dependencies를 파악하기 위해 self-gating mechanism을 수행한다. 
- Self-gating mechanism을 위해서는 soft-shrinkage 와 sigmoid function이 필요하다(식 8). 여기서 sigmoid의 output은 input channel feature에 의해 조정된다(식 9)
![image](https://user-images.githubusercontent.com/98244339/161673621-4803fee1-a930-4d22-aab6-59c4833f7749.png)
![image](https://user-images.githubusercontent.com/98244339/161673629-b963db9b-5bea-4454-a76d-174a2b507b17.png)
![image](https://user-images.githubusercontent.com/98244339/161673631-9aaf165d-4a49-42dd-820f-79af16d8851d.png)
- (식 8)의 Hu 와 Hd는 각각 channel up-sampling 과 channel reduction 이다.
![image](https://user-images.githubusercontent.com/98244339/161673641-de7b4801-2013-4dee-86c0-1be43bc0ac81.png)


## Implementation
- 해당 모델은 총 4개의 EAM module을 포함한다. Kernel size는 ERB 마지막 채널을 제외하고 3*3 이며, 3*3의 output feature map을 유지하기 위해 zero-padding을 사용한다. 
- 각 convolutional layer channel은 feature attention downscaling을 제외하고는 64개이며, 해당 모델은 512*512 이미지를 처리하는데 약 0.2초가 소요된다.

## Experiment
- Influence of the skip connections and Feature-attention
![image](https://user-images.githubusercontent.com/98244339/161674001-b77ecd4a-d3a5-4de1-8ac2-cd2616e9d0bf.png)
상기 실험에서는 skip connection과 feature attention의 영향에 대하여 실험하였다.</br>
Skip connection을 사용할 수 있을 때 좋은 성능을 얻을 수 있었고, skip connection이 없을 때는 네트워크 깊이를 늘리는 것도 성능에 도움이 되지 않는다. </br>
또한, feature attention을 사용한 것에서 더 좋은 성능을 보였다.</br>

- Synthetic noisy image test
![image](https://user-images.githubusercontent.com/98244339/161674072-eb0531ad-8474-4358-87e1-d379c89166c1.png)
![image](https://user-images.githubusercontent.com/98244339/161674076-edd5ea22-d360-4fe1-975b-5829e0c7acb6.png)
Set12와 BSD에서의 성능이 가장 좋다는 것을 알 수 있었다. 또한, 아래와 같이 channel이 포함된 데이터에서도 시각적으로 및 수치적으로 우수한 성능을 보여 주었다.
![image](https://user-images.githubusercontent.com/98244339/161674093-b3bf9863-af0d-4615-a4cd-9cf9bcf1e5c5.png)
![image](https://user-images.githubusercontent.com/98244339/161674100-4de83f69-96a0-4f30-9e5f-206d3d9d1fb4.png)

- Real-World noisy images
Real-noisy image dataset인 RNI15에서는 실제 이미지가 존재하지 않아 정량적 비교가 불가능하지만, 타 알고리즘과 비교해보아도 훨씬 우수한 성능을 내는 것을 알 수 있다.</br>
![image](https://user-images.githubusercontent.com/98244339/161674110-d3bf0bde-ac6d-4255-ac66-003a2098cf99.png)
![image](https://user-images.githubusercontent.com/98244339/161674118-bf4cab64-a776-4da3-841d-f8aa94c24783.png)
![image](https://user-images.githubusercontent.com/98244339/161674128-856076b7-1f1c-4ffd-a642-109eef1e7e1a.png)
![image](https://user-images.githubusercontent.com/98244339/161674130-a4dd35f0-7e22-4994-abe2-94a7e9c22224.png)
Real-noisy image dataset인 Nam과 SSID에서도 정량적 및 시각적으로 우수한 성능을 보였다.
![image](https://user-images.githubusercontent.com/98244339/161674134-3b2578d0-bc5c-4bef-b89d-9af26c30d45e.png)
![image](https://user-images.githubusercontent.com/98244339/161674139-8c521b6c-8ed4-477d-ae77-142ff32dfb86.png)





