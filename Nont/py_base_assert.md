断言的使用方法
====
在开发一个程序时候, 与其让它运行时崩溃, 不如在它出现错误条件时就崩溃（返回错误）。

这时候断言assert 就显得非常有用。

assert的语法格式：
```Python
assert expression
```
### 检查条件, 不符合就终止程序  

它的等价语句为：
```Python
if not expression:
    raise AssertionError
```

这段代码用来检测数据类型的断言，因为 a_str 是 str 类型，所以认为它是 int 类型肯定会引发错误。
```Python
>>> a_str = 'this is a string'
>>> type(a_str)
<type 'str'>
>>> assert type(a_str) == str
>>> assert type(a_str) == int
```
```Python
Traceback (most recent call last):
  File "<pyshell#41>", line 1, in <module>
    assert type(a_str)== int
AssertionError
```


