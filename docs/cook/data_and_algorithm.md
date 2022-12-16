# data and algorithm

## 解包

丢弃不需要的值, 就是赋给自己不会用到的变量

```py
a, _, b = [1, 2, 3]
```

`_`就是一个变量, 只要保证自己接下来不会用到即可

---

剩余的丢尽列表

```py
a, *b, c = [1, 2, 3, 4]
# b = [2, 3]
```

`*b`就是一个列表, 里面包含了剩余的值

- 运用

  python 传递的参数是元组, 同样可以这样解包

  ```py
  def test(a, *b, c):
      print(a, b, c)
  ```

  for 循环也是

  ```py
  for a, *b, c in [[1, 2, 3, 4], [5, 6, 7, 8]]:
      print(a, b, c)
  ```

---

生成器的应用

将搜索过程与使用搜索结果进行解耦

使用 yeild 来构造生成函数

## 优先级

- queue
- heap

相同的优先级不方便比较, 可以在添加一个变量来区分, 比如放入的顺序

```py
(1, move) < (1, up) # error move up 不能比较
(1, 0, move) < (1, 1, up) # true
```

tuple 重载了比较运算符, 一个一个的比较, 直到 true 或 false

适用于字典的比较

```py
sorted(zip(dict1.values(), dict1.keys()))
```

先比较 values, 再比较 keys

---

zip 建立的迭代器只能被消费一次

```py
prices_and_names = zip(prices, names)
min_price = min(prices_and_names) # ok
min_price = max(prices_and_names) # error 不能再次使用
```

---

找相同的, 利用集合的运算去思考: 交集

像数学一样思考

---

去重, 并保持相对位置不变

用函数式思考, 相当于一个容器变成另一个容器

如文件去重:

```py
with open('somefile', 'r') as f:
    for line in dedupe(f):
        print(line)
```

- `dedupe(f)`

  文件"f"变成去重后的行数, 可以提供一个 lambda 表达式将不可"hashable"的对象转换为可 hashable 的对象
