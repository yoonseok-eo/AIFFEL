# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 어윤석
- 리뷰어 : 조대호 


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [O] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  > 네 코드가 정상작동 하였고, resnet50으로 모델이 잘 학습되었습니다.
  > 그래프도 그려주어 이해하는데 도움이 되었습니다
- [O] 주석을 보고 작성자의 코드가 이해되었나요?
  > 네. 필요한 부분에 주석을 달아주어 이해하는데 도움이 되었습니다.
- [O] 코드가 에러를 유발할 가능성이 없나요?
  > 에러를 유발할 가능성이 없었습니다.
- [O] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 네validation, test 부분에서  궁금했던 부분들을 답변을 잘 해주셨습니다.
- [O] 코드가 간결한가요?
  > 네 겹치는 부분을 함수로 구현하여 간결하게 작성하였습니다.
'''python
def compile_and_fit(train_data, val_data, epochs=5, model=None):
    if model is None:
        model = get_resnet50()
    model.compile(
        loss='categorical_crossentropy',
        optimizer=tf.keras.optimizers.SGD(learning_rate=0.01),
        metrics=['accuracy'],
    )

    return model, model.fit(
        train_data,
        steps_per_epoch=int(ds_info.splits['train'].num_examples/16),
        validation_steps=int(ds_info.splits['test'].num_examples/16),
        epochs=epochs,
        validation_data=val_data,
        verbose=1,
        use_multiprocessing=True,
    )
'''



# 예시
1. 코드의 작동 방식을 주석으로 기록합니다.
2. 코드의 작동 방식에 대한 개선 방법을 주석으로 기록합니다.
3. 참고한 링크 및 ChatGPT 프롬프트 명령어가 있다면 주석으로 남겨주세요.

