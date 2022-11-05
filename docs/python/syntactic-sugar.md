# 语法糖

Syntactic sugar

## Lambda

```py
add = lambda a, b: a+b
```

## for

```py
l = [i*2 for i in range(10)]
d = {"index"+str(i): i*2 for i in range(10)}
```

## if

```py
a = 1 if done else 2
```

## for-if

```py
l = [i*2 for i in range(10) if i%2==0]
```

## enumerate

自动加 index

```py
l = [11,22,33,44]
d = {}
for count, data in enumerate(l, start=5):
    d[count] = data
print(d)
# {5: 11, 6: 22, 7: 33, 8: 44}
```

## Zip

同时迭代

```py
name = ["a", "b", "c"]
score = [1,2,3]
bonus = [1,0,1]
d = {}
for n, s, b in zip(name, score, bonus):
    d[n]=s+b
print(d)
```
