## Key Point : Neural networks 에서, 중요한 weight 와 connections 만 학습하여, Accuracy 하락없이 모델 경량화하자.

## Key Step
1. Neural network에서 연결성 학습 ( 마지막 레이어 미학습, 어떤 레이어가 중요한가 학습 )
2. weight/connection 값이 지정한 threshold보다 낮은 모든 weight/connection 제거 ( to sparse layer )
3. sparse layer 재학습</br>
[ 2번 3번 iterative 반복 ]
<img width="837" alt="image" src="https://user-images.githubusercontent.com/98244339/161658280-cb0a2c0c-c0df-4ca0-9cc4-e59c0fcb377c.png">

## Other condition
- Regularization : L2 사용하는것이 우수(L1 사용하는것이 pruning관점에서는 우수하지만, retraing 까지 고려시 L2 우수 )
- Dropout Ratio : Retraing 에서 사용하지만, 기존 사용하는 Dropout과 다르게 조정할 필요 있음</br>
[ Dropout은 inference 단계에서 값이 돌아오지만, Pruning 에서는 값이 영영 돌아오지 않는다. ] </br>
![IMG_2D239DF6AAA3-1](https://user-images.githubusercontent.com/98244339/161658771-e1e4af47-cc8c-4604-a4d1-c6dc4bba8f23.jpeg)


