import导入模块     
=====   

## 问题来了, Python中有几种导入方式?    
```Python   
from xxx import yyy 
from xxx import *  
from import yyy, mmmm  

import ooo 
import xxx, ooo, vvv   
import requests as rq  # 避免重名, 简写  
import multiprocessing import Pool as P  
```

## import ooo作用   
1. 让解释器去加载ooo.py  
2. 在当前的模块定义一个变量aa, aa指向导入的模块  


## import路径  
python路径有很多坑点  
1. 在有些时候, 要导入模块, 但是导入报错, 基本上的原因就是因为路径不对  
2. 验证sys的路径  
![ScreenShot00010]()  
 
```Python
sys.path.append('/home/mylady/xxx')     # 添加到列表的最后面   
sys.path.insert(0, '/home/mylady/xxx')  # 可以确保先搜索这个路径  
```
```Python
sys.path.insert(0,"/home/python/xxxx")
sys.path

['/home/python/xxxx',
 '',
 '/usr/bin',
 '/usr/lib/python35.zip',
 '/usr/lib/python3.5',
 '/usr/lib/python3.5/plat-x86_64-linux-gnu',
 '/usr/lib/python3.5/lib-dynload',
 '/usr/local/lib/python3.5/dist-packages',
 '/usr/lib/python3/dist-packages',
 '/usr/lib/python3/dist-packages/IPython/extensions',
 '/home/python/.ipython']
```



## 重新导入模块  
在python中, import具有防止重复导入的功能(很实用)

> 模块被导入后，import module不能重新导入模块  
>> 重新导入需用reload(必须是全导入)      
```Python
from imp import reload
help(reload)
```
```Linux
Help on function reload in module imp:   

reload(module)
    **DEPRECATED**
    Reload the module and return it.
    The module must have been successfully imported before.
(END)
```




## 多模块开发时的注意点   
1. main函数在功能上往往只是调其他模块   
2, 通常没有具体的基础功能   

我们先看看下面的一段代码  
![ScreenShot00011-1](https://github.com/KissMyLady/Tools/blob/master/img/ScreenShot00011-1.jpg)  




