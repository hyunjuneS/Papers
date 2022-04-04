## Key Idea : original data 없이, new task data로만 네트워크를 학습시키고, original task performance를 유지할 수 있는 모델 제시

## Introduction
- Shared parameters( 전반적인 학습을 위해 공유되는 파라미터 ) : θs
- Original task-specific parameters ( 기존 task를 위해 있는 마지막 파라미터 ) : θo
- new task-specific paramters (새로운 task를 위해 있는 마지막 파라미터 ) : θn

- Feature Extraction : θs , θo 고정 / θn 새로 만든후 변경 ( new task 에서 성능 안좋음 )
- Fine-tuning : θo 고정 / θs , θn 변경 ( old task에서 성능이 떨어짐 )
- Fine-tuning FC : θs 고정 / θo , θn 변경 ( new task에서 성능 안좋음 )
- joint Training : θs , θo , θn 변경( 가장 좋음, 우리가 제안하는 모델과 비슷)



