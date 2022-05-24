## Key Idea : new trainig data 만 사용하여 new_model 만들고, Unlabeled data 를 활용해 이전 모델과 합치자.
![image](https://user-images.githubusercontent.com/98244339/169985704-e15517f3-470b-4567-af29-81869353cd38.png)

### 가정
![image](https://user-images.githubusercontent.com/98244339/169987622-42e93e4a-2a03-4317-9499-391e2b550563.png)

## Method
- new & old Combination model ( 단순 조합 )</br>
![image](https://user-images.githubusercontent.com/98244339/169988396-0753e840-0c66-47a3-877c-37e3414a766c.png)</br>
- 상단의 Combination model 기준으로 Consolidated model 만들자 ( logits(softmax 이전 inputs)  minimize )
- ![image](https://user-images.githubusercontent.com/98244339/169989988-ffdbf21e-ca14-41a1-9578-d552da936f93.png)
- ![image](https://user-images.githubusercontent.com/98244339/169990041-3561a5b9-8d8f-4908-8015-d165e7fe17df.png)




