## Key Idea
### Convolution Architecture 활용한 GAN 모델 처음 제시하며, GAN이 이미지 잘 생성할 수 있게 해준 모델
![image](https://user-images.githubusercontent.com/98244339/171778193-eb28b13c-83ab-43a3-b8a3-133584ed7d6c.png)

### Generator가 이미지를 외워서 준것이 아니란 것과, latent space(z-space)의 변화에 따라 부드러운 변화를 보여주어야 한다.
##### 이미지를 외워서 보여준것이 아니라는 결과물 : 1Epoch 만으로 그럴듯한 이미지 생성 </br>
![image](https://user-images.githubusercontent.com/98244339/171778464-50844150-7921-42e2-bc79-e4b961a122d7.png)

##### latent-space(z-space)의 변화에 따라 부드러운 변화 생성 (창문이 점점 생기는 과정 ) </br>
![image](https://user-images.githubusercontent.com/98244339/171778557-0bc7c3ba-23f2-4174-b1db-fd7516193b8e.png)

##### latent-space Z-벡터의 산술 표현으로 의미론적 이미지 생성가능 </br>
[image](https://user-images.githubusercontent.com/98244339/171778764-0b7e11f8-4545-4b92-a647-c3fce8dd3d82.png)


