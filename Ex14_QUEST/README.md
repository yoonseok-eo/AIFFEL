# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 어윤석
- 리뷰어 : 조대호 

# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [O] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  >네 코드가 정상작동하고 주어진 문제를 해결하였습니다.
- [O] 주석을 보고 작성자의 코드가 이해되었나요?
  > 네 주석을 달아주어 코드를 이해하는데 도움이 되었습니다.
  '''python
#----------------------------------------------------------------------------------------
# 스케치 및 채색된 2개 이미지를 입력으로 받아 랜덤 연산을 두 이미지에 동일하게 적용
#----------------------------------------------------------------------------------------
@tf.function() # 빠른 텐서플로 연산을 위해 @tf.function()을 사용합니다. 
def apply_augmentation(sketch, colored):
    # 역방향 축으로 이미지(텐서) 결합
    stacked = tf.concat([sketch, colored], axis=-1)
    
    # 랜덤으로 REFLECT 또는 CONSTANT 모드를 지정하여 30픽셀 만큼 패딩
    _pad = tf.constant([[30,30],[30,30],[0,0]])
    if tf.random.uniform(()) < .5:
        padded = tf.pad(stacked, _pad, "REFLECT")
    else:
        padded = tf.pad(stacked, _pad, "CONSTANT", constant_values=1.)

    # 256*256*6 크기로 랜덤으로 자르기
    out = image.random_crop(padded, size=[256, 256, 6])
    # 무작위로 좌우 반전
    out = image.random_flip_left_right(out)
    # 무작위로 상하 반전
    out = image.random_flip_up_down(out)
    # 90도 단위로 무작위 회전
    if tf.random.uniform(()) < .5:
        degree = tf.random.uniform([], minval=1, maxval=4, dtype=tf.int32)
        out = image.rot90(out, k=degree)
    
    return out[...,:3], out[...,3:]   
#----------------------------------------------------------------------------------------
  '''
- [O] 코드가 에러를 유발할 가능성이 없나요?
  >네 정상적으로 실행되어 에러가 유발하지 않을 것 같습니다.
- [O] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  >네. discriminator 구현부분 이나 학습부분에서 궁금했던 질문들을 잘 답변해 주셔서 코드를 이해하고 있다고 생각합니다.
- [O] 코드가 간결한가요?
  > 네. generator 구현 부분을함수로 작성하여 간결하게 작성한것 같습니다.

# 예시
1. 코드의 작동 방식을 주석으로 기록합니다.
2. 코드의 작동 방식에 대한 개선 방법을 주석으로 기록합니다.
3. 참고한 링크 및 ChatGPT 프롬프트 명령어가 있다면 주석으로 남겨주세요.
```python

```
# 참고 링크 및 코드 개선
코드 보면서 이야기 했던 augmentation 부분에 대해서 참고할 만한 링크 남겨드립니다.
[augmentation](https://lcyking.tistory.com/77)
