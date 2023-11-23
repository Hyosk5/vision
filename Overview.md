## OverView
### Image Data
- Image Data는 2차원 또는 3차원(Tensor) 형태의 행렬
- 흑백 Image는 (가로 X 세로) 형태의 2차원 행렬
- RGB Image는 (가로 X 세로 X 3) 형태의 3차원 행렬로 3은 각각 R(Red), G(Green), B(Blue)에 대한 scale을 의미
- Image Data 행렬의 element는 0~255 사이의 정수 값을 갖으며, 이를 pixel이라 부름
- RGB Image의 한 점은 R, G, B 각 채널 값의 결합으로 보여지며, 각 채널에서 0~255 사이의 정수 값을 갖음
- Red: (255,0,0) / Green: (0,255,0) / Blue: (0,0,255) / white: (0,0,0) / Black: (255,255,255)

### Computer Vision에서의 Challenge
- Illumination(조명)
- Deformation(변형된 형태)
- Occlusion(폐색)
- Background Clutter(배경에 대한 혼란)
- Intraclass variation(클래스 내의 변형)

### 기존 CV(Computer Vision) 알고리즘
- Find edges -> Find corners -> 문제 해결

### 대표적 Tasks
- Classification(분류)
- Object Detection(객체 인식)
- Instance Segmentation(객체 분할)
