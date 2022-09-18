# C 基本集

## 变量

直接使用, 无需声明

### 字符串

- 多行文本

  使用三个单引号或者三个双引号

## 条件判断

!> 有冒号

```py
if not exists:
    print("not exists")
elif he and she:
    print("he and she")
else:
    print("else")
```

### 逻辑判断

- `and`
- `or`
- `not`

## 循环

!> 有冒号, 条件总有冒号

- for

  偏好迭代器

  ```py
  for i in range(1, 10):
      print(i)
  ```

- while

  无限循环

- break, continue

## data structure

### List

- access

  索引为负的时候, 从后往前数

  > 索引从 0 开始, 左闭右开

### Dict

便于描述对象

- iteration

  ```py
  for key, value in dict.items():
      print(key, value)
  for key in dict.keys():
      print(key)
  for value in dict.values():
      print(value)
  ```

### Tuple

内容不可变

解包

### Set

用于去重

## 函数

> 对行为的抽象, 参数即是被抽象掉的东西, 函数本体即是骨骼

### 作用域

- 函数内的变量与外部重名

  仍然是局部变量, 覆盖外部

  使用 global 可以引用外部变量

  ```py
  global a
  ```
