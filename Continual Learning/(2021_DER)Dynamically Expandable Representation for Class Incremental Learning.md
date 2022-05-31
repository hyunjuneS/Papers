## Key Idea
#### 이전 학습된 Feater map(Freeze)과, 새로운 task의 Feature map을 합친다.
#### 새로운 task를 위한 Feature map 학습시에, 보조 Classifier loss term & mask-based pruning 추가한다.
![image](https://user-images.githubusercontent.com/98244339/171101238-0f8586c4-7466-4e5c-9448-724f54e9f297.png)

## Loss-term

### Classifier (L_ht)
- t번째 task의 trainig-data & Rehearsal memory 간 cross-entropy </br>
![image](https://user-images.githubusercontent.com/98244339/171101441-b919a98d-1142-4097-a5c1-eaf0ea6730fe.png)

### Auxiliary Classifier (L_hta)
- auxiliary classifier와 새로운 task의 Feature map만을 사용하여 Cross-entropy
- 이전 task 와 현재 task 분류하기 위해, 라벨의 갯수는 : 새로운 task의 라벨 갯수 + 1 ( 이전개념을 하나의 카테고리로 )

### Sparsity Loss (L_s)
- HAT개념을 사용하여, mask를 sigmoid & learnable parameter & scaling 으로 </br>
![image](https://user-images.githubusercontent.com/98244339/171102898-5232d10f-636a-4c88-ab71-798440a6a27c.png)

