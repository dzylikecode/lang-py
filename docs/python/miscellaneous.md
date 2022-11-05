# 杂项

## 浅拷贝与深拷贝

```py
from copy import deepcopy
l = [[1],[2],3]
_l = deepcopy(l)
_l[0][0] = -1
print(_l)
print(l)
```

## generator

生成器就是为循环设计的

那么是因为循环遇到了什么问题，才会有人想要要用生成器呢？ 在循环的时候，我们的目的是为了每次循环拿到一些特定数据，然后为这些数据做处理。但是无可避免的会在内存中记录这些数值， 当需要记录的数值很多的时候，我们的内存可能就吃不消了。而生成器，即现做现吃的意思

我只在需要这个数据的时候生成它，生成完了我就不用了，也不需要记录

```py
def need_return():
    for item in range(5):
        if item % 2 == 0:
            print("我要扔出去一个 item=%d 了" % item)
            yield item  # 这里就会返回给下面的 for 循环
            print("我又回到里面了")

for i in need_return():
    print("我在外面接到了一个 item=%d\n" % i)
```

- 定义生成器类

  - 生成器类必须实现 `__iter__` 和 `__next__` 方法

    - `__iter__` 当我在外面 for 循环进行迭代时，我返回什么？
    - `__next__` 每次迭代的时候，我的函数会放出来什么元素

    ```py
    class NeedReturn:
        def __init__(self, init_value=0):
            self.tmp = init_value
            self.item = 0

        def __iter__(self):
            return self

        def __next__(self):
            while True:
                if self.item == self.tmp:
                    self.tmp *= 2
                    return self.item
                self.item += 1
                if self.item == 300:
                    raise StopIteration

    for i in NeedReturn(10):
        print(i)
    ```

## decorate

当你发现，有一批 Function 都要做些前置或者后置的工作，我们可以统一给他们装修，用一个装饰器统一处理

```py
def decorator(fn):
    def wrapper(name):
        print(name+"say I'm in")    # 这是我的前处理
        return fn(name)
    return wrapper

@decorator
def outer_fn(name):
    print(name+"say I'm out")

outer_fn("mofanpy")
```
