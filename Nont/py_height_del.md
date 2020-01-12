Python的垃圾回收机制: `__del__`     
========

创建对象后，python解释器默认调用__init__()方法    
当删除一个对象时，python解释器也会默认调用一个方法, 这个方法为__del__()方法   

在python中，对于开发者来说很少会直接销毁对象(如果需要，应该使用del关键字销毁)  
Python的内存管理机制能够很好的胜任这份工作。

# 结论: 不管是手动调用del还是由python自动回收, 都会触发__del__方法执行     

我们先看一个简单demo, 演示`__del__`魔法方法:      
```Python
class Cat:
    def __init__(self, name):
        self.name = name
        print("%s 来了" % self.name)

    def __del__(self):
        print("%s 我去了" % self.name)

tom = Cat("Tom")
print('This is tom.name: ',tom.name)

# del 关键字可以删除一个对象
del tom
print(tom)
```
输出内容:   
```
Tom 来了
This is tom.name:  Tom
Tom 我去了
Traceback (most recent call last):
  File "D:/07-___del__方法.py", line 21, in <module>
    print(tom)
NameError: name 'tom' is not defined
```

可以看到, tom这个实例对象被我们删除掉了, 找不到就报错了   


# 我们再看一个升级版demo:  
```Python
class Dog:
    pass

dog1 = Dog()
dog2 = dog1

del dog1
```
这个程序是可以运行了    
但是问题来了, Python中不是一切皆引用吗?   
deg2引用dog1,  删除了dog1这个根, dog2这个引申出来的也应该被删除啊?     

Python中有对象内存计数存在:  
#### 删除对象的意思就是这个对象所对应的内存空间被释放了
#### 当dog1被删除了，dog2还在，引用计数减掉1而已，内存还不会被释放


# 我们再看一个升级版demo:  
```Python
class Dog:
    def __init__(self, name):
        self.name = name
		
    def __del__(self):
        print("{}, 英雄over".format(self.name))
		
dog1 = Dog('haha')  # 创建一个对象
dog2 = dog1

del dog1

import time;  print('删除了dog1, 开始沉睡1s');  time.sleep(1); print(' ')

del dog2;  print('删除了dog2, 开始沉睡1s');  time.sleep(1); print(' ')

print("== == == == ==")
```
输出内容:  
```
删除了dog1, 开始沉睡1s
 
haha, 英雄over
删除了dog2, 开始沉睡1s
 
== == == == ==
```

