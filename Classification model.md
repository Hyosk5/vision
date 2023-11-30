# Classification Models
### Vision Classification
- Image의 label이 무엇인지를 예측하는 알고리즘
- 일반적으로 확률 벡터로 output을 구성
- 확률 벡터는 백터 내 모든 확률 값이 0이상 1이하여야 하며, 그 합은 1이어야 함
- 이를 위해 Softmax Function을 일반적으로 활용함

### VGGNet
![Alt text](/md_images/image-08.png)
- 2014년 Oxford 대학교의 VGGNet 팀에서 깊이(Layer의 수)와 성능의 관계를 파악하고자 만든 모델
- 간단한 구조이면서 성능이 훌륭하여 변형하여 많이 사용 중
- VGG16, VGG19 등의 모델이 있으며 뒷부분의 숫자가 층의 갯수를 의미함

#### 구조
![Alt text](/md_images/image-09.png)
![Alt text](/md_images/image-10.png)
- 깊이의 영향력을 밝히기 위해 3x3 크기의 Filter만을 사용하여 층의 갯수를 늘려가며 모델 구성
- 3x3 크기의 Filter를 3번 통과한 결과와 7x7 크기의 Filter를 한번 통과한 결과의 크기는 같지만 parmameter의 수가 상대적으로 적고 비선형성은 증가시켜 특징 추출에 효율적

### GoogleNet(InceptionNet)
- 학습할 parameter 수를 줄이는 방법에 대한 고민에서 출발
- 2014년 Google에서 bottleneck 구조의 Inception module를 구성하여 만든 모델

#### 구조
![Alt text](/md_images/image-11.png)
![Alt text](/md_images/image-12.png)
- Naive Inception module / 그림 (a)
    - 다양한 크기의 Filter를 통해 특징을 추출하여 마지막에 통합하는 과정
    - 각 Filter를 통과한 output은 height, width가 동일함
    - Channel의 수가 너무 많아지고 연산량이 많아짐
- Inception module / 그림 (b)
    - 그림 (a)에서의 연산량을 줄이고자 각 Filter를 통과하기 전에 1x1 크기의 Filter를 추가
    - Channel의 단위로 fully-conntected 연산을 하여 Channel 수를 줄이는 효과 - NIN. (Network in Network)
    - Output의 크기를 맞추기 위해 Max Pooling layer 뒤에 1x1 Conv 추가
- 전체 구조
    - 층이 깊어지면서 loss에 대한 back-propagation의 영향이 줄어드는 gradient vanishing 문제를 해결하기 위해 Auxiliary classification 추가
    - Auxiliary classification는 학습 시에만 사용되며 Inference에서는 삭제
    - 버전이 올라가면서 없어지는 구조


### ResNet
![Alt text](/md_images/image-13.png)
-  깊이가 깊을 수록 모델의 성능은 좋아지지만, 파라미터가 많아지고 overfitting, vanishing gradient 문제 발생
- 해당 문제 해결의 휘해 Skip(Shortcut) Connection 구조를 추가한 모델

#### 구조
- Residual block
![Alt text](/md_images/image-14.png)
    - Input 값을 그대로 전달하여 더해주는 Skip(Shortcut) Connection 구성
    - F(x)가 0이 되도록 학습하므로 나머지(residual)을 학습한다고 볼 수 있음

- 전체 구조
![Alt text](/md_images/image-15.png)
![Alt text](/md_images/image-16.png)
    - VGGNet 구조를 참고하여 2개의 Convolution layer 마다 Skip Connection 연결
    - Plain 모델과 ResNet은 34개 층의 모델의 에러가 더 낮은 것을 알 수 있음


### MobileNet
- Google이 모바일 기기에서 동작하는 것을 목표로 Depthwise separable convolution을 활용하여 경량화한 모델
- V2, V3로 발전해 가며 대표적 경량화 모델로 자리잡음

#### 구조
- Depthwise Separable Convolution
![Alt text](/md_images/image-17.png)
    - Depthwise Convolution 이후에 Pointwise Convolution을 적용한 것
    - 기존의 Convolution 연산은 decompose하여 연산하는 방식으로 parameter 수를 획기적으로 감소시킴
    - Depthwise Convolution
        - Input의 각 채널에 대하여 3x3 크기의 Filter로 하나의 Feature map을 생성하는 연산
        - 채널마다 독립적으로 연산을 수행하여 spatial correlation을 계산하는 역할
    - Pointwise Conovolution
        - 1x1 크기의 Filter로 채널 수를 조정하는 연산
        - 모든 채널에 대한 연산으로 corss-channel correlation을 계산하는 역할

#### 하이퍼파라미터
- MobileNet은 latnecy와 accuracy를 조절하는 하이퍼파라미터 Width Multiplier(α)와 Resolution Multiplier(ρ)가 존재함
- Width Multiplier(α): 모델의 채널 수를 줄이는 하이퍼파라미터로 0 ~ 1 사이의 값이며, 값이 작을수록 연산량과 파라미터 수가 감소
- Resolution Multiplier(ρ): 모델의 입력 해상도를 낮추는 하이퍼파라미터로 0 ~ 1 사이의 값이며, 값이 작을수록 연산량이 감소
![Alt text](/md_images/image-18.png)

#### 성능 비교
- VGG 16에 비해 연산량과 파라미터 수가 20배 이상 적지만 0.9% 정도의 성능 차이가 있으며, GoogleNet보다는 높은 성능을 보여줌
![Alt text](/md_images/image-19.png)
- 상대적으로 작은 크기의 모델인 SqueezeNet과 AlexNet에 비해 연산량과 파라미터 수가 적으면선 더 높은 성능을 보여줌 (하이퍼파라미터를 조정하여 MobileNet을 작게 만듦)
![Alt text](/md_images/image-20.png)

#### MobileNetV2
- relu 함수에서 exploding을 방지하기 위해 6 이상의 값을 6으로 일정하게 고정하는 relu6 사용
![Alt text](/md_images/image-21.png)
- residual block을 채널을 늘렸다 줄이는 형태의 Inverted residual block(MBConv)로 변환
![Alt text](/md_images/image-22.png)
- 기존 MobileNet에 비해 빠른 속도에 높은 성능을 보여줌
![Alt text](/md_images/image-23.png)

#### MobileNetV3
- NetAdapt 알고리즘이 적용된 NAS를 사용하여 구조를 탐색하고 수정하여 성능을 개선한 모델
- 비선형 함수 hard-swish를 고안하여 적용
- MobileNetV3-Large와 MobileNetV3-Small이 존재하며 자원에 따라 알맞게 사용
- Large는 20% 감소한 latency에서 정확도 3.2% 상승
- Small은 동일 latency에서 정확도 6.6% 상승
![Alt text](/md_images/image-24.png)

### EfficientNet
- 모델 경량화를 Width(각 layer의 채널 수), Depth(층의 개수), Resolution(입력 이미지 크기)의 관계를 분석하고 이를 수식으로 표현한 Compound Scaling 방법 제안
![Alt text](/md_images/image-25.png)

#### 구조
- Compound Scaling   
    -  α, β, γ는 small grid search로 결정되는 상수이고 ϕ는 주어진 연산량에 따라 사용자가 결정하는 상수
    - Width
        - 모델 Filter(또는 channel) 갯수를 의미하며 세밀한 Feature 추출을 위해 많이 사용
        - 연산량이 많아짐
    - Depth
        - 모델의 Layer 갯수를 의미하며 보다 복잡하고 많음 Feature 추출을 위해 많이 사용
        - 연산량이 많아지고 Vanishing gradient나 exploding 문제 발생 원인
    - Resolution
        - Image Data의 해상도를 의미하며 높은 해상도가 Feature 추출에 더 유리함
        - 연산량이 많아지고 성능 증가폭은 감소
    
    ![Alt text](/md_images/image-26.png)

#### 성능 비교
![Alt text](/md_images/image-27.png)

#### EfficientNetV2
- MBConv의 depthwise 3x3 크기의 Filter와 1x1 크기의 Filter를 3x3 크기의 Filter 하나로 합친 Fused MBConv 적용한 것이 특징
![Alt text](/md_images/image-28.png)
- EfficientNet에 비해 학습 속도, 파라미터 수, 정확도 측면에서 더욱 효율적이며, 크기에 따라 S, M, L, XL이 존재하여 환경에 따라 선택 가능
![Alt text](/md_images/image-29.png)


### Model training
- Image Classification 모델은 Image의 feature을 추출하기 위해 Convolution layer로 이루어진 Feature extractor(Backbone)와 추출된 feature에 따라 Image의 Label을 학습하는 classifier로 구분
- Image Classification 모델은 무겁고 학습에 있어 많은 시간과 자원이 필요하기 때문에 항상 새로운 모델을 구성하여 학습하기에는 어려움이 있음
- Classification을 통해 학습된 Network를 Object Detection 또는 Semantic Segmentation에 활용

#### Transfer Learning
- 새로운 task에서 학습을 증진시키기 위해 다른 task에서 학습된 model을 가져오는 학습 형태
- 목적
    - 모델 성능 개발
    - Pre-trained model 사용
- 학습방법
![Alt text](/md_images/image-30.png)
    1. 전체 모델 학습
    2. 일부 convolutional layer의 weight는 업데이트 하지 않고 학습
    3. 전체 convolutional layer의 weight는 업데이트 하지 않고 fully connected layer(classifier 부분)만 학습
- 데이터에 따른 학습 방법 선택
![Alt text](/md_images/image-31.png)