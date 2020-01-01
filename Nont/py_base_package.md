常用Python标准库    
=====  
一点小想法:   
当初学Python的原因, 就是突然想学, 然后就学了, 然后自己买书, 自己看书, 上网下载Python...    
到现在的写教程式自学习, 中间多少还是有些坎坷, 没关系, 都到这一步了   
能把心静下来我就能学好任何想学的东西,  尽管编程很难, 但我有信心学好她, 用好她, 更好的融入她    

现在我们来谈谈新手大礼包, 也就是零基础学Python入门最常用的包      

## 新手大礼包:   
### 1. math   
[math方法实例讲解--引导知识来源CSDN](https://www.cnblogs.com/666gang/p/10952421.html)  
当初学编程,  什么都不懂, 一清二白, 觉得编程就是上帝, 特别是计算数字这方面很厉害,  以前就老是听说xxx用分布式主机, 算`派`的值, 然后精确到后面很多很多位   
于是我就想, 都是编程语言, Python那可定也是绝对没毛病的. 百度后, 发现有几种方法, 其中一种简单的:    
```python
import math
print(math.pi)
```
可以看到结果: `3.141592653589793`  
当初还是有点失望, 什么, 我堂堂Python加高配电脑就算这么点? 这不行   
于是又看到文章, 然后复制粘贴,  确实有算到后面很多位,  但是这个速度确实慢,  可能电脑渣吧.....  

于是, 深入学习后, 才发现语言分为解释型和编译型语言, Python就像公交车, 停下走下停下走下, 慢了许多  
有很多人专门就各个语言的速度进行了测试,  Python确实慢, 就计算和单纯的执行速度来说确实是这样的, 但Python更多的优点也是有的, 且看我的更新   

好了, 我们现在深入看看`import math`math有那些方法看看, 看个究竟  
打开我们的Pycharm, 点击查看math源码:  
```Python
from typing import Tuple, Iterable, Optional, SupportsFloat, SupportsInt
import sys

e = ...   # type: float
pi = ...  # type: float
if sys.version_info >= (3, 5):
    inf = ...  # type: float
    nan = ...  # type: float
if sys.version_info >= (3, 6):
    tau = ...  # type: float
def acos(x: SupportsFloat) -> float: ...
def acosh(x: SupportsFloat) -> float: ...
def asin(x: SupportsFloat) -> float: ...
def asinh(x: SupportsFloat) -> float: ...
def atan(x: SupportsFloat) -> float: ...
```
可以发现, 数学方法都在里面了, 数学运算能用上,  一般的编程常用的表达式就够了   
     


### 2. time  
[time使用方法](https://www.cnblogs.com/komean/p/10603518.html)
[time模块进阶使用方法](https://www.cnblogs.com/pal-duan/p/10568829.html)  
问题来了, 我怎么知道Python运行的慢还是快? 上面那个派计算的时候, 一定要拿一个秒表去卡么?   
还好, python中有一个很好用的time模块方法,  通过不同点时间执行,  然后取差, 就能够得知程序的运行时间了   
```Python
import time
start = time.time()  
	# Do something

end = time.time()
print(end- start)
```
那么, time很多功能, 可以做点什么呢?   
* 获取当前日期  
```Python
import time
print(time.strftime('%Y-%m-%d %H:%M:%S', time.localtime(time.time())))
```
`%Y-%m-%d %H:%M:%S`: 年-月-日 时-分-秒 格式   
`time.time()` : 当前时间戳  
`time.localtime()` : 格式化时间戳为本地的时间   

```Python
print(time.localtime(time.time()))
# time.struct_time(tm_year=2020, tm_mon=1,  tm_mday=1, 
#                    tm_hour=22, tm_min=21, tm_sec=14, 
#                    tm_wday=2,  tm_yday=1, tm_isdst=0)
```
```linux
%y 两位数的年份表示（00-99）
%Y 四位数的年份表示（000-9999）
%m 月份（01-12）
%d 月内中的一天（0-31）
%H 24小时制小时数（0-23）
%I 12小时制小时数（01-12） 
%M 分钟数（00=59）
%S 秒（00-59）

%a 本地简化星期名称
%A 本地完整星期名称
%b 本地简化的月份名称
%B 本地完整的月份名称
%c 本地相应的日期表示和时间表示
%j 年内的一天（001-366）
%p 本地A.M.或P.M.的等价符
%U 一年中的星期数（00-53）星期天为星期的开始
%w 星期（0-6），星期天为星期的开始
%W 一年中的星期数（00-53）星期一为星期的开始
%x 本地相应的日期表示
%X 本地相应的时间表示
%Z 当前时区的名称
%% %号本身
```
人脑是CPU, 重要的东西需要记住, 能很快借助工具查到的东西, 做好备份, 写好文档, 用的时候查得到就可以  
人脑记忆的特点, 重复, 重复再重复,  比如这个time包, 如果你不用, 你记它干嘛?  
我想女朋友的生日一定不会忘,  太重要了嘛, 不是吗   


### 3. Re正则表达式     
[菜鸟教程Re文档](https://www.runoob.com/python/python-reg-expressions.html)尽管Python版本不同, 但re规则是一样的      
[Re讲解--自文档](https://github.com/KissMyLady/WEB_Server/blob/master/Re/re.md)     
[Re表达式--自文档](https://github.com/KissMyLady/WEB_Server/blob/master/Re/re_text.md)    
有时候, 我们会碰到文字需要处理, 这非常的棘手, 一个个用鼠标+键盘去删, 也不是不可以, 但是当文件按M或者是G来计算时, 这显然不现实   
re模块就能非常方便的解决我们的问题     
我们来看一个简单匹配163邮箱的demo:      
```Python
import re
text = input("Please input Email address： \n"):
if re.match(r'[0-9a-zA-Z_]{0,19}@163.com',text):
  print('Email address is Right!')
else:
  print('Please reset your right Email address!')
```
匹配规则: `[0-9a-zA-Z_]{0,19}@163.com`   
1. `^` :匹配字符串的开始    
2. `[...]`	:匹配字符组中的字符   
3. `[0-9a-zA-Z_]` : 匹配0-9数字,a-z,A-Z小写大写英文和下划线  
4. `{0,19}`前面有`0-19`位长, 注意这里, 逗号之间不能有空格  
5. `@163.com`固定域名, 直接匹配  

匹配任意邮箱:  `r'^[0-9a-zA-Z_]{0,19}@[0-9a-zA-Z]{1,13}\.[com,cn,net]{1,3}$'`


### 4. Os模块     
打印文件夹方法:   
```Python  
files = os.listdir(Path)
print(files)
```
当运行这句代码后, 就会打印Path路径下的文件和文件夹列表  
还有一种经常用到的, 创造文件夹:    
```
def mkdir(path):
    folder = os.path.exists(path)
    if not folder:  # 不存在则创建为文件夹
        os.makedirs(path)  # 路径不存在会创建这个路径
        print('"OK"')
    else:
        print("There is this folder!")
```
小程序,  启动电脑程序(在cmd输入system也可直接启动):  
```Python
import os 
os.system("notepad")					# txt写字本
os.system("write")						# 写字板
os.system("mspaint") 					# 画板
os.system("msconfig") 					# 系统设置
os.system("shutdown -s -t 500")			# 预约注销 在500秒后
os.system("shutdown -a") 				# 取消注销计划
os.system("taskkill /f /im notepad.exe") #关闭程序
```

### 5. random模块  
有时候, 我们需要打乱下顺序, 或是list, dict等内建序列     
```Python
from random import shuffle

class Card(object):
    suits = ['1黑桃','2红心', '3钻石', '4方块']
    values = ['None', 'None', '2', '3','4','5','6','7','8','9','10',
              'J', 'Q','K', 'A']
    
    def __init__(self, v, s):
        self.value = v
        self.suit = s
    
    def __lt__(self, other):
        if self.value < other.value:
            return True
        if self.value == other.value:
            if self.suits < other.value:
                return True
            else:
                return False
        return False
     
    def __gt__(self, other):
        if self.value > other.value:
            return True
        if self.value == other.value:
            if self.suits > other.value:
                return True
            else:
                return False
        return False
    
    def __repr__(self):
        v = self.values[self.value]
        s = self.suits[self.suit]
        print_v = v +' - '+ s
        return print_v
    
    
class Deck(object):
    def __init__(self):
        self.cards = []
        for i in range(2, 15):
            for j in range(4):
                self.cards.append(Card(i, j))
        shuffle(self.cards)
```
请注意最后一行的: `shuffle(self.cards)`, Deck类创建了牌堆, 并打乱了顺序, 这就相当于我们洗牌, 和麻将一样  
你当然不希望牌的顺序是固定了,  游戏完的就是不确定性不是吗   
```Python
print( random.randint(1,10) )        # 产生 1 到 10 的一个整数型随机数  
print( random.random() )             # 产生 0 到 1 之间的随机浮点数
print( random.uniform(1.1,5.4) )     # 产生  1.1 到 5.4 之间的随机浮点数，区间可以不是整数
print( random.choice('tomorrow') )   # 从序列中随机选取一个元素
print( random.randrange(1,100,2) )   # 生成从1到100的间隔为2的随机整数
```


random还有很多实用的地方:  
例如说爬虫不能爬的太快, 请求时间间隔不能一模一样, 所以, 需要模仿用户,  模仿用户的随机性     
于是我们有:   
```Python
time.sleep(random.randint(2, 10))
```
前面的time模块就和random模块关联上了, 是不是很简单   


## 6. loggingr日志模块  
Python中有个logging模块可以完成相关信息的记录，在debug时用它往往事半功倍   	 
### 1. 日志级别
日志一共分成5个等级，从低到高分别是:     
> DEBUG: 详细的信息,通常只出现在诊断问题上
> INFO: 确认一切按预期运行
> WARNING: 一个迹象表明,一些意想不到的事情发生了,或表明一些问题在不久的将来(例如。磁盘空间低”)。这个软件还能按预期工作   
> ERROR: 更严重的问题,软件没能执行一些功能   
> CRITICAL: 一个严重的错误,这表明程序本身可能无法继续运行
这5个等级，也分别对应5种日志的方法： debug 、info 、warning 、error 、critical  
默认的是`WARNING`, 当在WARNING或之上时才被跟踪   
### 2. 日志输出
有两种方式记录跟踪:  
> 一种输出控制台，  
> 另一种是记录到文件中，如日志文件   

### 3. 将日志输出到控制台
比如`log1.py`如下：   
```Python
import logging  
logging.basicConfig(level=logging.WARNING,  
                    format='%(asctime)s - %(filename)s[line:%(lineno)d] - 
                    %(levelname)s: %(message)s')  

# 开始使用log功能
logging.info('这是 loggging info message')  
logging.debug('这是 loggging debug message')  
logging.warning('这是 loggging a warning message')  
logging.error('这是 an loggging error message')  
logging.critical('这是 loggging critical message')
```
```
2000-01-06 21:26:55,725 - log1.py[line:9]  - WARNING: 这是 loggging a warning message
2000-01-06 21:26:55,725 - log1.py[line:10] - ERROR: 这是 an loggging error message
2000-01-06 21:26:55,725 - log1.py[line:11] - CRITICAL: 这是 loggging critical message
```
说  明:     
通过logging.basicConfig函数对日志的输出格式及方式做相关配置，上面代码设置日志的输出等级是WARNING级别   
意思是WARNING级别以上的日志才会输出。 另外还制定了日志输出的格式   
  
注 意:   
只要用过一次log功能再次设置格式时将失效，实际开发中格式肯定不会经常变化，所以刚开始时需要设定好格式   


### 将日志输出到文件  
我们还可以将日志输出到文件，只需要在`logging.basicConfig`函数中设置好输出文件的文件名和写文件的模式    
`log2.py`:    
```Python
import logging  

logging.basicConfig(level=logging.WARNING,  
                    filename='./log.txt',  
                    filemode='w',  
                    format='%(asctime)s - %(filename)s[line:%(lineno)d] - 
                    %(levelname)s: %(message)s')  
# use logging  
logging.info(' 这是 loggging info message')  
logging.debug('这是 loggging debug message')  
logging.warning(' 这是 loggging a warning message')  
logging.error('   这是 an loggging error message')  
logging.critical('这是 loggging critical message')
```
```
python@ubuntu: cat log.txt 
2000-01-06 21:26:55,725 - log2.py[line:9]  - WARNING: 这是 loggging a warning message
2000-01-06 21:26:55,725 - log2.py[line:10] - ERROR: 这是 an loggging error message
2000-01-06 21:26:55,725 - log2.py[line:11] - CRITICAL: 这是 loggging critical message
```

### 既输出到控制台, 还要写入日志文件  
```Python
import logging  

# 第一步，创建一个logger  
logger = logging.getLogger()  
logger.setLevel(logging.INFO)  # Log等级总开关  

# 第二步，创建一个handler，用于写入日志文件  
logfile = './log.txt'  
fh = logging.FileHandler(logfile, mode='a')  # open的打开模式这里可以进行参考
fh.setLevel(logging.DEBUG)  # 输出到file的log等级的开关  

# 第三步，再创建一个handler，用于输出到控制台  
ch = logging.StreamHandler()  
ch.setLevel(logging.WARNING)   # 输出到console的log等级的开关  

# 第四步，定义handler的输出格式  
formatter = logging.Formatter("%(asctime)s - 
							   %(filename)s[line:%(lineno)d] - 
							   %(levelname)s: %(message)s")  
fh.setFormatter(formatter)  
ch.setFormatter(formatter)  

# 第五步，将logger添加到handler里面  
logger.addHandler(fh)  
logger.addHandler(ch)  

# 日志  
logger.debug(' 这是 logger debug message')  
logger.info('  这是 logger info message')  
logger.warning(' 这是 logger warning message')  
logger.error('   这是 logger error message')  
logger.critical('这是 logger critical message')
```
```
运行时终端的输出结果:
2000-01-06 21:26:55,725 - log3.py[line:9]  - WARNING: 这是 loggging a warning message
2000-01-06 21:26:55,725 - log3.py[line:10] - ERROR: 这是 an loggging error message
2000-01-06 21:26:55,725 - log3.py[line:11] - CRITICAL: 这是 loggging critical message

在log.txt中，有如下数据：
2000-01-06 21:26:55,725 - log3.py[line:9]  - WARNING: 这是 loggging a warning message
2000-01-06 21:26:55,725 - log3.py[line:10] - ERROR: 这是 an loggging error message
2000-01-06 21:26:55,725 - log3.py[line:11] - CRITICAL: 这是 loggging critical message
```

## 日志格式说明
logging.basicConfig函数中，可以指定日志的输出格式format，这个参数可以输出很多有用的信息，
如 下:
%(levelno)s:   打印日志级别的数值     
%(levelname)s: 打印日志级别名称     
%(pathname)s:  打印当前执行程序的路径，其实就是`sys.argv[0]`    
%(filename)s:  打印当前执行程序名     
%(funcName)s:  打印日志的当前函数     
%(lineno)d:  打印日志的当前行号     
%(asctime)s: 打印日志的时间       
%(thread)d:  打印线程ID           
%(threadName)s: 打印线程名称       
%(process)d: 打印进程ID     
%(message)s: 打印日志信息     
在工作中给的常用格式如下:   
```Python  
format= '%(asctime)s - %(filename)s[line:%(lineno)d] - %(levelname)s: %(message)s'      
```
这个格式可以输出日志的打印时间，是哪个模块输出的，输出的日志级别是什么，以及输入的日志内容       

[点击进入Python标准库一览](https://docs.python.org/zh-cn/3.7/library/index.html)   
