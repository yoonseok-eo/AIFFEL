# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 어윤석
- 리뷰어 : 조준규

# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [X] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  > 전체적으로 코드가 정상적으로 잘 작동하였다.
- [X] 주석을 보고 작성자의 코드가 이해되었나요?
  > 각 코드블럭 위에 주제를 작성하여 어떤 역할을 하는지 쉽게 이해할 수 있었다.
- [X] 코드가 에러를 유발할 가능성이 없나요?
  > 에러가 일어날 부분은 크게 없었다.
- [X] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 함수를 제대로 이해하고 역연산 하는 함수를 작성하여 작업에 용이하도록 하였다.
- [X] 코드가 간결한가요?
  > 함수를 적극적으로 사용하여 코드의 길이를 최소화 하였다.

# 예시
1. 코드의 작동 방식을 주석으로 기록합니다.
2. 코드의 작동 방식에 대한 개선 방법을 주석으로 기록합니다.
3. 참고한 링크 및 ChatGPT 프롬프트 명령어가 있다면 주석으로 남겨주세요.
```python
# 코드 이해도 예시
# minmax_to_rect라는 함수를 구현하여 CAM이 잡은 bounding box도 이미지에 표현되게 하였다.
def minmax_to_rect(bbox, image):
    y_min, x_min, y_max, x_max = bbox
    rect = np.array([
        [int(x_min * image.shape[1]), int(y_min * image.shape[0])],
        [int(x_max * image.shape[1]), int(y_min * image.shape[0])],
        [int(x_max * image.shape[1]), int(y_max * image.shape[0])],
        [int(x_min * image.shape[1]), int(y_max * image.shape[0])]
    ])
    return rect
```
```python
# 코드 간결성 예시
# show_cam이라는 함수를 통해 CAM, Grad-CAM 등에서의 이미지를 한번에 출력할 수 있도록 함.
def show_cam(item, cam_image, title='CAM'):
    image = item['image']
    
    ...

    plt.show()

cam_image = generate_cam(project_cam_model, item)
show_cam(item, cam_image)

grad_image = generate_grad_cam(project_cam_model, 'conv5_block3_out', item)
show_cam(item, grad_image, 'Grad-CAM conv5_3')

grad_image = generate_grad_cam(project_cam_model, 'conv4_block3_out', item)
show_cam(item, grad_image, 'Grad-CAM conv4_3')

grad_image = generate_grad_cam(project_cam_model, 'conv3_block3_out', item)
show_cam(item, grad_image, 'Grad-CAM conv3_3')
```

# 참고 링크 및 코드 개선
```python
# CAM, Grad-CAM 등을 여러 이미지에 적용하여 다양한 이미지에 대한 결과를 비교하는 것도 좋을 것 같습니다.
# 리스트 등을 이용하여 이미지 별 결과를 저장해둔다면 반복문으로 쉽게 구현하실 수 있을거라 생각합니다.👍
```
