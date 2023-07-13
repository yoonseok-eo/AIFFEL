# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 어윤석
- 리뷰어 : 본인의 이름을 작성하세요.


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [X] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  
- [X] 주석을 보고 작성자의 코드가 이해되었나요?
  > 각 함수와 코드 별로 코드의 의미를 정리하기 위한 주석이 많이 달려있다.  
  > 덕분에 코드를 쉽게 이해하고 오히려 많이 배우게 되었다.
- [X] 코드가 에러를 유발할 가능성이 없나요?
  > 새로운 실험마다 변수명을 다르게 하여 여러 이미지에 대해 실행해도 에러가 일어나지 않도록 작성하였다.
- [X] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 라이브러리에서 제공되는 함수들도 주석을 달아서 함수를 제대로 이해하려고 했다.  
  > 이미지를 회전시키는 새로운 실험에 사용된 함수도 사용법을 잘 익히고 사용하였다.
- [X] 코드가 간결한가요?
  > 함수로 구현하여 새로운 이미지가 들어왔을 때 쉽게 실험할 수 있도록 하였다.

# 예시
1. 코드의 작동 방식을 주석으로 기록합니다.
2. 코드의 작동 방식에 대한 개선 방법을 주석으로 기록합니다.
3. 참고한 링크 및 ChatGPT 프롬프트 명령어가 있다면 주석으로 남겨주세요.
```python
# 예시: 주석 사용
def put_sticker_on_face(img, stiker, num_pyramid=1, show_landmark=False):
    return_img = img.copy()
    # 얼굴 정보 추출
    info_list = get_face_info(return_img, num_pyramid, show_landmark)
    # 얼굴에 스티커 적용
    for info in info_list:
        # 얼굴 정보
        w = info['width']
        h = info['height']
        nose_point = info['nose']
        # 스티커 이미지 복사
        temp_sticker = stiker.copy()
        # 얼굴 크기로 사이즈 조정
        temp_sticker = cv2.resize(temp_sticker, (w,h)) 
        # 스티커 이미지 위치 x, y 좌표 설정 : 코 위치로 부터 이미지 시작 위치 설정
        x = nose_point[0] - (w // 2)
        y = nose_point[1] - (h // 2)
        # 스티커 위치가 원본을 벗어 나는 경우 이미지 및 위치 조정
        if x < 0: 
            temp_sticker = temp_sticker[:, -x:]
            x = 0
        if y < 0:
            # ex> y가 -98이면, temp_sticker[98: , :]가 된다. (187, 187, 3)에서 (89, 187, 3)이 됨 (187개 중에서 98개가 잘려나감)
            temp_sticker = temp_sticker[-y:, :] 
            y = 0
        sticker_area = return_img[y:y+temp_sticker.shape[0], x:x+temp_sticker.shape[1]]
        
        return_img[y:y+temp_sticker.shape[0], x:x+temp_sticker.shape[1]] = \
            np.where(temp_sticker!=0, sticker_area, temp_sticker).astype(np.uint8)
    
    return return_img
```
```python
# 예시: 간결한 코드
img_two = cv2.imread('./images/twoshot.jpg')
img_result = put_sticker_on_face(img_two, img_sticker) # 함수 하나로 이미지에 스티커를 붙일 수 있도록 하였다.
plt.imshow(cv2.cvtColor(img_result, cv2.COLOR_BGR2RGB))
plt.show()
```

# 참고 링크 및 코드 개선
```python
def put_sticker_on_face(img, stiker, num_pyramid=1, show_landmark=False):
    return_img = img.copy()
    info_list = get_face_info(return_img, num_pyramid, show_landmark) # 얼굴 정보 추출

    # 얼굴에 스티커 적용
    for info in info_list:
        w = info['width']
        h = info['height']
        nose_point = info['nose']

        temp_sticker = stiker.copy()
        temp_sticker = cv2.resize(temp_sticker, (w,h))

        # 스티커 이미지 위치 x, y 좌표 설정 : 코 위치로 부터 이미지 시작 위치 설정
        x = nose_point[0] - (w // 2)
        y = nose_point[1] - (h // 2)

        # 스티커 위치가 원본을 벗어 나는 경우 이미지 및 위치 조정
        if x < 0: 
            temp_sticker = temp_sticker[:, -x:]
            x = 0
        if y < 0:
            temp_sticker = temp_sticker[-y:, :] 
            y = 0
        sticker_area = return_img[y:y+temp_sticker.shape[0], x:x+temp_sticker.shape[1]]
        
        return_img[y:y+temp_sticker.shape[0], x:x+temp_sticker.shape[1]] = \
            np.where(temp_sticker!=0, sticker_area, temp_sticker).astype(np.uint8)
    
    return return_img

# 개인적인 생각이지만 주석이 너무 많으면 오히려 가독성이 떨어질 수 있습니다.
# 웬만히 알 수 있는 정보들은 주석에서 제외하는 것도 좋을 것 같습니다.
# 그리고 각 주석이 달리는 코드 사이 또는 코드가 진행되는 스탭 사이에는
# 줄바꿈을 추가하는 것도 가독성에 많이 도움됩니다.😊
```
