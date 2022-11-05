# string

## 百分号模式

```py
print("我的名字是 %s !我 %d 岁了，我是 %s 的~" % (name, age, gender))
print("我的名字是 %(nm)s !我 %(age)d 岁了，我是 %(gd)s 的~" % {"nm": name, "age":age, "gd":gender})
```

| format | type |
| :----: | :--: |
|   %d   | 整数 |
|   %i   | 整数 |
|   %f   | 小数 |
|   %s   | 字符 |

```py
print("%f" % (1/3))     # 后面不限制
print("%.2f" % (1/3))   # 后面限制 2 个位置
print("%4d" % (1/3))    # 前面补全最大 4 个位置
print("%5d" % 12)       # 前面补全最大 5 个位置
```

> `5.2f` 表示前面补全最大 5 个位置, 后面限制 2 个位置

### format

```py
print("我的名字是 {} !我 {} 岁了，我 {} 米高~".format(name, age, height))
```

```py
print("我的名字是 {nm} !我 {age} 岁了，我 {ht} 米高~我是{nm}".format(nm=name, age=age, ht=height))
print("我 {ht:.1f} 米高".format(ht=1.12345))
```
