# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 어윤석
- 리뷰어 : 김범준

# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [V] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  > 
- [ ] 주석을 보고 작성자의 코드가 이해되었나요?
  > 간혹 주석이 달려있지 않은 코드가 있었다.
- [V] 코드가 에러를 유발할 가능성이 없나요?
  > 에러 없이 잘 작동하는 코드들을 볼 수 있었다.
- [V] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 위 항목에 대한 근거 작성 필수
- [V] 코드가 간결한가요?
  > 비교적 간결한 편인 것 같다.

# 예시
1. 코드의 작동 방식을 주석으로 기록합니다.
2. 코드의 작동 방식에 대한 개선 방법을 주석으로 기록합니다.
3. 참고한 링크 및 ChatGPT 프롬프트 명령어가 있다면 주석으로 남겨주세요.
```python
# 사칙 연산 계산기
class calculator:
    # 예) init의 역할과 각 매서드의 의미를 서술
    def __init__(self, first, second):
        self.first = first
        self.second = second
    
    # 예) 덧셈과 연산 작동 방식에 대한 서술
    def add(self):
        result = self.first + self.second
        return result

a = float(input('첫번째 값을 입력하세요.')) 
b = float(input('두번째 값을 입력하세요.')) 
c = calculator(a, b)
print('덧셈', c.add()) 
```

# 참고 링크 및 코드 개선
```python
# 코드 리뷰 시 참고한 링크가 있다면 링크와 간략한 설명을 첨부합니다.
# 코드 리뷰를 통해 개선한 코드가 있다면 코드와 간략한 설명을 첨부합니다.
```
### project_01

#### (5)
* X_train.shape[1] --> X.shape[1]

#### (6)
* 문제에 맞추어 손실함수 MSE를 정의하는 것이 좋을 것 같다.

#### (9)
* 모델 학습 epoch를 줄여 overfitting을 방지하자.

### project_02

#### (3)
* plt.tight_layout()를 추가해 frame에 적합하게 맞춰보기

#### Additionally,
* Column(feature)를 선정하는 데 기준을 염두해 feature engineering 과정을 거치는 것이 좋을 것 같다.



