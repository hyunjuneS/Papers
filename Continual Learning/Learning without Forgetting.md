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

## Experiment Total Result
- new task 에서 다른 모델에 비해 전반적으로 우수하다.
- old task 에서도 fine-tuning보다 우수하고, 종종 다른 모델에 비해서는 떨어진다.
- 종합적으로 살펴보면 람다가 조정되면 아래 그래프와 같이 LWF의 성능이 우수하다.
- Joint Training 에 비해서는 old task에서는 약간 떨어지고, new task에서는 우수하다.
- 하지만 joinn-training의 경우, original data가 필요하지만, 우리는 필요 없다.
- 유사하지 않은 newtask 에서는 일반적으로 성능이 좋지 않았다.
![image](https://user-images.githubusercontent.com/98244339/161502680-898da315-4c0a-4ee8-972f-4f3bf53fb02e.png)
![image](https://user-images.githubusercontent.com/98244339/161502607-e918cb1a-fd53-4156-ba3b-0e91720b2c68.png)
![image](https://user-images.githubusercontent.com/98244339/161502614-d38ce518-0d10-4961-835f-27a6d0ee19c3.png)


## Experiment Other Result
1. Multiple new task scenario
- new task를 큰 class 별 part로 나누어서 순차적으로 학습한 결과
- LWF 가 joint-training 을 제외하고는 거의 앞선결과를 냈다.
![image](https://user-images.githubusercontent.com/98244339/161507559-8ee3d409-aff9-4d4f-94f6-20fd9b80d01f.png)


2. Influence of dataset size
- new task의 dataset size에 따른 performance를 평가
- LWF가 Fine tuning에서 앞선 성능을 보여주었다.
![image](https://user-images.githubusercontent.com/98244339/161507602-eb7143ba-2882-4e47-afa6-6367deb7ac8a.png)


3. Choice of task-specific layers & Network expansion & Effect of lower lr & L2 soft-constrained weights
- Choice of task-specific layers : taks-specific layers를 증가시키거나
- Network expansion : 네트워크 마지막의 dimension 증가
- Effect of lower lr : θs 의 learning rate 감소
- L2 soft-constrained weights : weight 간 L2 loss term 추가
와 같이 여러 실험을 해도, 성능에 큰 부족함이 없다. 

- ![image](https://user-images.githubusercontent.com/98244339/161509970-40b3c157-3bb4-44dc-8c26-a41000a7333c.png)
- ![image](https://user-images.githubusercontent.com/98244339/161510130-25c0b97c-5a23-4407-82af-3c192dc9b225.png)






