## KeyIdea : GAN을 Continual Learning 하자. ( Continual Learning 의 Rehearsal 을 Generator하는 것이 아닌, Generative model을 Continual Learning 하자 )

## Main Method
![image](https://user-images.githubusercontent.com/98244339/168967929-1450d7d0-581a-45db-815b-126cfa305852.png)

### Joint retraining with replayed samples
- current task의 real data & previous task 의 memory replay(by generator) 를 합친다.
- 그후, Joinnt trainig 
![image](https://user-images.githubusercontent.com/98244339/168967897-86e617c7-59bc-4687-9ef8-17b6493b8618.png)

### Replay alignment
- 현재 task(t)까지 학습한 Generator 와 이전 task(t-1)까지 학습한 Generator 간 L2 loss 
![image](https://user-images.githubusercontent.com/98244339/168968369-d2525e70-c836-4ae7-b63e-0dbabd58f2f6.png)


## Experiment
![image](https://user-images.githubusercontent.com/98244339/168968437-11ec8880-9a3b-4e9e-8a21-276ab773f654.png)

