### [all方法与any方法](https://blog.csdn.net/u010339879/article/details/80459476)

all 一般判断, 所有元素都不为空, 返回True   
有一个假, 返回假(包含{}, [], 0, false(), '')
请注意, 这里都是可迭代对象判断(iterable)
```Python
names  = ('name', 'laoda', 'laoer', )
names2 = ('name', 'laoda', 'laoer', False)
names3 = ('name', 'laoda', 'laoer', [])

print(all(names))   # True
print(all(names2))  # False
print(all(names3))  # False
```

any 一般判断 是否值全部为空, 0, false 这种情况.
any 判断iterable 全为空 返回False
有一个为真, 返回 真 True

```Python
# 简单来说, 有一个不为空, 返回True
names    = ('frank', 'lijiaxuan', 'weiliang', 'lile', ' ')
defaults = ('', None, [], (), False,)
hobbys   = ['name', False, [], (), ]

print(any(names))     # True
print(any(defaults))  # False
print(any(hobbys))    # True
```
