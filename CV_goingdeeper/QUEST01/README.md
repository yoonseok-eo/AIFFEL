# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 어윤석
- 리뷰어 : 이수봉


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [X] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  
- [X] 주석을 보고 작성자의 코드가 이해되었나요?
  > 네, 주석을 통하여 작성자의 코드를 이해할 수 있었습니다.
  > 시각화 코드를 통해 모델의 결과값을 시각화 한것도 인상깊었습니다.
  > 회고를 통해 모델의 결과를 분석한점도 인상깊었습니다.
- [X] 코드가 에러를 유발할 가능성이 없나요?
  > 아니요. 에를 유발할 가능성이 없었습니다.
- [X] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 네, ResNet 모델의 구조와 특징에 대해 이해하고 작성을 하였습니다.
- [X] 코드가 간결한가요?
  > 불필요한 코드 없이 간결하였습니다.

# 예시
1. 코드의 작동 방식을 주석으로 기록합니다.
2. 코드의 작동 방식에 대한 개선 방법을 주석으로 기록합니다.
3. 참고한 링크 및 ChatGPT 프롬프트 명령어가 있다면 주석으로 남겨주세요.
```python
import tensorflow as tf
from tensorflow.keras import layers, Model
import numpy as np 

def resnet_block(input_layer, filters, strides=1, is_50=False, is_plain=False):
    first_kernel_size = 3
    first_padding = 'same'
    last_filters = filters    
    if is_50:
        first_kernel_size = 1
        first_padding = 'valid'
        last_filters = filters * 4
    
    x = layers.Conv2D(filters, kernel_size=first_kernel_size, strides=strides, padding=first_padding)(input_layer)
    x = layers.BatchNormalization()(x)
    x = layers.Activation('relu')(x)
    
    x = layers.Conv2D(filters, kernel_size=3, strides=1, padding='same')(x)
    x = layers.BatchNormalization()(x)
    
    if is_50:
        x = layers.Activation('relu')(x)
        x = layers.Conv2D(last_filters, kernel_size=1, strides=1, padding='valid')(x)
        x = layers.BatchNormalization()(x)
    
    if is_plain==False:
        # 잔차 연결
        shortcut = input_layer
        if strides > 1 or is_50:
            shortcut = layers.Conv2D(last_filters, kernel_size=1, strides=strides, padding=first_padding)(shortcut)
            if strides > 1:
                shortcut = layers.BatchNormalization()(shortcut)    
        x = layers.Add()([x, shortcut])
        
    x = layers.Activation('relu')(x)
    return x

def build_resnet(input_shape, num_classes, is_50=False, is_plain=False):
    # input layer
    input_layer = layers.Input(shape=input_shape)
    
    x = input_layer
        
    # Conv1
    x = layers.Conv2D(64, 7, strides=2, padding='same')(x)
    x = layers.BatchNormalization()(x)
    x = layers.Activation('relu')(x)
        
    # Conv2
    x = layers.MaxPool2D(pool_size=(3, 3), strides=2, padding='same')(x)
    for i in range(3):
        x = resnet_block(x, 64, 1, is_50, is_plain)
    
    # Conv3
    for i in range(4):
        s = 1
        if i==0:
            s = 2
        x = resnet_block(x, 128, s, is_50, is_plain)
    
    # Conv4
    for i in range(6):
        s = 1
        if i==0:
            s = 2
        x = resnet_block(x, 256, s, is_50, is_plain)
        
    # Conv5
    for i in range(3):
        s = 1
        if i==0:
            s = 2
        x = resnet_block(x, 512, s, is_50, is_plain)
    
    x = layers.GlobalAveragePooling2D()(x)
    outputs = layers.Dense(num_classes, activation="softmax")(x)
    
    return Model(
        inputs=input_layer, 
        outputs=outputs
    )
```

# 참고 링크 및 코드 개선
```python
# 프로젝트 노드에서 제시된 cats_vs_dogs 데이터로 학습을 진행했을때의 결과도 궁금합니다.

```