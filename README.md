# 동서한의원 경혈점 AR 자동 태깅을 위한 이미지 딥러닝

#### 파일 설명
- 2022/04/15 업로드: 
  - training_unet.ipynb
    - 정면, 측면에서 귀를 Segment하기 위해 Unet에 학습시키고 평가해 본 코드.
    - 사용 데이터: AI Hub 얼굴 데이터 약 20명 가량, 각도 5가지 (정면, 양쪽 45도각도, 양쪽 90도각도 측면 이용)
    - 참고 코드: https://github.com/hanyoseob/youtube-cnn-002-pytorch-unet, https://www.youtube.com/watch?v=sSxdQq9CCx0&t=204s&ab_channel=hanyoseob
    - UNet으로 AI Hub의 사람 데이터에서는 귀를 잘 잡아내었고, LOSS 값이 0.006 나왔으나, 인터넷에서 구한 연예인 얼굴에서는 귀를 거의 탐지하지 못함.
  - backgroundRemove.ipynb
    - AI Hub 데이터만 학습시킬 경우 과대적합이 발생한다는 사실을 UNet 구현 코드로 인지하였기 때문에, 인물을 제외한 배경을 제거하고 랜덤으로 배경 이미지를 삽입하여 학습 데이터를 풍부하게 구축하기 위해 사용해 본 코드.
    - 사용 데이터: AI Hub 얼굴 데이터, 구글 검색을 활용한 랜덤 풍경 이미지
    - 참고 코드: https://data-flair.training/blogs/python-remove-image-background/
    - MediaPipe 제공 코드로 거의 완벽하게 사람 부분만 Segment해 주는 것을 확인하였음. 이를 활용하여 학습 데이터에 배경을 랜덤하게 삽입할 예정.
  - downloadBackgroundImg.ipynb
    - Selenium을 이용해 랜덤 배경을 N개 확보한 후, 해당 배경 중 랜덤으로 AI Hub 인물 이미지에 합성시켜서 학습용 데이터셋을 만들어 주는 코드.
    - 사용 데이터: pixel 사이트에서 풍경 사진 검색, AI Hub 얼굴 데이터
    - 참고 코드: https://youtu.be/ZylRBW6tL-I
    - class Name은 작동이 안 돼서 XPath로 이미지 src에 접근했으며, BGR RGB가 자꾸 반대로 출력돼서 좀 코드가 이상함.. 몇번이고 바꾸고있음..
