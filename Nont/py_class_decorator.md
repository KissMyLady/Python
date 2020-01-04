类装饰器 
=====

什么是类装饰器?  
很简单  
我们先看下面一段代码:  
```Python
class Decorator(object):
    pass

@Decorator
def Worker():
    print('Do something')

print(Worker())
```
如果我们要用类装饰一个函数, 我们是这么写的,  现在类里面还没有写任何东西  

实际上, 这里的装饰器decorator表示的含义是: Decorator(Worker)   

### 所以, 问题来了, 我们类里面该写点什么 ?   
```Python
class Decorator(object):
    def __call__(self):
        pass
```
### 于是, 我们通过类里面的魔法方法就可以Decorator()直接在里面写参数然后调用  
就像这样的代码:   
```
class Get(object):
    def __init__(self, a, b):
        self.a = a
        self.b = b

    def __call__(self, x):
        result = self.a * x + self.b
        print(result)
```
然后调用:  
```Python
c = Get(3, 7)
c(4)
```
我们做到了直接调用类方法: `c(4)`   

### 所以, 上面看起来应该像是这样:  
```Python
class Decorator(object):
    def __call__(self):
        print('Do something)
```
这样还不够, 仅仅调用了装饰器的`Do something`, 没有调用装饰的函数, 我们需要再把函数写进去   
```Python
class Decorator(object):
    def __init__(self, func):
        self.__func = func

    def __call__(self):
        print('Do something)
        self.__func()
```
```
@Decorator
def Worker():
    print('Do something')

print(Worker())
```
如此这样即可  



## 继续分析分析  
```Python
class Decorator(object):
    def __init__(self, func):
        print(func)
        self.__name__ = func
        self.__func = func

    def __call__(self):
        print('decorator work: Do something')
        print(self.__name__)
        print(self.__func)
        self.__func()
    
@Decorator
def Worker():
    print('work one: Do something')

print(Worker())
```
打印结果:  
```Linux
<function Worker at 0x000002BF236B4378>
decorator work: Do something
<function Worker at 0x000002BF236B4378>
<function Worker at 0x000002BF236B4378>
work one: Do something
None
```
我们发现, 这里的三种方法都一样:      
```Linux
print(func) ------------------<function Worker at 0x000002BF236B4378>
self.__name__ = func ---------<function Worker at 0x000002BF236B4378>
self.__func = func   ---------<function Worker at 0x000002BF236B4378>
```
这三种方法都可以, 所以, 任选其一即可  


这三种方法演示:      
### 第一种`func`方法:    
```Python
class Decorator(object):
    def __init__(self, func):
        self.func = func

    def __call__(self):
        print('decorator work: Do something')
        self.func()

@Decorator
def Worker():
    print('work one: Do something')
	
Worker()

# 打印结果:  

# decorator work: Do something
# work one: Do something
```

### 第二种`__func`方法:    
```Python
class Decorator(object):
    def __init__(self, func):
        self.__func = func

    def __call__(self):
        print('decorator work: Do something')
        self.__func()

@Decorator
def Worker():
    print('work one: Do something')
	
Worker()

# 打印结果:

# decorator work: Do something
# work one: Do something
```

### 第三种`__func`方法:    
```Python
class Decorator(object):
    def __init__(self, func):
        self.__name__ = func

    def __call__(self):
        print('decorator work: Do something')
        self.__name__()

@Decorator
def Worker():
    print('work one: Do something')
	
Worker()

# 打印结果:  
# decorator work: Do something
# work one: Do something
```
### [Python常用内建方法：__init__,__new__,__class__的使用详解](https://blog.csdn.net/qq_26442553/article/details/82464682)


#### 1.每天进步一丢丢，做个有趣的人    
#### 2.种一棵树最好时间是十年前，其次是现在     
#### 3.每个人都有一个觉醒期，但觉醒的早晚决定个人的命运    
#### 4.知行合一，知道了不去做，等于不知道    
