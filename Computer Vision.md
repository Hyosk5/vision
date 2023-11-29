# Computer Vision
### Image Data
![Alt text](/md_images/image-01.png)
- Image Data는 2차원 또는 3차원(Tensor) 형태의 행렬
- Image Data 행렬의 element는 0~255 사이의 정수 값을 갖으며, 이를 pixel이라 부름
- 흑백 Image는 (가로 X 세로) 형태의 2차원 행렬

![Alt text](/md_images/image-02.png)
- RGB Image는 (가로 X 세로 X 3) 형태의 3차원 행렬로 3은 각각 R(Red), G(Green), B(Blue)에 대한 scale을 의미
- RGB Image의 한 점은 R, G, B 각 채널 값의 결합으로 보여지며, 각 채널에서 0~255 사이의 정수 값을 갖음
- Red: (255,0,0) / Green: (0,255,0) / Blue: (0,0,255) / white: (0,0,0) / Black: (255,255,255)

### Computer Vision에서의 Challenge
![Alt text](/md_images/image-03.png)

### 기존 CV(Computer Vision) 알고리즘
- Find edges -> Find corners -> 문제 해결

### 대표적 Tasks
![Alt text](/md_images/image-04.png)

### 응용분야
- 물체 인식(Object detection): CCTV, 자율주행, 의료 등
- OCR(Optimal Character Recognition): NLP와 결합하여 사진 속의 의미있는 것을 추출하여 인식하고 해석
- 얼굴 인식(Face Recognition): iPhone 얼굴 인식 등
- Artistic Images: 가상 이미지를 생성하는 생성 모델 
