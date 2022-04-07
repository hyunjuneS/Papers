## Key Idea : classifier 와 representation(feature extraction , θs) 을 동시에 learning 할 수 있다.


## Class-Incremental 의 3가지 특징
1. 다른시간에 발생한 다른 class의 데이터를 학습할 수 있어야 한다.
2. 지금까지 본 class까지 multi classification할 수 있어야 한다.
3. 지금까지 본 class의 수와 관련하여, computation 과 memory는 매우 천천히 증가하거나 그 주변이여야 한다.

## iCaRL 구성요소
1. Nearest-mean-of-examplars ( Classification )
2. Prioritized examplar selection
3. Knowledge distillation and prototype rehearsal ( Representation learning )




