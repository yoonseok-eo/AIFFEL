# AIFFEL Campus Online Code Peer Review Templete
- 코더 : 어윤석
- 리뷰어 : 최예나


# PRT(Peer Review Template)
- [ㅇ]  **1. 주어진 문제를 해결하는 완성된 코드가 제출되었나요?**
    - 문제에서 요구하는 최종 결과물이 첨부되었는지 확인
    - 문제를 해결하는 완성된 코드란 프로젝트 루브릭 3개 중 2개, 
      퀘스트 문제 요구조건 등을 지칭
        - 해당 조건을 만족하는 코드를 캡쳐해 근거로 첨부



네 아래 코드를 보시면 1, 2, 3 평가문항을 제대로 완수하였습니다
```
# inference 전용 모델
input_data = model.get_layer('input_image').output
y_pred = model.get_layer('output').output
model_crnn = Model(inputs=input_data, outputs=y_pred)

def decode_predict_ctc(out, chars = TARGET_CHARACTERS):
    results = []
    indexes = K.get_value(
        K.ctc_decode(
            out, input_length=np.ones(out.shape[0]) * out.shape[1],
            greedy=False , beam_width=5, top_paths=1
        )[0][0]
    )[0]
    text = ""
    for index in indexes:        
        #999... 숫자 출력x
        if index == -1:
            continue
        text += chars[index]
    results.append(text)
    return results

def recognize_img(pil_img, input_img_size=(100,32)):
    try:
        img = pil_img.convert('RGB')
    except IOError:
        img = Image.new('RGB', img_size)
        label = '-'
    width, height = img.size
    target_width = min(int(width*input_img_size[1]/height), input_img_size[0])
    target_img_size = (target_width, input_img_size[1])
    resize_img = img.resize(target_img_size)
    img = np.array(resize_img).transpose(1,0,2)
    input_image = np.zeros([1, *input_img_size, 3])
    width = img.shape[0]
    input_image[0,:width,:,:] = img
    output = model_crnn.predict(input_image)
    result = decode_predict_ctc(output, chars="-"+TARGET_CHARACTERS)[0].replace('-','')
    pil_img.show()
    resize_img.show()
    print("Result: \t", result)
```
    
- [ㅇ]  **2. 전체 코드에서 가장 핵심적이거나 가장 복잡하고 이해하기 어려운 부분에 작성된 
  주석 또는 doc string을 보고 해당 코드가 잘 이해되었나요?**
    - 해당 코드 블럭에 doc string/annotation이 달려 있는지 확인
    - 해당 코드가 무슨 기능을 하는지, 왜 그렇게 짜여진건지, 작동 메커니즘이 뭔지 기술.
    - 주석을 보고 코드 이해가 잘 되었는지 확인
        - 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부합니다.
     
![스크린샷 2023-09-11 오후 6 17 50](https://github.com/yoonseok-eo/AIFFEL/assets/83259497/87376f25-96f7-408a-a952-ef5118e36301)


  
- [x]  **3. 에러가 난 부분을 디버깅하여 문제를 “해결한 기록을 남겼거나” 
  ”새로운 시도 또는 추가 실험을 수행”해봤나요?**
    - 문제 원인 및 해결 과정을 잘 기록하였는지 확인
    - 문제에서 요구하는 조건에 더해 추가적으로 수행한 나만의 시도, 
      실험이 기록되어 있는지 확인
        - 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부합니다.
  
- [ ]  **4. 회고를 잘 작성했나요?**
    - 주어진 문제를 해결하는 완성된 코드 내지 프로젝트 결과물에 대해
    배운점과 아쉬운점, 느낀점 등이 기록되어 있는지 확인
    - 전체 코드 실행 플로우를 그래프로 그려서 이해를 돕고 있는지 확인
        - 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부합니다.

![스크린샷 2023-09-11 오후 6 19 48](https://github.com/yoonseok-eo/AIFFEL/assets/83259497/314ebb2d-ae83-49dd-a3e0-ee74aa7ceb7a)



- [ ]  **5. 코드가 간결하고 효율적인가요?**
    - 파이썬 스타일 가이드 (PEP8) 를 준수하였는지 확인
    - 하드코딩을 하지않고 함수화, 모듈화가 가능한 부분은 함수를 만들거나 클래스로 짰는지
    - 코드 중복을 최소화하고 범용적으로 사용할 수 있도록 함수화했는지
        - 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부합니다.

![스크린샷 2023-09-11 오후 6 20 11](https://github.com/yoonseok-eo/AIFFEL/assets/83259497/dd75aac9-d8ea-48c4-8233-fefdf14878b6)


이런식으로 lambda함수를 쓰심으로 전체적인 코드를 간결하게 하신 부분이 좋았습니다. 



# 참고 링크 및 코드 개선
```
# 코드 리뷰 시 참고한 링크가 있다면 링크와 간략한 설명을 첨부합니다.
# 코드 리뷰를 통해 개선한 코드가 있다면 코드와 간략한 설명을 첨부합니다.
```
