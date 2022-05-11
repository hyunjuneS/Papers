## Key Idea : Hard Attention mask를 사용하여 task-classifier 하자.
- task identifier 하기위해, 레이어별로 condition 을 매기는 attention-mechanism 이용하자.
- task 를 학습하는 동시에, attention-mechanism 도 같이 학습한다.
- 이전 task 의 attention vector는 mask를 정의하고, 현재 task의 weight update를 제약한다.
- mask가 거의 binary 이기때문에, 일정비율은 고정되고 남은것은 새로운 task에서 학습된다.

## main structure

[forward (상단)] </br>
- 이전 layer 와 attention vector 간 element-wise multiply
- ![image](https://user-images.githubusercontent.com/98244339/167348658-d675da57-60ba-43e0-9684-6151ed95bfa6.png)
- attention vector는 embedding 된 task 와 s(positive scaling) 를 곱한후 gate(sigmoid)통과
- ![image](https://user-images.githubusercontent.com/98244339/167348623-784aedf5-4742-47e8-836e-78c7b03afc72.png)


[ backward (하단)] </br>
- 이전 task를 위해 누적된 attention 사용.
- ![image](https://user-images.githubusercontent.com/98244339/167348519-31e8cd05-c1cb-4eb6-bce8-c6f62815367f.png)
- 누적된 attention 을 expand / wlement-wise minimum / subtraction / multiplication
- ![image](https://user-images.githubusercontent.com/98244339/167348933-d456472a-1719-4028-ac26-15c24646bd07.png)

[ backward 의 positive scaling ]</br>
- binary한 attention 을 얻기위해 unit-step-function 을 사용해야 하지만, embedding 된 e가 back-propagation 을 사용하므로, s(positive scaling) 를 곱한 sigmoid를 사용한다. 
- s(positive scaling)는 trainnig과정에서 s를 점차 키우고, test에서는 s를 max로 둔다.
- s를 점차 키우는 식은 아래와 같다.
- ![image](https://user-images.githubusercontent.com/98244339/167350342-f99b6ccf-2424-4601-8722-da40bc29e511.png)

[ backward 의 Embedding gradient Compensation]</br>
- positive scaling 으로 annealed sigmoid(상승시키며 sigmoid) 의 효과를 없애주고, 이전 분포의 magnitude를 변화시키기 위해 embedding gradient compensation 을 사용한다. 
- ![image](https://user-images.githubusercontent.com/98244339/167351449-493fcca0-0532-4627-8e04-c7dfdd000355.png)


[ main structure ]</br>
- ![image](https://user-images.githubusercontent.com/98244339/167347943-2d2fdbff-6187-4a37-9fef-b7caa0c7bc12.png)

- 특정 task 에서 사용될 수 있도록 attention mask 에 sparsity를 부여하기 위해 regularization term 을 추가한다.
- ![image](https://user-images.githubusercontent.com/98244339/167528897-5fe7f9d7-93ad-450f-a4f0-427a314c4745.png)
