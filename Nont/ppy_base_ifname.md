[Python中的__name__=="__main__"](https://blog.csdn.net/yjk13703623757/article/details/77918633)  
======

结 论: 
#### 当`.py`文件被直接运行时，`if __name__ == '__main__'`之下的代码块将被运行     
#### 当`.py`文件以模块形式被导入时，`if __name__ == '__main__'`之下的代码块不被运行       



解释:  
`__name__ == '__main__'`:   
假如你叫小明`.py`(当前执行py文件)，在朋友眼中(模块导入)，你是小明(`__name__ == '小明'`)   

在你自己眼中(直接执行)，你是你自己(`__name__ == '__main__'`)   
 
其他解释:   
像演讲稿: 各位领导, 各位首长, 下面开始我的表演...     


# 1. 作为程序入口  
比如C, `C++`, 以及完全面向对象的编程语言Java，`C#`等, 程序都必须要有一个入口   
如果你接触过这些语言，对于程序入口这个概念应该很好理解, C, C++都需要有一个main函数作为程序的入口    
也就是程序的运行会从main函数开始   

同样, Java, `C#`必须要有一个包含Main方法的主类，作为程序入口      

而Python则不同，它属于脚本语言，不像编译型语言那样先将程序编译成二进制再运行，而是动态的逐行解释运行    
#### 从脚本第一行开始运行，没有统一的入口   

一个Python源码文件`.py`除了可以被直接运行外，还可以作为模块(也就是库), 被其他`.py`文件导入   
不管是直接运行还是被导入，`.py`文件的最顶层代码都会被运行, Python用缩进来区分代码层次      
而当一个`.py`文件作为模块被导入时，我们可能不希望一部分代码被运行, 使用`if __name__ == '__main__'`在别处调用此包时, if下面的代码就不会执行  


# 2. __name__     
## 2.1 __name__反映一个包的结构    
__name__是内置变量，可用于反映一个包的结构     
我们现在有一个包a，包的结构如下:      
![ScreenShot-00297](https://github.com/KissMyLady/Python/blob/master/Img/1_13/ScreenShot-00297.jpg)  
在包a中，文件`c.py`,   `__init__.py`,  `__init__.py`的内容都为: `print(__name__)`  

当一个.py文件（模块）被其他.py文件（模块）导入时，我们在命令行执行  
`python -c "import a.b.c"`   
![ScreenShot-00298](https://github.com/KissMyLady/Python/blob/master/Img/1_13/ScreenShot-00298.jpg)   
由此可见，__name__可以清晰地反映一个模块在包中的层次    


## 2.2 `__name__`表示当前模块的名字   
__name__是内置变量，可用于表示当前模块的名字   
我们直接运行一个`.py`文件(模块)   
![ScreenShot-00299](https://github.com/KissMyLady/Python/blob/master/Img/1_13/ScreenShot-00299.jpg)  
可以看到, 输出了`__main__`   

结论: 如果一个.py文件(模块)被直接运行时, 则它没有包结构, 它`__name__`值为`__main__` 即模块名为`__main__`   

所以, `if __name__ == '__main__'`的意思是: 当`.py`文件被直接运行时, if __name__ == '__main__'`之下的代码块将被运行   
当`.py`文件以模块形式被导入时，if __name__ == '__main__'之下的代码块不被运行   



# 3. `__main__.py`文件与`python -m`  
`__main__.py`文件相当于是一个包的`入口程序`     
Python 的-m 用于将一个模块或者包作为一个脚本运行   

## 3.1 运行Python程序的两种方式     
* 1. python xxx.py, 直接运行xxx.py文件  
* 2. python -m xxx.py, 把xxx.py当做模块运行   

1. 现在我们有一个文件run.py，内容如下:  
```Python
import sys
print(sys.path)
```
我们直接启动它:   
![ScreenShot-00300](https://github.com/KissMyLady/Python/blob/master/Img/1_13/ScreenShot-00300.jpg)  

2. 然后以模块的方式运行:  
`python -m run.py`    
![ScreenShot-00301](https://github.com/KissMyLady/Python/blob/master/Img/1_13/ScreenShot-00301.jpg)   
> Error while finding module specification for 'run.py' 
> (ModuleNotFoundError: __path__ attribute not found on 'run' while trying to find 'run.py')

差异:  
#### 1. 直接运行方式是把`run.py`文件所在的目录放到了`sys.path`属性中   
#### 2. 模块方式运行是把输入命令的目录(也就是当前工作路径), 放到了`sys.path`属性中 

以模块方式运行还有一个不同的地方: 多出了一行`No module named run.py`的错误   

实际上以模块方式运行时，Python先对`run.py`执行一遍 import，所以print(sys.path)被成功执行，
然后Python才尝试运行run.py模块，但是在path变量中并没有run.py这个模块，所以报错   
正确的运行方式，应该是`python -m run`
![ScreenShot-00302](https://github.com/KissMyLady/Python/blob/master/Img/1_13/ScreenShot-00302.jpg)   

## 3.2 `__main__.py`的作用  
我们现在一个包Package:  
![ScreenShot-00303](https://github.com/KissMyLady/Python/blob/master/Img/1_13/ScreenShot-00303.jpg)   
1. `__init__`内容:  
```Python
import sys

print("__init__")
print(sys.path)
```
2. `__main__`内容:  
```Python
import sys

print("__main__")
print(sys.path)
```
1. `python package`运行
![ScreenShot-00305](https://github.com/KissMyLady/Python/blob/master/Img/1_13/ScreenShot-00305.jpg)  

2. `python -m package`运行:      
![ScreenShot-00304](https://github.com/KissMyLady/Python/blob/master/Img/1_13/ScreenShot-00304.jpg)  

结论:   
#### 1. 当加上-m时，Python会把当前工作目录添加到`sys.path`中, 而不加-m时，Python则会把脚本所在目录添加到`sys.path`中    
   
#### 2. 当加上-m时，Python会先将模块或者包导入，然后再执行      

### 3. 1__main__.py1文件是一个包或者目录的入口程序, 不管是用python package还是用python -m package运行, 1__main__.py1文件总是被执行      
   	
