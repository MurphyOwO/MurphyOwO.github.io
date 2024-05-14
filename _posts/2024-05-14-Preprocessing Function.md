---
layout: post
title:  "Preprocessing Function"
date:   {{data}}{{time}}
categories: Data
---



记录一些与处理数据时常用的函数

##### DataFrame

```python
data = [
    [1, 4, 7],
    [2, 5, 8],
    [3, 6, 9]
]
df = pd.DataFrame(data, columns=['A', 'B', 'C'])
print(df)
```

每个DataFrame都有行索引和列标签。

* 查看和检查数据
  * 查看前几行df.head(n=5)默认查看前五行；查看后几行df.tail(n=5)默认查看后5行
  * 查看列名df.columns；查看索引df.index
* 数据选择和过滤
  * 按列选择df['A']返回Series
  * 按行选择df.loc[0]按标签选择；df.iloc[0]按位置选择
* 数据转换
  * 转换为NumPy数组array = df.values or array = df.to_numpy()
  * 转换为CSV文件df.to_csv('data.csv', index=False)



##### `pd.read_csv()`

`pd.read_csv()`是pandas库中的函数，用于读取CSV(逗号分隔值)文件并将其转换为DataFrame对象。

```python
import pamdas as pd

df = pd.read_csv('path_to_file.csv', header=0)
```

* header:指定用作列名的行号，默认为0(即第一行)；如果没有列名，可以设置为“None”。



##### `pd.get_dummies()`

`pd.get_dummies()`是pandas库中的函数，用于将分类变量转换为哑变量(独热编码)。

* 分类变量：取值为有效个类别的变量。例如颜色(红色，蓝色，绿色)。这些变量通常是字符串或标签，而不是数值。
* 哑变量：分类变量转换为了数值。

```python
import pandas as pd

df = pd.DataFrame({'Category': ['A', 'B', 'A', 'C']})
df_encoded = pd.get_dummies(df, columns=['Category'])
label_num = df_encoded.values.argmax(1)
print(label_num)

#输出
#array([0, 1, 0, 2], dtype=int64)
```

* data：输入的数据，可以是DataFrame，Serise或者其他类型数据
* columns：指定需要进行热独编码的列。如果没有指定则对全部分类进行编码。

```python
import numpy as np

# 独热编码矩阵示例
one_hot_labels = np.array([
    [1, 0, 0],
    [0, 1, 0],
    [0, 0, 1]
])

# 使用argmax(1)得到原始分类标签
original_labels = one_hot_labels.argmax(1)
print(original_labels)  # 输出: [0, 1, 2]
```



##### `argmax()`

`argmax()`用于返回沿指定轴最大值的索引。



##### `np.assrray()`

`np.asarray()`是NumPy库中的一个函数，用于将输入数据转换为数组，不需要复制。

```python
import numpy as np

list_data = [1, 2, 3, 4]
array_data = np.asarray(list_data, dtype=np.float32)
print(list_data) #输出[1. 2. 3. 4.]
```

