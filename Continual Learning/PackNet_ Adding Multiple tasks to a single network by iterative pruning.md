## key Idea : pruning을 이용해 pruning 된 parameter는 새로운 task에 학습하고, pruning되지 않은 파라미터는 고정시키자.

- task1학습에서 고정된(pruning되지 않음) 회색 parameter도 task2학습에 이용된다.
![image](https://user-images.githubusercontent.com/98244339/164135836-acedbef8-14a4-4f90-a063-e8be1930fb7d.png)
