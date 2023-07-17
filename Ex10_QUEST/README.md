# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 어윤석
- 리뷰어 : 이수봉


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [X] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  
- [X] 주석을 보고 작성자의 코드가 이해되었나요?
  > 코드블럭에 주석이 있어서 이해가 되었습니다.
- [X] 코드가 에러를 유발할 가능성이 없나요?
  > 아니요 에러를 유발할 가능성이 없었습니다.
- [X] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 네, 코드 작성자가 코드 설명을 해주었습니다.

  > 모델의 문제점에 대해서도 설명해주었습니다.

  > 노드의 코드를 작성자가 재구성 해서 코드를 작성했습니다.


- [X] 코드가 간결한가요?
  > 불필요한 코드없이 코드가 간결했습니다.

# 예시
1. 코드의 작동 방식을 주석으로 기록합니다.
2. 코드의 작동 방식에 대한 개선 방법을 주석으로 기록합니다.
3. 참고한 링크 및 ChatGPT 프롬프트 명령어가 있다면 주석으로 남겨주세요.
```python
'''
Parameter
- img_orig : cv2 이미지 객체
- output : 이미지 분할 output
- label: 마스킹 label명
- is_label_blurring : label 블러 여부(default: False)
    False - label 블러 제외, True - label 블러 처리
- ksize: 블러링 커널 사이즈

Return
- 블러 처리 적용 cv2 이미지 객체
'''    
def get_blurring_img(img_orig, output, label, is_label_blurring=False, ksize = (13, 13)):
    
    img_orig_blur = cv2.blur(img_orig, ksize)
    
    # label segment
    seg_color = get_rgb_of_label(label)
    seg_map = np.all(output == seg_color, axis=-1)    
    
    # True과 False인 값을 각각 255과 0으로 바꿔줍니다
    img_mask = seg_map.astype(np.uint8) * 255
    
    # mask 이미지를 BGR 채널로 변경
    img_mask_color = cv2.cvtColor(img_mask, cv2.COLOR_GRAY2BGR)
    
    a, b  = img_orig, img_orig_blur
    if is_label_blurring:
        a, b  = img_orig_blur, img_orig
        
        
    img_concat = np.where(img_mask_color==255, a, b)
    return cv2.cvtColor(img_concat, cv2.COLOR_BGR2RGB)

plt.imshow(get_blurring_img(img_orig, output, 'person'))
plt.show()
```

# 참고 링크 및 코드 개선
```python
# 코드 리뷰 시 참고한 링크가 있다면 링크와 간략한 설명을 첨부합니다.
# 코드 리뷰를 통해 개선한 코드가 있다면 코드와 간략한 설명을 첨부합니다.

# pixellib 라이브러리를 활용한 instance segmentation 하는 방법
# https://pixellib.readthedocs.io/en/latest/Image_instance.html
```
