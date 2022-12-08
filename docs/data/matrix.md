# matrix

numpy

## install

```bash
pip install numpy
```

- python 3

  ```bash
  pip3 install numpy
  ```

test:

```py
python3 -c "import numpy"
```

## list

对比 python list 的优势:

- 运算快

  用电脑内存中连续的一块物理地址存储数据

### usage

- create:

  ```py
  cars = np.array([
  [
      [5, 10, 12, 6],
      [5.1, 8.2, 11, 6.3],
      [4.4, 9.1, 10, 6.6]
  ],
  [
      [6, 11, 13, 7],
      [6.1, 9.2, 12, 7.3],
      [5.4, 10.1, 11, 7.6]
  ],
  ])
  ```

- merge

  ```py
  print("第一维度叠加：\n", np.concatenate([all_tests, all_tests], axis=0))
  print("第二维度叠加：\n", np.concatenate([all_tests, all_tests], axis=1))
  print("竖直合并\n", np.vstack([a, b]))
  print("水平合并\n", np.hstack([a, b]))
  ```

- info

  ```py
  print("维度：", cars.ndim)
  print("形状：", cars.shape)
  print("元素个数：", cars.size)
  print("元素类型：", cars.dtype)
  ```

- filter

  - 单个选取
    - `array[1]`
    - `array[1,2,3]`
    - `array[1][1]`
  - 切片划分
    - `array[:3]`
    - `array[2:4, 1:3]`
  - 条件筛选
    - `array[array<0]`
    - `np.where(array, array < 0)`

## operator

类似于 matlab

- 加减乘除
  - `+-*/`
  - `np.dot()`
- 数据统计分析
  - `np.max()` `np.min()` `np.sum()` `np.prod()` `np.count()`
  - `np.std()` `np.mean()` `np.median()`
- 特殊运算符号
  - `np.argmax()` `np.argmin()`
  - `np.ceil()` `np.floor()` `np.clip()`

> 我感觉数学常识就不要列出来吧, 分散精力

## 改变数据形态

- 改变形态
  - `array[np.newaxis, :]`
  - `array.reshape()`
  - `array.ravel(), array.flatten()`
  - `array.transpose()`
- 合并
  - `np.column_stack(), np.row_stack()`
  - `np.vstack(), np.hstack(), np.stack()`
  - `np.concatenate()`
- 拆解

  - `np.vsplit(), np.hsplit(), np.split()`

### 改变维度

```py
import numpy as np
a = np.array([1,2,3,4,5,6])
a_2d = a[np.newaxis, :]
a = np.array([1,2,3,4,5,6])
a_none = a[:, None]
a_expand = np.expand_dims(a, axis=1)
a_squeeze = np.squeeze(a_expand)
a_squeeze_axis = a_expand.squeeze(axis=1)
```

numpy.newaxis 效果和 None 是一样的，None 是它的别名 numpy.newaxis 效果和 None 是一样的，None 是它的别名

- [How do I use np.newaxis?](https://stackoverflow.com/questions/29241056/how-do-i-use-np-newaxis)

> 相当于在`none`或者`np.newaxis`的位置增加一个维度(增加一个中括号)

转置:

```py
aT1 = a.T
aT2 = np.transpose(a)
```

## skill

- 过滤非零元素

  ```py
  not_zero_mask = data[:, new_recovered_idx] != 0 # 排除 0
  ratio = data[not_zero_mask, new_cases_idx] / data[not_zero_mask, new_recovered_idx] #利用了切片
  ```

## example

- covid-19
