元类与ORM   
====

# 1. 类是对象--该找一个对象了        
我们先看一张图, 分别显示了Python3.8版本与3.6版本的细微区别:  

![ScreenShot-00289](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot-00289.jpg)  

`'AAA': <function __main__.AAA()>`  
之所以我们能用的全局变量, 它在哪里?  就在这里, 在特殊空间存着   

如果我们此时定义一个不可变类型int:   
![ScreenShot-00290](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot-00290.jpg)   
此时发现, a出现在了全局中  
数字`666`是对象, 变量名a就指向了这个对象   

#### 结论: 所有的东西都是对象    
 
此时我们定义一个什么都不做的函数OOO:    
![ScreenShot-00291](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot-00291.jpg)  
`'OOO': <function __main__.OOO(objecte)>`    

不管创建的什么, 就在里面创建一个key,对应名字, value对应创建的东西   

解释了: 为什么导入包, 只有先导入的生效  
这是字典, 字典key唯一   
所以, 名字不能相同   

### 结论: 谁指向这个对象?　类的名字　


小知识点: 在Ipython中, 有个对应的SQLite数据库(支持SQL, 不需要建立服务器, 直接操作文件), 存储了命令   

内嵌模块:  
为什么调用print, input, int等方法时, 在globals中没有?  
在globals中有一个默认加载模块:     
```Python
{
 '__builtin__': <module 'builtins' (built-in)> 
 '__builtins__': <module 'builtins' (built-in)>} 
```
globles作为字典, 我们是不是可以直接这样调用里面的对象?    
![ScreenShot-00292](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot-00292.jpg)   

如果我们加上括号, 是不是就是调用函数?  `xx['OOO']()`   

我们现在来看一看内建模块: `__builtin__`      
![ScreenShot-00293](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot-00293.jpg)     
# 'builtin'模块    
```Python
{'__name__': 'builtins',
 '__doc__': "Built-in functions, exceptions, and other objects.\n\nNoteworthy: None is the `nil' object; Ellipsis represents `...' in slices.",
 '__package__': '',
 '__loader__': _frozen_importlib.BuiltinImporter,
 '__spec__': ModuleSpec(name='builtins', loader=<class '_frozen_importlib.BuiltinImporter'>),
 '__build_class__': <function __build_class__>,
 '__import__': <function __import__>,
 'abs': <function abs(x, /)>,
 'all': <function all(iterable, /)>,
 'any': <function any(iterable, /)>,
 'ascii': <function ascii(obj, /)>,
 'bin': <function bin(number, /)>,
 'breakpoint': <function breakpoint>,
 'callable': <function callable(obj, /)>,
 'chr': <function chr(i, /)>,
 'compile': <function compile(source, filename, mode, flags=0, dont_inherit=False, optimize=-1, *, _feature_version=-1)>,
 'delattr': <function delattr(obj, name, /)>,
 'dir': <function dir>,
 'divmod': <function divmod(x, y, /)>,
 'eval': <function eval(source, globals=None, locals=None, /)>,
 'exec': <function exec(source, globals=None, locals=None, /)>,
 'format': <function format(value, format_spec='', /)>,
 'getattr': <function getattr>,
 'globals': <function globals()>,
 'hasattr': <function hasattr(obj, name, /)>,
 'hash': <function hash(obj, /)>,
 'hex': <function hex(number, /)>,
 'id': <function id(obj, /)>,
 'input': <function input(prompt=None, /)>,
 'isinstance': <function isinstance(obj, class_or_tuple, /)>,
 'issubclass': <function issubclass(cls, class_or_tuple, /)>,
 'iter': <function iter>,
 'len': <function len(obj, /)>,
 'locals': <function locals()>,
 'max': <function max>,
 'min': <function min>,
 'next': <function next>,
 'oct': <function oct(number, /)>,
 'ord': <function ord(c, /)>,
 'pow': <function pow(base, exp, mod=None)>,
 'print': <function print>,     # I'm here
 'repr': <function repr(obj, /)>,
 'round': <function round(number, ndigits=None)>,
 'setattr': <function setattr(obj, name, value, /)>,
 'sorted': <function sorted(iterable, /, *, key=None, reverse=False)>,
 'sum': <function sum(iterable, /, start=0)>,
 'vars': <function vars>,
 'None': None,
 'Ellipsis': Ellipsis,
 'NotImplemented': NotImplemented,
 'False': False,
 'True': True,
 'bool': bool,
 'memoryview': memoryview,
 'bytearray': bytearray,
 'bytes': bytes,
 'classmethod': classmethod,
 'complex': complex,
 'dict': dict,
 'enumerate': enumerate,
 'filter': filter,
 'float': float,
 'frozenset': frozenset,
 'property': property,
 'int': int,
 'list': list,
 'map': map,
 'object': object,
 'range': range,
 'reversed': reversed,
 'set': set,
 'slice': slice,
 'staticmethod': staticmethod,
 'str': str,
 'super': super,
 'tuple': tuple,
 'type': type,
 'zip': zip,
 '__debug__': True,
 'BaseException': BaseException,
 'Exception': Exception,
 'TypeError': TypeError,
 'StopAsyncIteration': StopAsyncIteration,
 'StopIteration': StopIteration,
 'GeneratorExit': GeneratorExit,
 'SystemExit': SystemExit,
 'KeyboardInterrupt': KeyboardInterrupt,
 'ImportError': ImportError,
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
 'Warning': Warning,
 'UserWarning': UserWarning,
 'DeprecationWarning': DeprecationWarning,
 'PendingDeprecationWarning': PendingDeprecationWarning,
 'SyntaxWarning': SyntaxWarning,
 'RuntimeWarning': RuntimeWarning,
 'FutureWarning': FutureWarning,
 'ImportWarning': ImportWarning,
 'UnicodeWarning': UnicodeWarning,
 'BytesWarning': BytesWarning,
 'ResourceWarning': ResourceWarning,
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
 'TimeoutError': TimeoutError,
 'open': <function io.open(file, mode='r', buffering=-1, encoding=None, errors=None, newline=None, closefd=True, opener=None)>,
 'copyright': Copyright (c) 2001-2019 Python Software Foundation.
 All Rights Reserved.
 
 Copyright (c) 2000 BeOpen.com.
 All Rights Reserved.
 
 Copyright (c) 1995-2001 Corporation for National Research Initiatives.
 All Rights Reserved.
 
 Copyright (c) 1991-1995 Stichting Mathematisch Centrum, Amsterdam.
 All Rights Reserved.,
 'credits':     Thanks to CWI, CNRI, BeOpen.com, Zope Corporation and a cast of thousands
     for supporting Python development.  See www.python.org for more information.,
 'license': Type license() to see the full license text,
 'help': Type help() for interactive help, or help(object) for help about object.,
 '__IPYTHON__': True,
 'display': <function IPython.core.display.display(*objs, include=None, exclude=None, metadata=None, transient=None, display_id=None, **kwargs)>,
 'get_ipython': <bound method InteractiveShell.get_ipython of <IPython.terminal.interactiveshell.TerminalInteractiveShell object at 0x7ff96faa6f70>>}
```
# 'builtins'模块   
```Python
{'__name__': 'builtins',
 '__doc__': "Built-in functions, exceptions, and other objects.\n\nNoteworthy: None is the `nil' object; Ellipsis represents `...' in slices.",
 '__package__': '',
 '__loader__': _frozen_importlib.BuiltinImporter,
 '__spec__': ModuleSpec(name='builtins', loader=<class '_frozen_importlib.BuiltinImporter'>),
 '__build_class__': <function __build_class__>,
 '__import__': <function __import__>,
 'abs': <function abs(x, /)>,
 'all': <function all(iterable, /)>,
 'any': <function any(iterable, /)>,
 'ascii': <function ascii(obj, /)>,
 'bin': <function bin(number, /)>,
 'breakpoint': <function breakpoint>,
 'callable': <function callable(obj, /)>,
 'chr': <function chr(i, /)>,
 'compile': <function compile(source, filename, mode, flags=0, dont_inherit=False, optimize=-1, *, _feature_version=-1)>,
 'delattr': <function delattr(obj, name, /)>,
 'dir': <function dir>,
 'divmod': <function divmod(x, y, /)>,
 'eval': <function eval(source, globals=None, locals=None, /)>,
 'exec': <function exec(source, globals=None, locals=None, /)>,
 'format': <function format(value, format_spec='', /)>,
 'getattr': <function getattr>,
 'globals': <function globals()>,
 'hasattr': <function hasattr(obj, name, /)>,
 'hash': <function hash(obj, /)>,
 'hex': <function hex(number, /)>,
 'id': <function id(obj, /)>,
 'input': <function input(prompt=None, /)>,
 'isinstance': <function isinstance(obj, class_or_tuple, /)>,
 'issubclass': <function issubclass(cls, class_or_tuple, /)>,
 'iter': <function iter>,
 'len': <function len(obj, /)>,
 'locals': <function locals()>,
 'max': <function max>,
 'min': <function min>,
 'next': <function next>,
 'oct': <function oct(number, /)>,
 'ord': <function ord(c, /)>,
 'pow': <function pow(base, exp, mod=None)>,
 'print': <function print>,      # I'm here
 'repr': <function repr(obj, /)>,
 'round': <function round(number, ndigits=None)>,
 'setattr': <function setattr(obj, name, value, /)>,
 'sorted': <function sorted(iterable, /, *, key=None, reverse=False)>,
 'sum': <function sum(iterable, /, start=0)>,
 'vars': <function vars>,
 'None': None,
 'Ellipsis': Ellipsis,
 'NotImplemented': NotImplemented,
 'False': False,
 'True': True,
 'bool': bool,
 'memoryview': memoryview,
 'bytearray': bytearray,
 'bytes': bytes,
 'classmethod': classmethod,
 'complex': complex,
 'dict': dict,
 'enumerate': enumerate,
 'filter': filter,
 'float': float,
 'frozenset': frozenset,
 'property': property,
 'int': int,
 'list': list,
 'map': map,
 'object': object,
 'range': range,
 'reversed': reversed,
 'set': set,
 'slice': slice,
 'staticmethod': staticmethod,
 'str': str,
 'super': super,
 'tuple': tuple,
 'type': type,
 'zip': zip,
 '__debug__': True,
 'BaseException': BaseException,
 'Exception': Exception,
 'TypeError': TypeError,
 'StopAsyncIteration': StopAsyncIteration,
 'StopIteration': StopIteration,
 'GeneratorExit': GeneratorExit,
 'SystemExit': SystemExit,
 'KeyboardInterrupt': KeyboardInterrupt,
 'ImportError': ImportError,
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
 'Warning': Warning,
 'UserWarning': UserWarning,
 'DeprecationWarning': DeprecationWarning,
 'PendingDeprecationWarning': PendingDeprecationWarning,
 'SyntaxWarning': SyntaxWarning,
 'RuntimeWarning': RuntimeWarning,
 'FutureWarning': FutureWarning,
 'ImportWarning': ImportWarning,
 'UnicodeWarning': UnicodeWarning,
 'BytesWarning': BytesWarning,
 'ResourceWarning': ResourceWarning,
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
 'TimeoutError': TimeoutError,
 'open': <function io.open(file, mode='r', buffering=-1, encoding=None, errors=None, newline=None, closefd=True, opener=None)>,
 'copyright': Copyright (c) 2001-2019 Python Software Foundation.
 All Rights Reserved.
 
 Copyright (c) 2000 BeOpen.com.
 All Rights Reserved.
 
 Copyright (c) 1995-2001 Corporation for National Research Initiatives.
 All Rights Reserved.
 
 Copyright (c) 1991-1995 Stichting Mathematisch Centrum, Amsterdam.
 All Rights Reserved.,
 'credits':     Thanks to CWI, CNRI, BeOpen.com, Zope Corporation and a cast of thousands
     for supporting Python development.  See www.python.org for more information.,
 'license': Type license() to see the full license text,
 'help': Type help() for interactive help, or help(object) for help about object.,
 '__IPYTHON__': True,
 'display': <function IPython.core.display.display(*objs, include=None, exclude=None, metadata=None, transient=None, display_id=None, **kwargs)>,
 'get_ipython': <bound method InteractiveShell.get_ipython of <IPython.terminal.interactiveshell.TerminalInteractiveShell object at 0x7ff96faa6f70>>}
```
在python3.8.1中, 带s和不带s的都有, 这里都放出来了    


python如何用名字调包的?   
#### 结论: 先在`globals()`中找, 如果没有就去`__builtin__`找, 找不到就砰的报错   


![ScreenShot-00294](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot-00294.jpg)   


# 类的功能: 就是用来创建实例对象的   
元类: 特殊的类, 用来创建类    
类:  拥有创建实例对象的功能   

关系划分:    
> ... → 元类 → 元类 → 类 → 实例对象  
Python顶层的造物主: 元类   


我们先看一段代码:  
```Python
def choose_class(name):
	if name == 'foo':
		class Foo(object):
			pass
		return Foo 
	else:
		class Bar(object):
			pass
		return Bar

MyClass = choose_class('foo')

print(MyClass)  # 函数返回的是类，不是类的实例
<class '__main__'.Foo>

print(MyClass())  # 你可以通过这个类创建类实例，也就是对象
<__main__.Foo object at 0x89c6d4c>
```
我们这样就可以动态的创建一个类, 但是这么做很low   

升级方案: Type   

Tpye在python中主要拿来用来测试对象属性, 但是它还可以动态的创建一个类  
在开发中, 一个函数就该有一个特定功能, 根据传入的参数不同导致功能不一样, 这样是在玩火   

但Python很久前为了兼容以后版本, 保留了它    

# Type创建一个类: 

![ScreenShot-00295](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot-00295.jpg)  
```
Help on class T_T in module __main__:

class T_T(builtins.object)
 |  Data descriptors defined here:
 |  
 |  __dict__
 |      dictionary for instance variables (if defined)
 |  
 |  __weakref__
 |      list of weak references to the object (if defined)
 |  
 |  ----------------------------------------------------------------------
 |  Data and other attributes defined here:
 |  
 |  a = 100
 |  
 |  b = 5
```
我们查看tt是什么情况:　　
```
Help on class T_TQ in module __main__:

class T_TQ(builtins.object)
 |  Data descriptors defined here:
 |  
 |  __dict__
 |      dictionary for instance variables (if defined)
 |  
 |  __weakref__
 |      list of weak references to the object (if defined)
 |  
 |  ----------------------------------------------------------------------
 |  Data and other attributes defined here:
 |  
 |  a = 100
 |  
 |  b = 5

```
可以发现, 两者一模一样　　  
help(type)   
```
Help on class type in module builtins:

class type(object)
 |  type(object_or_name, bases, dict)
 |  type(object) -> the object's type
 |  type(name, bases, dict) -> a new type
 |  
 |  Methods defined here:
 |  
 |  __call__(self, /, *args, **kwargs)
 |      Call self as a function.
 |  
 |  __delattr__(self, name, /)
 |      Implement delattr(self, name).
 |  
 |  __dir__(self, /)
 |      Specialized __dir__ implementation for types.
 |  
 |  __getattribute__(self, name, /)
 |      Return getattr(self, name).
 |  
 |  __init__(self, /, *args, **kwargs)
 |      Initialize self.  See help(type(self)) for accurate signature.
 |  
 |  __instancecheck__(self, instance, /)
 |      Check if an object is an instance.
 |  
 |  __repr__(self, /)
 |      Return repr(self).
 |  
 |  __setattr__(self, name, value, /)
 |      Implement setattr(self, name, value).
 |  
 |  __sizeof__(self, /)
 |      Return memory consumption of the type object.
 |  
 |  __subclasscheck__(self, subclass, /)
 |      Check if a class is a subclass.
 |  
 |  __subclasses__(self, /)
 |      Return a list of immediate subclasses.
 |  
:
```
真正的type并不是一个函数, 而是一个类, 根据传递的参数不一样,  实现的功能不一样   
这个类有特殊功能, 它返回的功能, 具有创建实例对象的功能   

所以我们在上面创建的`tt = type('T_TQ', (), {'a':100, 'b':5})`它就是一个元类  
返回值就是我们说的类, 即动态的创建类   


# 元类中的继承与方法       
继承:    
`A = type('T_TQ', (farther, ), {'a':100, 'b':5})`   

实例方法:    
```
def demo(self):
    print('This is test')

B = type('T_TQ', (farther, ), {'demo':demo})`    
```
所有的方法, 都是创建了一个名字当做key, 然后value指向实例方法   

类方法:  
[classmethod类方法跟staticmethod静态方法](https://blog.csdn.net/ljt735029684/article/details/80714274)     	

1.使用@staticmethod目的之一是为了增加可读性，不需要参数self的方法都可以加上@staticmethod增加可读性，    
因为，这个方法是类级别的，在调用时要使用类名。    

2.使用@classmethod是为了处理一些__init__处理不了的赋值问题（一般是参数不对应）,    
可以当成，有第二，第三个__init__方法，当然它要通过类名显示调用   

```Python 
@classmethod  
def test4():
    print('This is class method')

ttt = tyoe('Test4', (), {'test4':test4})
```

静态方法:  
```Python 
@staticmethod 
def test5():
    print('This is class staticmethod')

ttt = tyoe('Test5', (), {'test5':test5})
```


# 元类产生元类   
我们先看一段代码:
xx.__class__可以告诉我们创建的对象是谁   
```
class TT(object):
	pass

tt = TT()
tt.__class__
>>> __main__.TT
```

我们现在看看tt是谁创建的:  
![ScreenShot-00296](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot-00296.jpg)   

#### 结论: 元类创建类   


# 元类创建实例讲解   
先看一段代码:   
```Python
#-*- coding:utf-8 -*-
def upper_attr(class_name, class_parents, class_attr):
    new_attr = {}
    for name,value in class_attr.items():
        if not name.startswith("__"):
            new_attr[name.upper()] = value

    return type(class_name, class_parents, new_attr)

class Foo(object, metaclass=upper_attr):
    bar = 'bip'

print(hasattr(Foo, 'bar'))
print(hasattr(Foo, 'BAR'))

f = Foo()
print(f.BAR)
```
通过这个返回type, 我们将类方法中的所有小写转换成了大写   

其中的对应关系:      
class_name == Foo   
class_parents == object   
class_attr == upper_attr   

我们type中的字典{}, 然后将key转成大写即可, 最后返回type, 类只能是type创建的      


所以说, 在代码中定义class只是表面现象, 实质是type创建的     
 

# 元类装饰器   
在函数中, 我们可以写装饰器, 在不修改函数的前提下添加额外的增强功能  
像这样通用装饰器:   
```Python
def one(function_output):
    def two(*args, **kwargs):
        print!("This is function");
        return function_output(*args, **kwargs)
    return two(*args, **kwargs)

@one
def demo():
	print('This is demo function') 
```

或是这样的装饰器--带参数装饰器:    
```Python  
def one(date):
    def two(function_output):
        def three
            print('This is a date')
            return function_output
        return three
    return two(*args, **kwargs)
```
```Python 
@one('This is my decorator')
def Mylady():
    print('Kiss My Lady')
```

在python3中, 指定用谁创建用`class Foo(object, metaclass=upper_attr):`   
使用`metaclass=upper_attr`指定   


```Python
class UpperAttrMetaClass(type):
    def __new__(cls, class_name, class_parents, class_attr):
        new_attr = {}
        for name, value in class_attr.items():
            if not name.startswith("__"):
                new_attr[name.upper()] = value
        return type(class_name, class_parents, new_attr)

class Foo(object, metaclass=UpperAttrMetaClass):
    bar = 'bip'

print(hasattr(Foo, 'bar'))
print(hasattr(Foo, 'BAR'))

f = Foo()
print(f.BAR)
```
说明:    
1. __new__ 是在__init__之前被调用的特殊方法    
2. __new__是用来创建对象并返回之的方法    
3. 而__init__只是用来将传入的参数初始化给对象    
4. 你很少用到__new__，除非你希望能够控制对象的创建    
5. 这里，创建的对象是类，我们希望能够自定义它，所以我们这里改写__new__    
6. 如果你希望的话，你也可以在__init__中做些事情    
7. 还有一些高级的用法会涉及到改写__call__特殊方法，但是我们这里不用    

第二种方法说明:      
1. 方法2：复用type.__new__方法        
2. 这就是基本的OOP编程，没什么魔法    
3. return type.__new__(cls, class_name, class_parents, new_attr)    


就是这样，除此之外，关于元类真的没有别的可说的了。但就元类本身而言，它们其实是很简单的：   

1. 拦截类的创建
2. 修改类
3. 返回修改之后的类
4. 究竟为什么要使用元类？

现在回到我们的大主题上来，究竟是为什么你会去使用这样一种容易出错且晦涩的特性？好吧，一般来说，你根本就用不上它：

> “元类就是深度的魔法，99%的用户应该根本不必为此操心。如果你想搞清楚究竟是否需要用到元类，那么你就不需要它。
> 那些实际用到元类的人都非常清楚地知道他们需要做什么，而且根本不需要解释为什么要用元类。” 
> —— Python界的领袖 Tim Peters



