深拷贝--浅拷贝  
====

## 深与浅的区别  
1. 浅拷贝, 复制了引用(指向), 没有复制内容    

2. 深拷贝, 对于一个对象所有层次的复制(递归)   
```Python
import copy

a = [22, 66]
b = copy.deepcopy(a)

print(id(a),  id(b))
```


## 关注点    
- 1. copy.copy对于可变复制([list])类型, 进行浅拷贝  
- 2. copy.copy对于不可变复制类型(turple), 不会拷贝, 仅仅指向  

