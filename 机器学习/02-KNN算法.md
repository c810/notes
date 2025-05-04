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

### 1.2 KNN 算法 API 介绍

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

## 2 鸢尾花识别案例

### 2.1 普通 KNN 版

```python
# 0.导入工具包
from sklearn.datasets import load_iris  # 加载鸢尾花数据集
from sklearn.model_selection import train_test_split  # 数据集划分
from sklearn.preprocessing import StandardScaler  # 数据标准化
from sklearn.neighbors import KNeighborsClassifier  # KNN算法
import pandas as pd  # 数据处理
import matplotlib.pyplot as plt  # 可视化
import seaborn as sns  # 可视化


def lm01_loadiris():
    # 1.加载数据集
    # 加载鸢尾花数据集
    mydataset = load_iris()
    print(mydataset.feature_names)  # 查看特征名
    # print(mydataset)
    # print('\n查看数据集信息 mydataset.data[:5]：\n', mydataset.data[:5]) # 查看数据集信息，查看前5行
    # print('\n查看目标值 mydataset.target：\n', mydataset.target) # 查看目标值
    # print('\n查看目标值名字 mydataset.target_names：\n', mydataset.target_names) # 查看目标值名字
    # print('\n查看数据集描述 mydataset.DESCR：\n', mydataset.DESCR) # 查看数据集描述
    # print('\n查看数据文件路径 mydataset.filename：\n', mydataset.filename) # 数据文件路径

    # 2.数据展示（可以不展示）
    # 把数据转换成dataframe格式，设置data、columns属性
    iris_d = pd.DataFrame(mydataset['data'], columns=mydataset['feature_names'])
    # 再加一列目标值
    iris_d['Species'] = mydataset.target
    print(iris_d)
    # 然后从特征值中选择两个特征值进行可视化，哪个分类效果好就选哪两个
    col1 = 'sepal length (cm)'  # 特征1，花萼长度
    col2 = 'petal width (cm)'  # 特征2，花瓣宽度
    # col2 = 'petal length (cm)' # 特征3，花瓣长度
    # col2 = 'sepal width (cm)' # 特征4，花萼宽度
    # 绘制散点图，hue='Species'表示根据目标值进行分类，fit_reg=False表示不拟合回归曲线
    sns.lmplot(x=col1, y=col2, data=iris_d, hue='Species', fit_reg=False)
    plt.xlabel(col1)
    plt.ylabel(col2)
    plt.title('Iris Dataset')
    plt.show()

    # 3.特征工程（预处理-标准化）
    # 3.1.数据集划分
    X_train, X_test, y_train, y_test = train_test_split(mydataset.data, mydataset.target, test_size=0.3, random_state=22)
    # print('数据总数', len(mydataset.data))
    # print('训练集数据总数', len(X_train))
    # print('测试集数据总数', len(X_test))
    # 3.2.数据标准化
    process = StandardScaler()
    X_train = process.fit_transform(X_train)
    X_test = process.transform(X_test)
    
    # 4.模型训练
    estimator = KNeighborsClassifier(n_neighbors=3)
    estimator.fit(X_train, y_train)

    # 5.模型评估
    # 直接计算准确率，100个样本中模型预测对多少
    myscore = estimator.score(X_test, y_test)
    print('模型预测准确率：', myscore)
    
    # 6.模型预测
    # 需要对待预测数据，执行标准化
    print('通过模型查看分类类别：', estimator.classes_)
    x_data = [[5.1, 3.5, 1.4, 0.2], [4.6, 3.1, 1.5, 0.2]]
    x_data = process.transform(x_data)
    print('标准化后的数据：', x_data)
    y_pred = estimator.predict(x_data)
    print('预测鸢尾花类别：', y_pred)
    print('不同类别的概率：', estimator.predict_proba(x_data))
    

if __name__ == '__main__':
    lm01_loadiris()
```

### 2.2 网格搜索交叉验证版

```python
# 0.导入工具包
from sklearn.datasets import load_iris  # 加载鸢尾花数据集
from sklearn.model_selection import GridSearchCV, train_test_split  # 数据集划分
from sklearn.preprocessing import StandardScaler  # 数据标准化
from sklearn.neighbors import KNeighborsClassifier  # KNN算法
import pandas as pd  # 数据处理
import matplotlib.pyplot as plt  # 可视化
import seaborn as sns  # 可视化


def lm01_loadiris():
    # 1.加载数据集
    mydataset = load_iris()

    # 3.特征工程（预处理-标准化）
    # 3.1.数据集划分
    X_train, X_test, y_train, y_test = train_test_split(mydataset.data, mydataset.target, test_size=0.2, random_state=22)
    # 3.2.数据标准化
    process = StandardScaler()
    X_train = process.fit_transform(X_train)
    X_test = process.transform(X_test)
    
    # 4.模型训练
    # 4.1.初始化模型
    estimator = KNeighborsClassifier()   
    # 4.2.网格搜索交叉验证
    param_grid = {'n_neighbors': [1, 3, 5, 7]}
    estimator = GridSearchCV(estimator=estimator, param_grid=param_grid, cv=5) # 给estimator附魔，网格搜索交叉验证
    # 4.3.训练模型
    estimator.fit(X_train, y_train) # 4个模型，每个模型5折交叉验证
    print('最佳参数：', estimator.best_params_)
    print('最佳结果：', estimator.best_score_)
    print('最佳估计器：', estimator.best_estimator_)
    print('交叉验证结果：', estimator.cv_results_)
    # 4.4.保存交叉验证结果
    cv_results = pd.DataFrame(estimator.cv_results_)
    cv_results.to_csv(path_or_buf='./gridsearchcv_results.csv')
    
    # 5.模型评估
    myscore = estimator.score(X_test, y_test)
    print('模型预测准确率：', myscore)
    

if __name__ == '__main__':
    lm01_loadiris()
```

## 3 手写数字识别案例

### 3.1 KNN 算法实现手写数字识别

数据集介绍：

1. 数据文件 train. csv 和 test. csv 包含从 0 到 9 的手绘数字的灰度图像。
2. 每个图像 28 x 28，共 784 个像素。
3. 每个像素取值范围\[0, 255\]，0 为黑。
4. 训练数据集（train. csv）共 785 列。第一列为标签，为该图片对应的手写数字。其余 784 列为该图像的像素值。
5. 训练集中的特征名称均有 pixel 前缀，后面的数字（\[0, 783\]）代表了像素的序号。

![[Pasted image 20250426214105.png]]
