## Key Point : Neural networks 에서, 중요한 weight 와 connections 만 학습하여, Accuracy 하락없이 모델 경량화하자.

## Key Step
1. Neural network에서 연결성 학습 ( 마지막 레이어 미학습, 어떤 레이어가 중요한가 학습 )
2. weight/connection 값이 지정한 threshold보다 낮은 모든 weight/connection 제거 ( to sparse layer )
3. sparse layer 재학습</br>
[ 2번 3번 iterative 반복 ]
<img width="837" alt="image" src="https://user-images.githubusercontent.com/98244339/161658280-cb0a2c0c-c0df-4ca0-9cc4-e59c0fcb377c.png">

## Other condition
- Regularization : L2 사용하는것이 우수(L1 사용하는것이 pruning관점에서는 우수하지만, retraing 까지 고려시 L2 우수 )
<img width="1066" alt="image" src="https://user-images.githubusercontent.com/98244339/161661865-2d1a8ed0-259c-48f8-9701-4ae1861fbc5a.png">


- Dropout Ratio Adjustment : Retraing 에서 사용하지만, 기존 사용하는 Dropout과 다르게 조정할 필요 있음</br>
[ Dropout은 inference 단계에서 값이 돌아오지만, Pruning 에서는 값이 영영 돌아오지 않는다. ] </br>
![IMG_2D239DF6AAA3-1](https://user-images.githubusercontent.com/98244339/161658771-e1e4af47-cc8c-4604-a4d1-c6dc4bba8f23.jpeg)

- Local Pruning and Parameter Co-adaptation : Retrain 단계를 위해, pruning에서 살아난 weight값 가지고있자

## Experiment
- LeNet_300-100 / LeNet-5 / AlexNet / VGG-16 에서 모두 좋은 성능을 유지하며, parameter 수를 획기적으로 줄였다.
<img width="964" alt="image" src="https://user-images.githubusercontent.com/98244339/161660500-1571a56c-7783-4538-9acc-f9dde2e7bd6b.png">

- Byproduct (Attention 효과) : 28*28 image 300장 (784*300)에서, 색칠된 부분 non-zero parameter 중심부분 
- <img width="680" alt="image" src="https://user-images.githubusercontent.com/98244339/161661804-a04c4f70-00cc-496e-8bd1-4c20057a4b4e.png">

- 타 모델과 비교 ( weight가 퍼지는 효과도 있음 )
<img width="987" alt="image" src="https://user-images.githubusercontent.com/98244339/161662201-3faedd6b-3a0c-442b-8e0b-b73763a87819.png">
