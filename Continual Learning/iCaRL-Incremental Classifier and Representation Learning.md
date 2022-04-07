## Key Idea : classifier 와 representation(feature extraction , θs) 을 동시에 learning 할 수 있다.

## Class-Incremental 의 3가지 특징
1. 다른시간에 발생한 다른 class의 데이터를 학습할 수 있어야 한다.
2. 지금까지 본 class까지 multi classification할 수 있어야 한다.
3. 지금까지 본 class의 수와 관련하여, computation 과 memory는 매우 천천히 증가하거나 그 주변이여야 한다.

## iCaRL 구성요소
1. Nearest-mean-of-examplars ( Classification )
2. Prioritized examplar selection
3. Knowledge distillation and prototype rehearsal ( Representation learning )

## Classification (by Nearest-mean-of-examplars)
![image](https://user-images.githubusercontent.com/98244339/162116920-2820e658-730f-405f-9515-40889dc05355.png)

## 전체 Training 과정
- X1 ~ Xs-1 까지는 기존에 학습이 되었고 P1~Ps-1 까지의 examplar(각 n개)로 저장되어 있다. Xs ~ Xt 의 class를 새로 학습한다고 가정.
- memory size는 K로 고정되어 있으며, 해당 모델이 가지고있을 수 있는 이미지는 총 K개 이다.
- Xs ~ Xt 의 새로운 class와, 기존examplar 를 가지고 Representation(feature extraction)을 학습 ( UPDATE REPRESENTATION )
- class의 갯수가 많아져서 기존에 n개씩 저장했다면, examplar의 크기를 m개씩 으로 줄여야함 ( n > m )
- 기존에 P1~Ps-1 까지의 examplar크기 감소시키기 ( n -> m , REDUCE EXAMPLAR )
- Xs ~ Xt 의 새로운 class의 examplar 생성 ( 각 m 개 CONSTRUCT EXAMPLAR SET)
![image](https://user-images.githubusercontent.com/98244339/162118944-703508f3-453a-48a7-877b-9ef9b30dedfc.png)

## Training Architecture
- 기본적인 feature extractor 는 CNN 구조이고, classfication layer는 class별 sigmoid 함수로 구성되어 있다.
- class별 sigmoid를 사용하여 classification 하는것은 training 을 위한 용도로서, inference시에는 상단에 Nearest-mean-Examplars 사용
- feature extraction part의 paramter : ![image](https://user-images.githubusercontent.com/98244339/162119950-706cd7a1-f25a-4f86-943f-dcdc3773158c.png)
- sigmoid 이전의 마지막 weight vector : ![image](https://user-images.githubusercontent.com/98244339/162120815-e50074ef-e477-4c0d-8d9f-8d18c521e9af.png)
- ![image](https://user-images.githubusercontent.com/98244339/162122921-d52ca5bc-2fd0-458e-836c-038281026c5e.png)

## 실질적인 학습 ( 전체 Training 과정 , UPDATE REPRESENTATION )
- ![image](https://user-images.githubusercontent.com/98244339/162133246-ef351620-1365-4dfa-9fa9-5c41dedb6592.png)

## 새로운 class의 examplar 생성 ( CONSTRUCT EXAMPLARSET )
- 각 class를 대표할 수 있는 이미지 ![image](https://user-images.githubusercontent.com/98244339/162139214-49cff028-ba82-443c-b4f9-431f1019cee5.png) 중에서, 가장 작은 차이를 가진 이미지부터 앞부터 쌓아간다. 
- examplar의 크기를 줄여야할때 뒤에서 부터 없애버리면 된다.

![image](https://user-images.githubusercontent.com/98244339/162135909-e096a2bd-e7eb-4ab9-89c6-27a2260e0ac7.png)

## 기존 P1~Ps-1 까지의 examplar 갯수 감소 ( REDUCE EXAMPLAR SET )
![image](https://user-images.githubusercontent.com/98244339/162139002-169a867a-d741-481a-9b4b-2310fc1e414f.png)


