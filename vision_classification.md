# Vision Classification
- Image의 label이 무엇인지를 예측하는 알고리즘
- 일반적으로 확률 벡터로 output을 구성
- 확률 벡터는 백터 내 모든 확률 값이 0이상 1이하여야 하며, 그 합은 1이어야 함
- 이를 위해 Softmax Function을 일반적으로 활용함

### Convolutional Layer
- Image Data를 이해하기 위해서는 이미지의 특징을 잘 파악해야 함
- Fully Connected Layer로는 이미지 특징을 활용하기 어렵고, parameter 수가 너무 많아짐
- Convolutioanl Layer는 선형함수이고 데이터의 공간적 특징(Spatial feature)를 잘 추출함
- 이미지의 특징을 잘 추출하고 down size(적은 parmeter 수) 할 수 있도록 Convolutioanl Layer를 활용
- Convolutional Layer를 통해 Filter된 matrix를 Activation map이라 함
- 하나의 Convolutional Layer가 하나의 층으로 생각할 수 있음

### Padding
- 원본 Image Data에 행과 열을 추가하는 방법
- 커널을 통과하면서 Image Data의 크키가 작아지는 것을 방지하는 것으로 생각할 수 있음
- 일반적으로 0으로 행과 열을 추가하기 때문에 원본 Image Data에 대한 왜곡은 생기지 않음

### Stride 
- kernel이 움직이는 칸의 수로 이해할 수 있음
- Stride가 n이라면 kernel이 n칸씩 이동하며 특징을 추출하는 것

### Pooling
- Image Data에서 학습하는 parameter 없이 크기를 줄이는 방법
- Max pooling: kernel에 포함되는 값 중 최대값을 대표값으로 추출하여 Image Data의 크기를 줄이는 방식
- Average pooling: kernel에 포함되는 값의 평균을 대표값으로 추출하여 Image Data의 크기를 줄이는 방식

### Convolutional Block
- Convolutional Layer와 Activation Function으로 구성된 block
- Convolutional Layer를 통과한 각 Pixel을 Activation Function통해 Non-linear 하게 변환
- 대표적 Activation Function: Relu

### Simple Convolutional Network
- Inputs => n개의 Conv Block => Flatten => Fully Connected Layer => Softmax => Output(확률 벡터)

### Loss
- Image Data에 대한 Label은 one-hot vector로 표현
- Cross-Entropy Function: 두 확률 벡터 사이의 거리를 측정하는 지표
- Kullback-Leibler Divergence(KL divergence): Cross-Entropy에서 Entropy를 뺀 값
- Cross-Entropy 또는 KL divergence를 통해 Softmax로 계산된 확률 벡터와 Label의 one-hot vector가 같아지도록 학습

### 