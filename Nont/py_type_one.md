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


