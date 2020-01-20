with与“上下文管理器”      
======
如果你有阅读源码的习惯，可能会看到一些优秀的代码经常出现带有 “with” 关键字的语句，它通常用在什么场景呢？       
今对于系统资源如文件、数据库连接、socket 而言，应用程序打开这些资源并执行完业务逻辑之后，必须做的一件事就是要关闭（断开）该资源      
    
比如 Python 程序打开一个文件，往文件中写内容，写完之后，就要关闭该文件，否则会出现什么情况呢？      
极端情况下会出现 "Too many open files" 的错误，因为系统允许你打开的最大文件数量是有限的。      

同样，对于数据库，如果连接数过多而没有及时关闭的话       
就可能会出现 "Can not connect to MySQL server Too many connections"      
因为数据库连接是一种非常昂贵的资源，不可能无限制的被创建。    

我们 来看看如何正确关闭一个文件。    

常规版:  
```Python
def common():
    f = open("output.txt", "w")
    f.write("python之禅")
    f.close()
```
那么问题来了, 如果`f.write("python之禅")`这句话出现了异常, 会怎么样?    
close会一直被占用,  就不能通过其他方式打开了  

如何改进改进下?  

升级版:  
```Python
def lv_common():
    f = open("output.txt", "w")
    try:
        f.write("python之禅")
    except IOError:
        print("oops error")
    finally:
        f.close()
```
只要把 close放在 finally代码中，文件就一定会关闭   

高级版:  
```Python
def high_level():
    with open("output.txt", "r") as f:
        f.write("Python之禅")
```
一种更加简洁、优雅的方式就是用 with关键字         
open方法的返回值赋值给变量 f，当离开 with代码块的时候，系统会自动调用f.close()方法         
with的作用和使用 `try/finally`语句是一样的       

那么它的实现原理是什么？   
要涉及到另外一个概念，就是上下文管理器(Context Manager)     


## 上下文管理器  
任何实现了 `__enter__()` 和 `__exit__()`方法的对象都可称之为上下文管理器,  上下文管理器对象可以使用 with关键字   
显然，文件(file)对象也实现了上下文管理器    

那么文件对象是如何实现这两个方法的呢？   
我们可以模拟实现一个自己的文件类，让该类实现 __enter__()和 __exit__() 方法   
```Python
class File():
    def __init__(self, filename, mode):
        self.filename = filename
        self.mode = mode

    def __enter__(self):
        print("entering")
        self.f = open(self.filename, self.mode)
        return self.f

    def __exit__(self, *args):
        print("will exit")
        self.f.close()
```
__enter__()方法返回资源对象，这里就是你将要打开的那个文件对象，__exit__() 方法处理一些清除工作     

因为 File 类实现了上下文管理器，现在就可以使用 with 语句了:     
```Python  
with File('out.txt', 'w') as f:
    print("writing")
    f.write('hello, python')
```
这样，你就无需显示地调用 close方法了, 由系统自动去调用，哪怕中间遇到异常 close方法也会被调用       



### 实现上下文管理器的另外方式
Python 还提供了一个 contextmanager 的装饰器，更进一步简化了上下文管理器的实现方式     
通过 yield 将函数分割成两部分，yield 之前的语句在 __enter__ 方法中执行，yield 之后的语句在 __exit__ 方法中执行   
紧跟在 yield 后面的值是函数的返回值     
```Python
from contextlib import contextmanager

@contextmanager
def my_open(path, mode):
    f = open(path, mode)
    yield f
    f.close()
```
调 用:    
```Python
with my_open('out.txt', 'w') as f:
    f.write("hello , the simplest context manager")
```
小  结:   
Python 提供了 with语法用于简化资源操作的后续清除操作  
* 是 try/finally 的替代方法   
* 实现原理建立在上下文管理器之上    
* 此外，Python 还提供了一个 contextmanager装饰器更进一步简化上下管理器的实现方式     

# [菜鸟教程-文件读取方法](https://www.runoob.com/python/file-methods.html)  
