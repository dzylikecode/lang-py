# 迭代器与生成器

## 委托构造

比如有一个类, 内部含有一个迭代器, 可以将这个类的迭代委托给内部的迭代器

```py
def __iter__(self):
    return iter(self._children)
```

## 生成器构造迭代器

`yield`

`next(obj)`会下一个

```py
ele = x * x for x in nums
```

`ele`也是生成器

## 迭代协议

用 Node 表示`Tree`结构

```py
class Node:
    def __init__(self, value):
        self._value = value
        self._children = []

    def __repr__(self):
        return 'Node({!r})'.format(self._value)

    def add_child(self, node):
        self._children.append(node)

    def __iter__(self):
        return iter(self._children)

    def depth_first(self):
        yield self
        for c in self:
            yield from c.depth_first()
```

- [In practice, what are the main uses for the "yield from" syntax in Python 3.3?](https://stackoverflow.com/questions/9708902/in-practice-what-are-the-main-uses-for-the-yield-from-syntax-in-python-3-3)

  `yield from g` is equivalent to `for v in g: yield v`

```py
def depth_first(self):
    yield self
    for c in self:
        yield from c.depth_first()
```

- `yield self`相当于 yield root

- `for c in self`相当于 extract subTree

  `[left subTree, right subTree]`

- `yield from c.depth_first()`: `c`是 node 类, 递归地调用`depth_first`, 进入下一次 for 循环

---

`__iter__`是选择迭代的对象, 返回迭代器, 给`for ... in` 使用

`__next__`是迭代器需要实现的方法

```py
class Node:
    def __init__(self, value):
        self._value = value
        self._children = []

    def __repr__(self):
        return 'Node({!r})'.format(self._value)

    def add_child(self, node):
        self._children.append(node)

    def __iter__(self):
        return iter(self._children)

    def depth_first(self):
        return DepthFirstIterator(self)

class DepthFirstIterator(object):
    '''
    Depth-first traversal
    '''

    def __init__(self, start_node):
        self._node = start_node
        self._children_iter = None
        self._child_iter = None

    def __iter__(self):
        return self

    def __next__(self):
        # Return myself if just started; create an iterator for children
        if self._children_iter is None:
            self._children_iter = iter(self._node)
            return self._node
        # If processing a child, return its next item
        elif self._child_iter:
            try:
                nextchild = next(self._child_iter)
                return nextchild
            except StopIteration:
                self._child_iter = None
                return next(self)
        # Advance to the next child and start its iteration
        else:
            self._child_iter = next(self._children_iter).depth_first()
            return next(self)
```

很复杂

第一个 next 执行第一个`if`, 返回 root, `_children_iter`此时是`root`的两个子节点`[left subTree, right subTree]`

第二个 next 执行第三个`else`, `next(self._children_iter)`调用了 node 的 next, 相当于`for c in self`(调用了 Node 的 next), 取出其中一个 subTree, subTree 的`depth_first`返回了一个迭代器`DepthFirstIterator`, 放到`self._child_iter`中. `return next(self)`, 则会进入第二个`elif`, `nextchild = next(self._child_iter)`实际上是调用了 subTree 的`DepthFirstIterator`的 next, 回到了 subTree 的第一个`if`, 返回子节点的`root`. 最终返回了子节点的 root

> 用类型去查看, 区分`Node`和`DepthFirstIterator`

第三个 next, 执行的是第二个 else, `nextchild = next(self._child_iter)`返回子节点的子节点的 root(第二个过程返回了子节点的 root),实际上重复的是第二个过程. 只用抽象地理解到`nextchild = next(self._child_iter)`代表了对子节点的 DepthFirst

最终会到结尾, `StopIteration`, 此时会到第三个`else`最终, `self._child_iter = next(self._children_iter).depth_first()`开始访问 right subTree

代入一个元素的例子, 知道`else`会产生`StopIteration`

## reverse

`__reversed__`

## itertools

里面有很多高级的概念

chain: 和 Haskell 的`>>=`类似

---

```py
def gen_opener(filenames):
    '''
    Open a sequence of filenames one at a time producing a file object.
    The file is closed immediately when proceeding to the next iteration.
    '''
    for filename in filenames:
        if filename.endswith('.gz'):
            f = gzip.open(filename, 'rt')
        elif filename.endswith('.bz2'):
            f = bz2.open(filename, 'rt')
        else:
            f = open(filename, 'rt')
        yield f
        f.close()
```

后续继续是生成器, f 依然没有关闭, 知道到真正的 for 的时候, 下一个迭代才会关闭

`*gen_opener(filenames)`可以将生成器展开, 也会导致关闭`f`

[Generator Tricks For Systems Programmers](http://dabeaz.com/generators)
