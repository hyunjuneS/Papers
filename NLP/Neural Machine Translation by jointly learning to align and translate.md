## 논문명 : Neural Machine Translation by jointly Learning to Align and Translate

## Key Idea : Align ( 문장에서 어디에 집중해야되어 번역을 해야되는지 ) 하고, Translate ( 단어 예측 )

- Input Sentence를 고정된 context vector 로 Encoding 하는것이 아닌, 각 단어별 context vector를 만들고, decoding 할때 필요한 context vector를 선정한다.


# RNN Encoder - Decoder
## Encoder 
- 입력 문장(벡터 x)을 hidden state(h)로 만든후, nonlinear function(q) 사용하여 context vector(c)로 만든다. 
- <img width="343" alt="스크린샷 2022-03-24 오전 9 42 50" src="https://user-images.githubusercontent.com/98244339/159819565-5f6bcc42-4742-4d13-bc91-ba11d9af314c.png">

## Decoder
- 고정된 길이의 context vector(c)와 이전 예측단어 (y)가 주어지면 조건부확률로 구할 수 있음.
- 각 조건부 확률은 이전 단어(y) , hidden state(s) , context vector(c), nonlinear function(g) 로 구할 수 있음.
- <img width="441" alt="스크린샷 2022-03-24 오전 9 46 40" src="https://user-images.githubusercontent.com/98244339/159819902-0bc2c12c-259f-47bf-9938-d9277aa2520d.png">
- <img width="474" alt="스크린샷 2022-03-24 오전 9 46 45" src="https://user-images.githubusercontent.com/98244339/159819910-a78b08ad-397a-4af2-bcb1-01613b500545.png">


# Learning to align and translate 의 Encoder - Decoder

## Encoder
- 저자는 각 단어별 context vector 를 annotation이라 부른다.
- Bidirectinal RNN 을 사용하여 annotation Sequence를 만든다.
- BiRNN 은 최근단어가 focus 되도록 정방향,역방향 으로 hidden state를 계산한다.
- 따라서, 각 단어별 annotation 은 정방향 h, 역방향 h의 결합으로 표현된다.
- 즉, 각 단어별 annotation 은 뒷단어와 앞단어 모두의 정보를 가지고 있다. ( 즉 각단어의 context vector 는 앞뒤의 정보를 가지고있다.)
- <img width="309" alt="스크린샷 2022-03-24 오전 10 02 24" src="https://user-images.githubusercontent.com/98244339/159821412-e32d7166-2397-425d-abfe-749584cae98b.png">



## Decoder
- 
