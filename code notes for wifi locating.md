隨機森林法則![image](https://github.com/user-attachments/assets/0b9edfcb-cf05-48aa-82ec-2c049e4141ff)![image](https://github.com/user-attachments/assets/1af7f702-18bc-4a18-a72a-b4ace1342c63)
![image](https://github.com/user-attachments/assets/4ad4fbc7-f0b2-4612-a140-012b5b85c39a)
code:
from sklearn.ensemble import RandomForestRegressor
from sklearn.model_selection import GridSearchCV

## can be updated to include a greater variety of parameters and their values to explore
from sklearn.ensemble import RandomForestRegressor
from sklearn.model_selection import RandomizedSearchCV  # 或 GridSearchCV

# 1. 定義要搜尋的參數格線
param_dist = {
    'n_estimators':      [50, 100, 150],
    'max_features':      ['sqrt', 'log2'],
    'max_depth':         [None, 10, 20],
    'min_samples_split': [2, 5],
    'min_samples_leaf':  [1, 2],
    'bootstrap':         [True]
}

# 基底模型
forest = RandomForestRegressor(random_state=42, n_jobs=-1)

# 隨機搜尋：只試 10 組參數
rand_search = RandomizedSearchCV(
    estimator=forest,
    param_distributions=param_dist,
    n_iter=10,                # 只試 10 種組合
    cv=3,                     # 3 折交叉驗證
    scoring='neg_mean_squared_error',
    random_state=42,
    n_jobs=-1,
    return_train_score=False
)

# 執行
rand_search.fit(feats_train, targets_train)

# 5. 查看最佳參數
print("Best params:", rand_search.best_params_)

# you can check out the result details in a dataframe format
cvres = rand_search.cv_results_
pd.set_option("max_colwidth", 80)
df_cvres = pd.DataFrame(cvres)
df_cvres[["params", "mean_test_score", "std_test_score"]]
def mean_error_dist(targets, preds):
    # TODO: implement the function
    dist = 0
    for i in range(len(targets)):
      dist += np.linalg.norm(targets[i] - preds[i])
    dist /= len(targets)
    return dist
  from sklearn.metrics import mean_squared_error

forest_preds = rand_search.best_estimator_.predict(feats_val)

forest_med = mean_error_dist(targets_val, forest_preds)

forest_mse = mean_squared_error(targets_val, forest_preds)
forest_rmse = np.sqrt(forest_mse)

print("Random Forest. RMSE: {:.3f}, MSE: {:.3f}, MED: {:.3f}".format(forest_rmse, forest_mse, forest_med))
變異係數Coefficient of variation:![image](https://github.com/user-attachments/assets/83d8a1c8-fedb-4c8d-b9da-554118cdfc7a)![image](https://github.com/user-attachments/assets/d115b4a1-c71f-497b-b23a-2ff9f6d2154a)
決策樹中兩個重要參數1.![image](https://github.com/user-attachments/assets/56c477ae-375c-4163-87de-72ee5ad2b21b)
2. ![image](https://github.com/user-attachments/assets/1139761f-f4a6-4bb9-8960-ce8c26e68a3f)
更多資訊可以參照https://ithelp.ithome.com.tw/m/articles/10296318

