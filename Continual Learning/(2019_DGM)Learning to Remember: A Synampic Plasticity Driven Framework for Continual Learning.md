## Key Idea : GAN에 Sparse Attention Mask(HAT 개념)추가 & Dynamic network expansion mechanism 수행
- 본 논문을 보기전 ( 2018_HAT , 2018_DEN 을 먼저보아야함 )
- DGR과 다르게 매번 Generator 가 이전 data를 생성할 필요없이, Sparse attention mask를 통해 GAN만 추가적으로 학습

## Main Structure
![image](https://user-images.githubusercontent.com/98244339/167539484-26094f00-f608-4d69-94cf-5a64e650e54b.png)


## Learning Binary Masks ( Learning Sparse attention mask )
- GAN 을 학습시키는 동시에 Binary Mask도 같이 학습시킨다.
- 이후 mask를 학습시키는 방법은 --> 2018_HAT 논문참조

## 


