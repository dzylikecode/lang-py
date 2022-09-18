# 异常

## 处理

```py
try:
    print(1/0)
except ZeroDivisionError:
    print("ZeroDivisionError")
except:
    print("other error")
```

```py
try:
    print(1/0)
except (ZeroDivisionError, NameError):
    print("ZeroDivisionError or NameError")
except IndexError as e:
    print("IndexError", e)
else:
    print("other error")
finally:
    print("finally")
```

## 抛出

```py
if not exists:
    raise Exception("not exists")
```
