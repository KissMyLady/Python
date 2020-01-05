生成器--迭代器     
====

## 生成器   
形如这样的就是生成器:  
```Python
x = (a for a in range(3))   
```
打印结果:   
```Python
print(x)			# <generator object <genexpr> at 0x03AFCE60>	
print(x.__next__()) # 0
print(x.__next__()) # 1
print(x.__next__()) # 2
print(x.__next__()) # error
```
![ScreenShot-00258](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot-00258.jpg)  
请注意: 使用`next()`方法也是一样的效果  
如果使用for循环:  
![ScreenShot-00259](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot-00259.jpg)   
基本上从来不会用`x.__next__()`方法, 用`for`   


我们再看一种生成器:    
```Python
def fib(max):
	n, a, b =0, 0, 1
	while n < max:
		yield b
		a, b = b, a +b
		n += 1
		
fb = fib(10)
for i in fb:
	print(i)
```
它将分别打印数列的前10项   
此时的`fb`, 就是一个`生成器`: `<generator object fib at 0x0577CE98>`   


### 说明:   
1. 每调用一次生成器, 都会暂停一次, 需要`x.__next__()`或`send()`方法恢复   
2. 生成器每次产生一个值, 这就是它优点: 占用内存数非常小   
3. 函数里只要有`yield`, 它就变成了`生成器`   
  


## 迭代器      
迭代器满足条件:  
1. 有`__iter__`方法  
2, 在1的基础上, 有`__next__`方法  

迭代器测试:  
![ScreenShot-00260](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot-00260.jpg)  
1. list, dict, str是Iterable(对象), 但不是Itertor(器)                  
2. Iterable变成Itertor, 使用iter()函数:     
> isinstance(iter([]), Iterator)  `True`  


### `for`循环的本质:     
```Python
for i in [1, 2, 3]:
	pass
```
完全等价于:   
```Python
iterator = iter([1, 2, 3])
while True:
	try:
		a = next(iterator)
	except StopIteration:
		break
```
可以看到, for循环就是不断调用next实现的   



## 知识引导:  
1. 迭代是访问集合元素的一种方式   
2. 迭代器是一个可以记住遍历的位置的对象(指针)        
3. 迭代器对象从集合的第一个元素开始访问，直到所有的元素被访问完结束(遍历)     
4. 迭代器只能往前不会后退(顺序)      
[优秀文章-python生成器和迭代器](https://www.cnblogs.com/wj-1314/p/8490822.html)  

## 1. 可迭代对象     
我们已经知道可以对`list、 tuple、 str`等类型的数据使用`for  in  `的循环语法从其中依次拿到数据进行使用        
#### 我们把这样的过程称为`遍历`，也叫`迭代`            

## 2. 如何判断一个对象是否可以迭代     
Python3.8以前版本     
```Python 
from collections import Iterable
	
isinstance([], Iterable)
isinstance({}, Iterable)
isinstance('abc', Iterable) 
isinstance(mylist, Iterable)
isinstance(100, Iterable)
```
#### Python3.8以后版本   
```Python
from collections.abc import Iterable
	
isinstance([], Iterable)
isinstance({}, Iterable)
isinstance('abc', Iterable) 
isinstance(mylist, Iterable)
isinstance(100, Iterable)
```
如果为True, 则为可迭代对象   

## 2. 如何判断一个对象是否是迭代器   
```Python 
from collections import Iterator	
isinstance([], Iterable)        # False
isinstance(iter([]), Iterable)  # True  
```



### 迭代器的应用
1. 第一种应用: [并发](https://blog.csdn.net/qq_43273590/article/details/84937907):  


2. 第二种应用:  
有一个文件 大概有500G，并且只有一行，行之间有分隔符，我们需要把文件内的数据一行一行的读取出来然后写入数据库里面     

有的小伙伴就报名说了，我们取行可以用open，然后用for循环   

看我的
```Python    
with open（'500G.txt'）as f:
     for i in f.readlines():
        print i 
```
由于它只有一行，这样读取会把所有数据读取出来，500G内存谁也承受不了, 这是没有办法做到的   
注意, 行之间有分隔符  

首先解释一个函数 file.read()
1. 这个read函数并不是一次读取所有，可以传入int参数, 代表读取的字符数   
2. 连续调用, 可以读取偏移量的值    
有了这个我们的问题就迎刃而解, 例子如下：
```Python   
file_phth="C:/500G.txt"

with open(file_phth, "r") as f:
    a = f.read(20)
    b = f.read(20)
    print(a, b)
```
如果有这个函数, 我们就可以做到读取大数据:   
```Python   
file_phth="C:/500G.txt"

def The_read(f, newline):
    NEW_STR = ""     
    while True:	
    	while newline in NEW_STR:
            pos =  NEW_STR.index(newline) 
            yield  NEW_STR[:pos]         
            NEW_STR = NEW_STR[pos + len(newline):]

        chunk = f.read(200)

        if not chunk:  
            yield NEW_STR 
            break    

        NEW_STR = NEW_STR + chunk  

with open(file_phth,"r") as f:
    for i in The_read(f, newline="{|}"):
        print(i)
```
其中while循环是指取到的200字符里最后一个分隔符后边的值加上再次取到的chunk值不停的遍历直到把所有的分隔符前面的值取完毕   

if 语句的用意是：
当chunk取不到值，也就是文件内容的边界了，要结束循环，并把最后一个分隔符后边的值再次yield   

最后一个for循环 遍历生成器的值，取到的值直接可以插入数据库   

切入点: 遇到超大文件，不能直接放在内存中，要分段进行读取 以减少内存的占用


