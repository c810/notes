## 1 KNN 算法简介

K- 近邻算法（K Nearest Neighbor，简称 KNN）。

### 1.1 KNN 思想

如果一个样本在特征空间（训练集）中的 **k 个最相似的样本**中的大多数属于某一个类别，则该样本也属于这个类别。

样本相似性：样本都是属于一个任务数据集的，样本**距离越近则越相似**。

例如用欧式距离：

![[Pasted image 20250424214431.png]]

具体流程：计算未知样本到每个训练样本的距离，将训练样本根据距离大小升序排列，取出距离最近的 K 个训练样本：

- 分类：进行**多数表决**，统计 K 个样本中哪个类别的样本个数最多，则归属到那个样本。
- 回归：把这 K 个样本的目标值**计算其平均值**，作为样本的预测的值。

K 值为超参数，需要人为设置。K 过小：容易受异常点影响，K 减小意味着整体模型变得复杂，容易过拟合。K 过大：受到样本均衡的问题，且容易欠拟合。

那么如何对 K 超参数进行调优？下面会讲到：交叉验证、网格搜索。

## 2 KNN 算法 API 介绍

```python
from sklearn.neighbors import KNeighborsClassifier, KNeighborsRegressor

# 分类问题
def knn_api_classifier():
    # 实例化模型，这里的 estimator 随意改名，比如 model
    estimator = KNeighborsClassifier(n_neighbors=1)
    # 数据集
    X = [[0], [1], [2], [3]]
    y = [0, 0, 1, 1]
    # 训练模型
    estimator.fit(X, y)
    # 预测
    print(estimator.predict([[4]])) # [1]

# 回归问题
def knn_api_regressor():
    estimator = KNeighborsRegressor(n_neighbors=2)
    X = [[0,0,1], [1,1,0], [3,10,10], [4,11,12]]
    y = [0.1, 0.2, 0.3, 0.4]
    estimator.fit(X, y)
    print(estimator.predict([[3,11,10]])) # [0.35]

if __name__ == '__main__':
    knn_api_classifier()
    knn_api_regressor()
```

### 2.1 鸢尾花识别案例

## 3 超参数选择方法

### 3.1 交叉验证

### 3.2 网格搜索

### 3.3 手写数字识别案例
