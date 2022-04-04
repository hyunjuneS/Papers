## Key Idea : original data 없이, new task data로만 네트워크를 학습시키고, original task performance를 유지할 수 있는 모델 제시

## Introduction
- Shared parameters( 전반적인 학습을 위해 공유되는 파라미터 ) : θs
- Original task-specific parameters ( 기존 task를 위해 있는 마지막 파라미터 ) : θo
- new task-specific paramters (새로운 task를 위해 있는 마지막 파라미터 ) : θn

- Feature Extraction : θs , θo 고정 / θn 새로 만든후 변경 ( new task 에서 성능 안좋음 )
- Fine-tuning : θo 고정 / θs , θn 변경 ( old task에서 성능이 떨어짐 )
- Fine-tuning FC : θs 고정 / θo , θn 변경 ( new task에서 성능 안좋음 )
- joint Training : θs , θo , θn 변경( 가장 좋음, 우리가 제안하는 모델과 비슷)
- ![image](https://user-images.githubusercontent.com/98244339/161488561-f7635946-039d-4540-9724-ec1a74b0a640.png)

## Learning Without Forgetting Step
- Step1. 기존 네트워크에서 새로운 이미지에 대한 출력값 저장( Yo )
- Step2. 기존 네트워크에 새로운 class의 노드를 마지막 레이어 아래에 추가시키고,θn 으로 초기화
- Step3. θs , θo 고정 / θn 학습 ( Warm-up step )
- Step4. θs , θo , θn 학습 ( Joint-optimize step )
- ![image](https://user-images.githubusercontent.com/98244339/161492222-77dd0bae-d31f-4a0a-85f9-f6efa8132f03.png)




## Loss-Function
- Loss for new task 
- ![image](https://user-images.githubusercontent.com/98244339/161491088-9df5838b-945d-489d-9807-e869cb5d2567.png)

- Loss for original task
- ![image](https://user-images.githubusercontent.com/98244339/161491404-ef804a66-9c91-46dd-8b80-e91807b4dc88.png)
- ![image](https://user-images.githubusercontent.com/98244339/161491462-ce14e33d-8993-4ea0-bee5-3d875201adce.png)



