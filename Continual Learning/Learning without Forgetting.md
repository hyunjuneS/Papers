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

## Result
- new task 에서 다른 모델에 비해 전반적으로 우수하다.
- old task 에서도 fine-tuning보다 우수하고, 종종 다른 모델에 비해서는 떨어진다.
- 종합적으로 살펴보면 람다가 조정되면 아래 그래프와 같이 LWF의 성능이 우수하다.
- Joint Training 에 비해서는 old task에서는 약간 떨어지고, new task에서는 우수하다.
- 하지만 joinn-training의 경우, original data가 필요하지만, 우리는 필요 없다.
- 유사하지 않은 newtask 에서는 일반적으로 성능이 좋지 않았다.
![image](https://user-images.githubusercontent.com/98244339/161502680-898da315-4c0a-4ee8-972f-4f3bf53fb02e.png)
![image](https://user-images.githubusercontent.com/98244339/161502607-e918cb1a-fd53-4156-ba3b-0e91720b2c68.png)
![image](https://user-images.githubusercontent.com/98244339/161502614-d38ce518-0d10-4961-835f-27a6d0ee19c3.png)




