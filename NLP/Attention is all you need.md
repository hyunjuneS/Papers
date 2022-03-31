## 논문명 : Attention is all you need

## Key idea : RNN 구조를 사용하지 않고, Neural Machine translation ~~ 에서 제시한 Attention 개념만 사용한 transformer제안한다.
<img width="714" alt="스크린샷 2022-03-31 오전 8 43 17" src="https://user-images.githubusercontent.com/98244339/160949936-8ae42288-d9ea-41d4-90f1-437b8826ce0f.png">

- Self attention : query , key 가 같은 문장안에서 나오는상황 , 즉 해당문장에 어떠한 단어가 다른 단어와 어떤 연관이 있나 . 즉 자기문장안에 단어별로 어떠한 연관성이 잇는지를 파악하는것 

- Multi Head Attention 과 Scaled Dot-Product Attention
<img width="786" alt="스크린샷 2022-03-31 오전 9 10 02" src="https://user-images.githubusercontent.com/98244339/160951100-7ba986a5-765d-4fca-87c0-91f1bd0834f3.png">
- Scaled Dot-Product Attention 은 Query 와 key를 이용하여, energy를 구하고, scale후, softmax 거치고, Value와 곱하여 Attention 을 구한다.
<img width="419" alt="스크린샷 2022-03-31 오전 9 12 58" src="https://user-images.githubusercontent.com/98244339/160951076-8cd39ac2-61a5-42bd-891d-8ea076c99057.png">
- 주로 사용하는 attention mechanism 에는 dot-product attention과 additive attention이 있는데, 이론적으로는 동일하고, scale되는 것만 다르다. 
- scale로 root(dk)를 나누는 이유는 softmax함수의 경우 값이 커지거나 작아지면 gradient 가 너무작아져서 scale 해줌

- Multi Head Attention 의 경우, scaled dot prodcut attention 을 h번만큼 사용한 것. 
