[Python内存管理机制](https://www.cnblogs.com/geaozhang/p/7111961.html)
===

Python的内存管理机制：引用计数、 垃圾回收、 内存池机制

## 1. 引用计数:  
在Python中, 每个对象都有指向该对象的引用总数, 引用计数   

查看对象的引用计数: sys.getrefcount()   
### 1. 普通引用
```Python
good_day = [10000]
import sys

con = sys.getrefcount(good_day)
print(con)
```
![ScreenShot-00341](https://github.com/KissMyLady/Python/blob/master/Img/Python/ScreenShot-00341.jpg)     
当使用某个引用作为参数，传递给getrefcount()时，参数实际上创建了一个临时的引用。
因此，getrefcount()所得到的结果，会比期望的多1   

### 2. 容器对象
Python的一个容器对象(比如：表、词典等)，可以包含多个对象   

容器对象中包含的并不是元素对象本身，是指向各个元素对象的引用   
![ScreenShot-00342](https://github.com/KissMyLady/Python/blob/master/Img/Python/ScreenShot-00342.jpg)  

### 3. 引用计数增加   
#### 1. 对象被创建   
![ScreenShot-00343](https://github.com/KissMyLady/Python/blob/master/Img/Python/ScreenShot-00343.jpg)  

#### 2. 另外的别人被创建   
![ScreenShot-00344](https://github.com/KissMyLady/Python/blob/master/Img/Python/ScreenShot-00344.jpg)  
```Python
good_day = [10000]
import sys

con = sys.getrefcount(good_day)
# print(con)

print(sys.getrefcount(6666666))

n = 6666666
print(sys.getrefcount(6666666))

mm = n
print(sys.getrefcount(6666666))
```
#### 3. 作为容器对象的一个元素
![ScreenShot-00345]()  
```Python
good_day = [10000]
import sys

con = sys.getrefcount(good_day)
# print(con)

print(sys.getrefcount(6666666))

n = 6666666
print(sys.getrefcount(6666666))

mm = n
print(sys.getrefcount(6666666))

importt = [1,2,3,6666666]
print(sys.getrefcount(6666666))
```
#### 4. 被作为参数传递给函数: `foo(x)`

### 4. 引用计数减少  
1、对象的别名被显式的销毁, 使用`del`方法   
```Python
del m
sys.getrefcount(123)
Out[47]: 8
```

2. 对象重新赋值减少
```Python
In [48]: n=456
In [49]: getrefcount(123)
Out[49]: 7
```

3. 对象从一个窗口对象中移除，或，窗口对象本身被销毁   
```Python
In [50]: a.remove(123)
In [51]: a
Out[51]: [1, 12]

In [52]: getrefcount(123)
Out[52]: 6
```
4. 一个本地引用离开了它的作用域，比如上面的foo(x)函数结束时，x指向的对象引用减1    

## 2. [垃圾回收](https://github.com/KissMyLady/Python/blob/master/Nont/py_height_del.md):
当Python中的对象越来越多，占据越来越大的内存，启动垃圾回收(garbage collection)，将没用的对象清除   

1. 原 理
#### 当Python的某个对象的引用计数降为0时，说明没有任何引用指向该对象，该对象就成为要被回收的垃圾   
比如某个新建对象，被分配给某个引用，对象的引用计数变为1。 如果引用被删除，对象的引用计数为0，那么该对象就可以被垃圾回收。
```Python
In [74]: a=[321,123]

In [75]: del a
```
2. 解析del  
del a后，已经没有任何引用指向之前建立的[321,123]，该表引用计数变为0，
用户不可能通过任何方式接触或者动用这个对象，当垃圾回收启动时，Python扫描到这个引用计数为0的对象，就将它所占据的内存

3、注 意
> 1、垃圾回收时，Python不能进行其它的任务，频繁的垃圾回收将大大降低Python的工作效率    
>      
> 2、Python只会在特定条件下，自动启动垃圾回收(垃圾对象少就没必要回收)      
>    
> 3、当Python运行时，会记录其中分配对象(object allocation)和取消分配对象(object deallocation)的次数。当两者的差值高于某个阈值时，垃圾回收才会启动     
```Python
In [93]: import gc

In [94]: gc.get_threshold()  # gc模块中查看阈值的方法
Out[94]: (700, 10, 10)
```
阈值分析:   

700即是垃圾回收启动的阈值   

每10次0代垃圾回收，会配合1次1代的垃圾回收；而每10次1代的垃圾回收，才会有1次的2代垃圾回收；   

当然也是可以手动启动垃圾回收：
```Python
In [95]: gc.collect()  # 手动启动垃圾回收
Out[95]: 2
```
4、何为分代回收
Python将所有的对象分为0，1，2三代   

所有的新建对象都是0代对象    

当某一代对象经历过垃圾回收，依然存活，就被归入下一代对象。    


## 3. 内存池机制: 
![ScreenShot-00346](https://github.com/KissMyLady/Python/blob/master/Img/Python/ScreenShot-00346.jpg)  
Python中有分为大内存和小内存: (256K为界限分大小内存)   
1、大内存使用malloc进行分配   

2、小内存使用内存池进行分配

3、Python的内存池(金字塔)
第3层: 最上层，用户对Python对象的直接操作   

第1层和第2层: 内存池，有Python的接口函数PyMem_Malloc实现-----若请求分配的内存在1~256字节之间就使用内存池管理系统进行分配，调用malloc函数分配内存   
但是每次只会分配一块大小为256K的大块内存，不会调用free函数释放内存，将该内存块留在内存池中以便下次使用。   

第0层: 大内存-----若请求分配的内存大于256K，malloc函数分配内存，free函数释放内存。  
第-1，-2层: 操作系统进行操作   


