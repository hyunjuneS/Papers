## Key Idea : Hard Attention mask를 사용하여 task-classifier 하자.
- 이전 task 의 attention vector는 mask를 정의하고, 현재 task의 weight update를 제약한다.
- mask가 거의 binary 이기때문에, 일정비율은 고정되고 남은것은 새로운 task에서 학습된다.

