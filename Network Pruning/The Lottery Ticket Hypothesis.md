## Key Idea(The Lottery Ticket Hypothesis) : Dense,randomly-initialized,feed-forward 네트워크는 sub-network를 가지고 있고, 이 sub-nerwork를 잘 학습시키면 비슷한 iteration안에서 같은 성능을 내게할 수 있어 ( sub-network : lottery ticket or winning ticket )

## Hypothesis 의 Formally Expression 
<img width="1248" alt="image" src="https://user-images.githubusercontent.com/98244339/161872503-a5fbc427-8268-454d-b9eb-a58a4e483612.png">


## 기존 문제점
- pruning 된 architecture는 학습하기 어렵고, 학습하여도 original network보다 성능에 못미친다.

## Identifying winning tickets.
Step1 . 랜덤하게 초기화(θo)된 네트워크 학습한다.<br/>
Step2 . j번 iteration결과 파라미터가 θj로 된다.<br/>
Step3 . p%로 pruning 한다. (0과1로 이루어진 행렬 m을 만들 수 있다.)<br/>
Step4 . 남아있는 네트워크를 Step1 에서 초기화 했던 θo로 초기화 한다.<br/>
[실질적으로 사용할때는 한번에 p%로 pruning하기보다는 iterative 하게 pruning한다.]</br>
<img width="961" alt="스크린샷 2022-04-06 오전 9 35 50" src="https://user-images.githubusercontent.com/98244339/161872917-153d190c-5286-488d-ba5d-cfe30076e4d7.png">

## Result
- 적절한 p%로 pruning 된 lottery ticket(winning ticket)이, 적은 iteration 안에서, 더 높은 Test accuracy를 달성하고 / 빨리학습하게 되어 오버피팅의 방지를 위한 Early-Stop(Val)도 더 적다.
- pruning된 네트워크를 랜덤하게 초기화 시켜버리면 효과가 좋지않다.( 기존에 학습했던 초기화값 적용해야한다.)
- p%로 pruning위해 iterative 하는것이 더 좋다. 
<img width="1047" alt="스크린샷 2022-04-06 오전 9 45 10" src="https://user-images.githubusercontent.com/98244339/161873639-e11c7102-b471-42ed-ba98-da8d6cee72c9.png"></br>

<img width="1196" alt="image" src="https://user-images.githubusercontent.com/98244339/161873922-1f74afa3-ca51-4c20-80c5-1f50ffc16a80.png">
