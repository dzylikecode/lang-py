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

## overload operator

```py
"""Binary Operators:
Operator Magic Method"""
+ __add__(self, other)
– __sub__(self, other)
* __mul__(self, other)
/ __truediv__(self, other)
// __floordiv__(self, other)
% __mod__(self, other)
** __pow__(self, other)
>> __rshift__(self, other)
<< __lshift__(self, other)
& __and__(self, other)
| __or__(self, other)
^ __xor__(self, other)
"""Comparison Operators :
Operator Magic Method"""
< __LT__(SELF, OTHER)
> __GT__(SELF, OTHER)
<= __LE__(SELF, OTHER)
>= __GE__(SELF, OTHER)
== __EQ__(SELF, OTHER)
!= __NE__(SELF, OTHER)
"""Assignment Operators :
Operator Magic Method"""
-= __ISUB__(SELF, OTHER)
+= __IADD__(SELF, OTHER)
*= __IMUL__(SELF, OTHER)
/= __IDIV__(SELF, OTHER)
//= __IFLOORDIV__(SELF, OTHER)
%= __IMOD__(SELF, OTHER)
**= __IPOW__(SELF, OTHER)
>>= __IRSHIFT__(SELF, OTHER)
<<= __ILSHIFT__(SELF, OTHER)
&= __IAND__(SELF, OTHER)
|= __IOR__(SELF, OTHER)
^= __IXOR__(SELF, OTHER)
"""Unary Operators :
Operator Magic Method"""
– __NEG__(SELF, OTHER)
+ __POS__(SELF, OTHER)
~ __INVERT__(SELF, OTHER)
```
