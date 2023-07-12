# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 어윤석
- 리뷰어 : 윤상현

# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- :white_check_mark: 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
- :warning: 주석을 보고 작성자의 코드가 이해되었나요?
  > 주석이 거의 없어서, 처음 코드를 보는 사람은 이해에 시간이 좀 필요할 것 같습니다.
- :white_check_mark: 코드가 에러를 유발할 가능성이 없나요?
- :white_check_mark: 코드 작성자가 코드를 제대로 이해하고 작성했나요?
- :white_check_mark: 코드가 간결한가요?

# 예시
1. 코드의 작동 방식을 주석으로 기록합니다.
2. 코드의 작동 방식에 대한 개선 방법을 주석으로 기록합니다.
3. 참고한 링크 및 ChatGPT 프롬프트 명령어가 있다면 주석으로 남겨주세요.
```python
# 1. 정규화 - 불균형한 데이터를 log를 사용하여 다시 분포를 확인한게 인상깊었습니다.
skew_columns = ['bedrooms', 'sqft_living', 'sqft_lot', 'sqft_above', 'sqft_basement', 'sqft_lot15']
for c in skew_columns:
    X[c] = np.log1p(X[c].values)

show_kdeplot(X)

y = np.log1p(y)
sns.kdeplot(y)
plt.show()

# 2. GridSearch - 함수화하여 바로바로 불러올 수 있게 함으로 OOP의 장점을 잘 살린 것 같습니다.
# 코드도 잘 동작하여 간결하고 좋았습니다.
def my_GridSearch(models, X, y, param_grid, verbose=2, n_jobs=5):
    results = pd.DataFrame()
    for model in models:
        grid_model = GridSearchCV(model, param_grid=param_grid, scoring='neg_mean_squared_error', \
                                cv=5, verbose=verbose, n_jobs=n_jobs)
        grid_model.fit(X, y)
        params = grid_model.cv_results_['params']
        score = grid_model.cv_results_['mean_test_score']
        
        tmp = pd.DataFrame(params)
        tmp['score'] = score
        tmp['RMSLE'] = np.sqrt(-1 * score)
        tmp['model'] = model.__class__.__name__
        results = pd.concat([results, tmp])
    return results.sort_values('RMSLE')

param_grid = {
    'n_estimators': [500, 1000],
    'max_depth': [5, 10],
    'learning_rate': [0.1]
}

results = my_GridSearch(models, X, y, param_grid)
```

# 참고 링크 및 코드 개선
```python
# 주석을 달아 코드의 이해를 도와주시면 도움이 될 것 같습니다.
```
