Python中异常捕获问题    
====

# 被动抛出异常   
我们先看一个简单demo:  
```Python
try:
    num = int(input("输入整数："))
    result = 8 / num
    
except ValueError:
    print("输入整数")
    
except Exception as result:
    print("未知错误 %s" % result)
    
else:
    print("成功")
    
finally:
    print("都会执行")

```
输出内容:   
``` 
输入整数：0
未知错误 division by zero
都会执行
```
可以看到, 我们使用了`except Exception as result:`捕获了异常  

#### 如果用try, except也可以, 但是会使程序的BUG隐藏的很深, 实际上, 也就是这里的BUG最多所以我们选择使用简单的方法包起来, 能跑起来再说  
程序员都比较懒    

像`except Exception as result:`这种的错误类型还有很多:   
如果不知道的话, 可以在打印`gobals()`然后查看Python内建模块     
```Python
 {'ImportError': ImportError,
 'ModuleNotFoundError': ModuleNotFoundError,
 'OSError': OSError,
 'EnvironmentError': OSError,
 'IOError': OSError,
 'EOFError': EOFError,
 'RuntimeError': RuntimeError,
 'RecursionError': RecursionError,
 'NotImplementedError': NotImplementedError,
 'NameError': NameError,
 'UnboundLocalError': UnboundLocalError,
 'AttributeError': AttributeError,
 'SyntaxError': SyntaxError,
 'IndentationError': IndentationError,
 'TabError': TabError,
 'LookupError': LookupError,
 'IndexError': IndexError,
 'KeyError': KeyError,
 'ValueError': ValueError,
 'UnicodeError': UnicodeError,
 'UnicodeEncodeError': UnicodeEncodeError,
 'UnicodeDecodeError': UnicodeDecodeError,
 'UnicodeTranslateError': UnicodeTranslateError,
 'AssertionError': AssertionError,
 'ArithmeticError': ArithmeticError,
 'FloatingPointError': FloatingPointError,
 'OverflowError': OverflowError,
 'ZeroDivisionError': ZeroDivisionError,
 'SystemError': SystemError,
 'ReferenceError': ReferenceError,
 'MemoryError': MemoryError,
 'BufferError': BufferError,
 'ConnectionError': ConnectionError,
 'BlockingIOError': BlockingIOError,
 'BrokenPipeError': BrokenPipeError,
 'ChildProcessError': ChildProcessError,
 'ConnectionAbortedError': ConnectionAbortedError,
 'ConnectionRefusedError': ConnectionRefusedError,
 'ConnectionResetError': ConnectionResetError,
 'FileExistsError': FileExistsError,
 'FileNotFoundError': FileNotFoundError,
 'IsADirectoryError': IsADirectoryError,
 'NotADirectoryError': NotADirectoryError,
 'InterruptedError': InterruptedError,
 'PermissionError': PermissionError,
 'ProcessLookupError': ProcessLookupError,
 'TimeoutError': TimeoutError,}
```


# 主动抛出异常   
一个简单demo:   
```Python
def input_password():
    pwd = input("请输入密码：")
    if len(pwd) >= 8:
        return pwd

    print("主动抛出异常")
    # 1> 创建异常对象 - 可以使用错误信息字符串作为参数
    ex = Exception("密码长度不够")

    # 2> 主动抛出异常
    raise ex

# 提示用户输入密码
try:
    print(input_password())
except Exception as result:
    print(result)
```
输出内容:   
```
请输入密码：0
主动抛出异常
密码长度不够
```
这种方法用的不多    
