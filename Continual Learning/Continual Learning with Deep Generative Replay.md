## Key Idea : Gernative model 이용하여 rehearsal 메모리 만들자.

- Scholar model (Generator & Solver) 을 통해서, fake data와 target 을 만들 수 있다.
- 이 쌍을 통해서, 새로운 데이터와 함께 보면서 Scholar model(Generator & Solver)을 학습시키자.
- 해당 논문에서느 GAN을 통한 Generative model 만들었지만, vae나 다른 모델 사용해도 무관함

## Gan 의 objective function
<img width="941" alt="image" src="https://user-images.githubusercontent.com/98244339/162859571-5090b60f-961d-462f-be8e-ae986f6c72a7.png">

## 모델의 전체 objective function 과 몇몇 정의
<img width="1180" alt="image" src="https://user-images.githubusercontent.com/98244339/162860500-14bee04b-fcff-4392-9724-bd3ba58f015d.png">

## 모델의 구조

- Scholar model Generator & Solver) 을 학습하는 것은 generator 와 solver를 독립적으로 학습하는 것이다.
- [Generator 학습]
- 먼저 새로운 Generator는 새로운 task의 input x 와 이전 task에서 재생된 x'을 받고 적절히 섞인다.
- Genrator 는 새로 들어온 input x까지 고려한 input 공간을 재생시키기 위해 학습한다.
- [Solver 학습]
- 실제 데이터(x,y)와 재생된 데이터(x',y')의 input과 target을 학습한다.
- 재생된 타겟데이터(y')은 이전에 solver에서의 x'에 대한 output이다.
- 


