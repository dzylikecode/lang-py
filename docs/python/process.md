# 多进程

对比多线程代码

## lib

```py
import multiprocessing as mp
import threading as td
```

## create

```py
t1 = td.Thread(target=job,args=(1,2))
p1 = mp.Process(target=job,args=(1,2))
```

## start

```py
t1.start()
p1.start()
```

## join

```py
t1.join()
p1.join()
```

## return

Queue 的功能是将每个核或线程的运算结果放在队里中，等到每个线程或核运行完毕后再从队列中取出结果，继续加载运算

线程调用的函数不能有返回值

## effect

运行时间依然是 多进程 < 普通 < 多线程

效率: 多线程 > 普通 > 多进程

## 进程池

`map` method:

```py
import multiprocessing as mp

def job(x):
    return x*x
def multicore():
    pool = mp.Pool()
    res = pool.map(job, range(10))
    print(res)

if __name__ == '__main__':
    multicore()
# python [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```

> `range(10)`是迭代传递的参数

`apply_async` method

只能传递一个值，它只会放入一个核进行运算，但是传入值时要注意是可迭代的，所以在传入值后需要加逗号, 同时需要用 `get()` 方法获取返回值

```py
def multicore():
    pool = mp.Pool()
    res = pool.map(job, range(10))
    print(res)
    res = pool.apply_async(job, (2,))
    # 用get获得结果
    print(res.get())
    # 迭代器，i=0时apply一次，i=1时apply一次等等
    multi_res = [pool.apply_async(job, (i,)) for i in range(10)]
    # 从迭代器中取出
    print([res.get() for res in multi_res])
```

## shared memory

```py
import multiprocessing as mp

value1 = mp.Value('i', 0)
value2 = mp.Value('d', 3.14)
array = mp.Array('i', [1, 2, 3, 4])
```

- [Efficient arrays of numeric values](https://docs.python.org/3.5/library/array.html)

## Lock

```py
def job(v, num, l):
    l.acquire() # 锁住
    for _ in range(5):
        time.sleep(0.1)
        v.value += num # 获取共享内存
        print(v.value)
    l.release() # 释放

def multicore():
    l = mp.Lock() # 定义一个进程锁
    v = mp.Value('i', 0) # 定义共享内存
    p1 = mp.Process(target=job, args=(v,1,l)) # 需要将lock传入
    p2 = mp.Process(target=job, args=(v,3,l))
    p1.start()
    p2.start()
    p1.join()
    p2.join()

if __name__ == '__main__':
    multicore()
```
