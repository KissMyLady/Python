Python的垃圾回收机制: `__del__`     
========

创建对象后，python解释器默认调用__init__()方法    
当删除一个对象时，python解释器也会默认调用一个方法, 这个方法为__del__()方法   

在python中，对于开发者来说很少会直接销毁对象(如果需要，应该使用del关键字销毁)  
Python的内存管理机制能够很好的胜任这份工作。

#### 结论: 不管是手动调用del还是由python自动回收, 都会触发__del__方法执行     

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





[Python的垃圾回收机制: 原理](https://www.jianshu.com/p/1e375fb40506)     
========
现在的高级语言如java，c#等，都采用了垃圾收集机制，而不再是c，c++里用户自己管理维护内存的方式。自己管理内存极其自由，可以任意申请内存，但如同一把双刃剑，为大量内存泄露，悬空指针等bug埋下隐患。    

对于一个字符串、列表、类甚至数值都是对象，且定位简单易用的语言，自然不会让用户去处理如何分配回收内存的问题。   
Python里也同java一样采用了垃圾收集机制，不过不一样的是:  
#### Python采用的是`引用计数机制`为主，`标记-清除`和`分代收集`两种机制为辅的策略    

## 1. 引用计数机制：
python里每一个东西都是对象，它们的核心就是一个结构体: `PyObject`   
```Python
 typedef struct_object {
 int ob_refcnt;
 struct_typeobject *ob_type;
} PyObject;
```
PyObject是每个对象必有的内容，其中ob_refcnt就是做为引用计数。     
当一个对象有新的引用时，它的ob_refcnt就会增加，当引用它的对象被删除，它的ob_refcnt就会减少      
```Python
#define Py_INCREF(op)   ((op)->ob_refcnt++) //增加计数
#define Py_DECREF(op) \ //减少计数
    if (--(op)->ob_refcnt != 0) \
        ; \
    else \
        __Py_Dealloc((PyObject *)(op))
```
当引用计数为0时，该对象生命就结束了。

引用计数机制的优点：

1. 简 单
2. 实时性: 一旦没有引用，内存就直接释放了。不用像其他机制等到特定时机。   
3. 实时性还带来一个好处：处理回收内存的时间分摊到了平时。  

引用计数机制的缺点：   
1. 维护引用计数消耗资源
2. 循环引用
```Python
list1 = []
list2 = []
list1.append(list2)
list2.append(list1)
```
list1与list2相互引用，如果不存在其他对象对它们的引用，list1与list2的引用计数也仍然为1，所占用的内存永远无法被回收，这将是致命的。   
对于如今的强大硬件，缺点1尚可接受，但是循环引用导致内存泄露，[注定Python还将引入新的回收机制](https://my.oschina.net/hebianxizao/blog/57367?fromerr=KJozamtm)。(标记清除和分代收集)    


[画说Ruby与Python垃圾回收](https://ruby-china.org/topics/28127)   
========  
[油管英文学术交流视频](https://www.youtube.com/watch?v=qzEekAnAS_g)   

### 应用程序那颗跃动的心   
GC(Garbage Collection)系统所承担的工作远比"垃圾回收"多得多。 实际上，它们负责三个重要任务:          
* 1. 为新生成的对象分配内存   
* 2. 识别垃圾对象      
* 3. 从垃圾回收内存   

如果将应用程序比作人的身体：所有你所写的那些优雅的代码，业务逻辑，算法，应该就是大脑。    
以此类推，垃圾回收机制应该是那个身体器官呢？（我从RuPy听众那听到了不少有趣的答案: 腰子、白血球)       

我认为垃圾回收就是应用程序那颗跃动的心。 像心脏为身体其他器官提供血液和营养物那样，垃圾回收器为你的应该程序提供内存和对象。  

如果心脏停跳，过不了几秒钟人就完了。如果垃圾回收器停止工作或运行迟缓, 像动脉阻塞, 你的应用程序效率也会下降，直至最终死掉。      

### 一个简单的例子    
分别用Python和Ruby写成，例:   
![ScreenShot-00307](https://github.com/KissMyLady/Python/blob/master/Img/oop/ScreenShot-00307.jpg)   
顺便提一句，两种语言的代码竟能如此相像: Ruby和 Python在表达同一事物上真的只是略有不同  
但是在这两种语言的内部实现上是否也如此相似呢？    

### 1. Ruby的可用列表分配方式     
```Ruby
class Node
    def initialize(val)
    	@value = val
    end
end

p Node.new(1)
p Node.new(2)
```
当我们执行上面的Node.new(1)时，Ruby到底做了什么？ Ruby是如何为我们创建新的对象的呢？       
出乎意料的是它做的非常少。 
实际上，早在代码开始执行前，Ruby就提前创建了成百上千个对象，并把它们串在链表上，名曰：可用列表。  
下图所示为可用列表的概念图：   
![ScreenShot-00308](https://github.com/KissMyLady/Python/blob/master/Img/oop/ScreenShot-00308.jpg)   
想象一下每个白色方格上都标着一个"未使用预创建对象"。当我们调用 Node.new ,Ruby只需取一个预创建对象给我们使用即可(简化图):    
![ScreenShot-00309](https://github.com/KissMyLady/Python/blob/master/Img/oop/ScreenShot-00309.jpg)   

上图中左侧灰格表示我们代码中使用的当前对象, 同时其他白格是未使用对象。     
实际上，Ruby会用另一个对象来装载字符串"ABC", 另一个对象装载Node类定义，还有一个对象装载了代码中分析出的抽象语法树，等等    

如果我们再次调用`Node.new`，Ruby将递给我们另一个对象:     
![ScreenShot-00310](https://github.com/KissMyLady/Python/blob/master/Img/oop/ScreenShot-00310.jpg)   
这个简单的用链表来预分配对象的算法已经发明了超过50年，而发明人这是赫赫有名的计算机科学家John McCarthy，一开始是用Lisp实现的。   
Lisp不仅是最早的函数式编程语言，在计算机科学领域也有许多创举。其一就是利用垃圾回收机制自动化进行程序内存管理的概念。   

标准版的Ruby，也就是众所周知的"Matz's Ruby Interpreter"(MRI),所使用的GC算法与McCarthy在1960年的实现方式很类似。无论好坏，Ruby的垃圾回收机制已经53岁高龄了。   
像Lisp一样，Ruby预先创建一些对象，然后在你分配新对象或者变量的时候供你使用。    



### 2. Python的对象分配
尽管由于许多原因Python也使用可用列表(用来回收一些特定对象比如 list)，但在为新对象和变量分配内存的方面Python和Ruby是不同的。   

例如我们用Pyhon来创建一个Node对象：
```Python
class Node:
	def __init__(self, val):
		self.value = val

print(Node(1))
print(Node(2))
```
![ScreenShot-00311](https://github.com/KissMyLady/Python/blob/master/Img/oop/ScreenShot-00311.jpg)   
#### 与Ruby不同，当创建对象时Python立即`向操作系统请求内存`      
Python实际上实现了一套自己的内存分配系统，在操作系统堆之上提供了一个抽象层   

当我们创建第二个对象的时候，再次像OS请求内存:    
![ScreenShot-00312](https://github.com/KissMyLady/Python/blob/master/Img/oop/ScreenShot-00312.jpg)  
很简单, 在我们创建对象的时候，Python会花些时间为我们找到并分配内存   


### 3. Ruby开发者住在凌乱的房间里
![ScreenShot-00313](https://github.com/KissMyLady/Python/blob/master/Img/oop/ScreenShot-00313.jpg)   
Ruby把无用的对象留在内存里，直到下一次GC执行

随着我们创建越来越多的对象，Ruby会持续寻可用列表里取预创建对象给我们。 因此，可用列表会逐渐变短, 然后更短:      
![ScreenShot-00314](https://github.com/KissMyLady/Python/blob/master/Img/oop/ScreenShot-00314.jpg)   
Ruby不会立即清除代码中不再使用的旧对象！Ruby开发者们就像是住在一间凌乱的房间，地板上摞着衣服，要么洗碗池里都是脏盘子。   
作为一个Ruby程序员，无用的垃圾对象会一直环绕着你。   


### 4. Python开发者住在卫生之家庭
![ScreenShot-00315](https://github.com/KissMyLady/Python/blob/master/Img/oop/ScreenShot-00315.jpg)   
在内部，创建一个对象时，Python总是在对象的C结构体里保存一个整数，称为`引用数`。 初，Python将这个值设置为1   

值为1说明分别有个一个指针指向或是引用这三个对象。  假如我们现在创建一个新的Node实例，JKL：   

与之前一样，Python设置JKL的引用数为1。然而，请注意由于我们改变了n1指向了JKL，不再指向ABC，Python就把ABC的引用数置为0了    
此刻，Python垃圾回出来! 每当对象的引用数减为0, Python立即将其释放，把内存还给操作系统      
![ScreenShot-00316](https://github.com/KissMyLady/Python/blob/master/Img/oop/ScreenShot-00316.jpg)   
这样Python就回收了ABC Node实例使用的内存。    
而Ruby弃旧对象原地于不顾，也不释放它们的内存。     
Python的这种垃圾回收算法被称为`引用计数`。 是George-Collins在1960年发明的，恰巧与John McCarthy发明的可用列表算法在同一年出现。    
就像Mike-Bernstein在6月份哥谭市Ruby大会杰出的垃圾回收机制演讲中说的: `"1960年是垃圾收集器的黄金年代..."`   

Python开发者工作在卫生之家，你可以想象，有个患有轻度OCD(一种强迫症)的室友一刻不停地跟在你身后打扫，你一放下脏碟子或杯子，有个家伙已经准备好把它放进洗碗机了!      


### 5. 标记-清除
最终那间凌乱的房间充斥着垃圾，再不能岁月静好。 在Ruby程序运行了一阵子以后，可用列表最终被用光了:       
![ScreenShot-00317](https://github.com/KissMyLady/Python/blob/master/Img/oop/ScreenShot-00317.jpg)   
此刻所有Ruby预创建对象都被程序用过了(变灰了)，可用列表里空空如也(没有白格子)     

此刻Ruby祭出另一McCarthy发明的算法，名曰: `标记-清除`    
* 1. 首先Ruby把程序停下来，Ruby用`地球停转垃圾回收大法`      
* 2. 之后Ruby轮询所有指针，变量和代码产生别的引用对象和其他值    
* 3. 同时Ruby通过自身的虚拟机遍历内部指针   
* 4. 标记出这些指针引用的每个对象。 图中M表示        
![ScreenShot-00318](https://github.com/KissMyLady/Python/blob/master/Img/oop/ScreenShot-00318.jpg)   
图中那三个被标M的对象是程序还在使用的。
在内部，Ruby实际上使用一串位值，被称为:可用位图来跟踪对象是否被标记了。       
![ScreenShot-00319](https://github.com/KissMyLady/Python/blob/master/Img/oop/ScreenShot-00319.jpg)   
Ruby将这个`可用位图`存放在独立的内存区域中，以便充分利用Unix的写时拷贝化。
如果说被标记的对象是存活的，剩下的未被标记的对象只能是垃圾，这意味着我们的代码不再会使用它了。 在下图中用白格子表示垃圾对象:       
![ScreenShot-00320](https://github.com/KissMyLady/Python/blob/master/Img/oop/ScreenShot-00320.jpg)   
接下来Ruby清除这些无用的垃圾对象，把它们送回到可用列表中:   
![ScreenShot-00321](https://github.com/KissMyLady/Python/blob/master/Img/oop/ScreenShot-00321.jpg)   
在内部这一切发生得迅雷不及掩耳，因为Ruby实际上不会吧对象从这拷贝到那。而是通过调整内部指针，将其指向一个新链表的方式，来将垃圾对象归位到可用列表中的。   

现在等到下回再创建对象的时候Ruby又可以把这些垃圾对象分给我们使用了。 在Ruby里，对象们六道轮回，转世投胎，享受多次人生。   



### 6. 标记-删除 VS 引用计数  
乍一看，Python的GC算法貌似远胜于Ruby的: 宁舍洁而居秽乎？ 为什么Ruby宁愿定期强制程序停止运行，也不使用Python的算法呢？

然而，引用计数并不像第一眼看上去那样简单。 有许多原因使得不许多语言不像Python这样使用引用计数GC算法:  

1. 首先，它不好实现。 Python不得不在每个对象内部留一些空间来处理引用数。 这样付出了一小点儿空间上的代价。但更糟糕的是，每个简单的操作（像修改变量或引用）都会变成一个更复杂的操作，因为Python需要增加一个计数，减少另一个，还可能释放对象。   

2. 第二点，它相对较慢。 虽然Python随着程序执行GC很稳健(一把脏碟子放在洗碗盆里就开始洗啦)，但这并不一定更快。Python不停地更新着众多引用数值。特别是当你不再使用一个大数据结构的时候，比如一个包含很多元素的列表，Python可能必须一次性释放大量对象。减少引用数就成了一项复杂的递归过程了。   

3. 最后，它不是总奏效的。 引用计数不能处理`环形数据结构`--也就是含有`循环引用`的数据结构。       



### 7. Python中的循环数据结构以及引用计数
Python在引用计数之外，还用了另一个名为`Generational Garbage Collection`的算法     
这意味着Python的垃圾回收器用不同的方式对待新创建的以及旧有的对象   
并且在即将到来的2.1版本的MRI Ruby中也首次引入了`Generational Garbage Collection`的垃圾回收机制   
(在另两个Ruby的实现：JRuby和Rubinius中，已经使用这种GC机制很多年了        

当然，这句话“用不同的方式对待新创建的以及旧有的对象”是有点模糊不清，比如如何定义新、旧对象？
又比如对于Ruby和Python来说具体是如何采取不同的对待方式？今天，我们就来谈谈这两种语言GC机制的运行原理，
回答上边那些疑问。但是在我们开始谈论Generational GC之前，我们先要花点时间谈论下Python的引用计数算法的一个严重的理论问题   

### 7.1 Python中的循环数据结构以及引用计数
我们知道在Python中，每个对象都保存了一个称为引用计数的整数值，来追踪到底有多少引用指向了这个对象。
无论何时，如果我们程序中的一个变量或其他对象引用了目标对象，Python将会增加这个计数值，而当程序停止使用这个对象，则Python会减少这个计数值。   
一旦计数值被减到零，Python将会释放这个对象以及回收相关内存空间。     

从六十年代开始，计算机科学界就面临了一个严重的理论问题，那就是针对引用计数这种算法来说: 如果一个数据结构引用了它自身，即如果这个数据结构是一个循环数据结构，那么某些引用计数值是肯定无法变成零的。   
为了更好地理解这个问题，让我们举个例子。   
下面的代码展示了一些上周我们所用到的节点类：  
![ScreenShot-00322](https://github.com/KissMyLady/Python/blob/master/Img/oop/ScreenShot-00322.jpg)   
我们有一个构造器(Python中叫做init), 在一个实例变量中存储一个单独的属性。 在类定义之后我们创建两个节点，ABC以及DEF，在图中为左边的矩形框。两个节点的引用计数都被初始化为1，因为各有两个引用指向各个节点(n1和n2)   

现在，让我们在节点中定义两个附加的属性，Next以及Prev:       
![ScreenShot-00323](https://github.com/KissMyLady/Python/blob/master/Img/oop/ScreenShot-00323.jpg)   
跟Ruby不同的是，Python中你可以在代码运行的时候动态定义实例变量或对象属性    
这看起来似乎有点像Ruby缺失了某些有趣的魔法。    
   
我们设置 n1.next 指向 n2，同时设置 n2.prev 指回 n1。现在，我们的两个节点使用循环引用的方式构成了一个双端链表。
同时请注意到 ABC 以及 DEF 的引用计数值已经增加到了2。这里有两个指针指向了每个节点：首先是 n1 以及 n2，其次就是 next 以及 prev。   

现在，假定我们的程序不再使用这两个节点了，我们将 n1 和 n2 都设置为null(Python中是None)。

好了，Python会像往常一样将每个节点的引用计数减少到1。   




### 8. 在Python中的零代(Generation Zero)
请注意刚刚说到的例子中，我们以一个不是很常见的情况结尾: 我们有一个“孤岛”或是一组未使用的、互相指向的对象，但是谁都没有外部引用。  
换句话说，我们的程序不再使用这些节点对象了，所以我们希望Python的垃圾回收机制能够足够智能去释放这些对象并回收它们占用的内存空间。  
但是这不可能，因为所有的引用计数都是1而不是0。 Python的引用计数算法不能够处理互相指向自己的对象。   

当然，上边举的是一个故意设计的例子，但是你的代码也许会在不经意间包含循环引用并且你并未意识到。  
事实上，当你的Python程序运行的时候它将会建立一定数量的“浮点数垃圾”，Python的GC不能够处理未使用的对象因为应用计数值不会到零。   

这就是为什么Python要引入Generational GC算法的原因! 正如Ruby使用一个链表(free list)来持续追踪未使用的、自由的对象一样，Python使用一种不同的链表来持续追踪活跃的对象。    
而不将其称之为“活跃列表”，Python的内部C代码将其称为零代(Generation Zero)。每次当你创建一个对象或其他什么值的时候，Python会将其加入零代链表：  
![ScreenShot-00324](https://github.com/KissMyLady/Python/blob/master/Img/oop/ScreenShot-00324.jpg)   

可以看到当我们创建ABC节点的时候，Python将其加入零代链表。 请注意到这并不是一个真正的列表，并不能直接在你的代码中访问，事实上这个链表是一个完全内部的Python运行时。   
相似的，当我们创建DEF节点的时候，Python将其加入同样的链表:     
![ScreenShot-00325](https://github.com/KissMyLady/Python/blob/master/Img/oop/ScreenShot-00325.jpg)  
现在零代包含了两个节点对象。(他还将包含Python创建的每个其他值，与一些Python自己使用的内部值。)   

### 9. 检测循环引用
随后，Python会循环遍历零代列表上的每个对象，检查列表中每个互相引用的对象，根据规则减掉其引用计数。      
在这个过程中，Python会一个接一个的统计内部引用的数量以防过早地释放对象。  

为了便于理解，来看一个例子
![ScreenShot-00326](https://github.com/KissMyLady/Python/blob/master/Img/oop/ScreenShot-00326.jpg)  
从上面可以看到 ABC和 DEF节点包含的引用数为1, 有三个其他的对象同时存在于零代链表中, 蓝色的箭头指示了有一些对象正在被零代链表之外的其他对象所引用。     
接下来我们会看到，Python中同时存在另外两个分别被称为一代和二代的链表     
这些对象有着更高的引用计数因为它们正在被其他指针所指向着。   
   
接下来看看Python的GC是如何处理零代链表的     
![ScreenShot-00327](https://github.com/KissMyLady/Python/blob/master/Img/oop/ScreenShot-00327.jpg)   
通过识别内部引用，Python能够减少许多零代链表对象的引用计数。   
在上图的第一行中你能够看见ABC和DEF的引用计数已经变为零了，这意味着收集器可以释放它们并回收内存空间了。  
剩下的活跃的对象则被移动到一个新的链表：一代链表。   

从某种意义上说，Python的GC算法类似于Ruby所用的标记回收算法。  
周期性地从一个对象到另一个对象追踪引用以确定对象是否还是活跃的，正在被程序所使用的，这正类似于Ruby的标记过程   
	

### 10. Python中的GC阈值
* Python什么时候会进行这个标记过程？   

随着你的程序运行，Python解释器保持对新创建的对象，以及因为引用计数为零而被释放掉的对象的追踪。
从理论上说，这两个值应该保持一致，因为程序新建的每个对象都应该最终被释放掉。

当然，事实并非如此。 因为循环引用的原因，并且因为你的程序使用了一些比其他对象存在时间更长的对象，从而被分配对象的计数值与被释放对象的计数值之间的差异在逐渐增长。   
一旦这个差异累计超过某个阈值，则Python的收集机制就启动了，并且触发上边所说到的零代算法，释放“浮动的垃圾”，并且将剩下的对象移动到一代列表。   

随着时间的推移，程序所使用的对象逐渐从零代列表移动到一代列表。 而Python对于一代列表中对象的处理遵循同样的方法，一旦被分配计数值与被释放计数值累计到达一定阈值，Python会将剩下的活跃对象移动到二代列表。

通过这种方法，你的代码所长期使用的对象，那些你的代码持续访问的活跃对象，会从零代链表转移到一代再转移到二代     
通过不同的阈值设置，Python可以在不同的时间间隔处理这些对象。Python处理零代最为频繁，其次是一代然后才是二代   

### 11. 弱代假说

根据假说，我的代码很可能仅仅会使用ABC很短的时间。  
这个对象也许仅仅只是一个方法中的中间结果，并且随着方法的返回这个对象就将变成垃圾了。  

大部分的新对象都是如此般地很快变成垃圾。 然而，偶尔程序会创建一些很重要的，存活时间比较长的对象-例如web应用中的session变量或是配置项。   

通过频繁的处理零代链表中的新对象，Python的垃圾收集器将把时间花在更有意义的地方: 它处理那些很快就可能变成垃圾的新对象。同时只在很少的时候，当满足阈值的条件，收集器才回去处理那些老变量。   








### 12. 回到Ruby的自由链
即将到来的Ruby 2.1版本将会首次使用基于代的垃圾回收算法！(请注意的是，其他的Ruby实现，例如JRuby和Rubinius已经使用这个算法许多年了)。让我们回到上篇博文中提到的自由链的图来看看它到底是怎么工作的。  

请回忆当自由链使用完之后，Ruby会标记你的程序仍然在使用的对象。
![ScreenShot-00328](https://github.com/KissMyLady/Python/blob/master/Img/oop/ScreenShot-00328.jpg)  
从这张图上我们可以看到有三个活跃的对象，因为指针n1、n2、n3仍然指向着它们。   
剩下的用白色矩形表示的对象即是垃圾。(当然，实际情况会复杂得多，自由链可能会包含上千个对象，并且有复杂的引用指向关系，这里的简图只是帮助我们了解Ruby的GC机制背后的简单原理，而不会将我们陷入细节之中)   

同样，我们说过Ruby会将垃圾对象移动回自由链中，这样的话它们就能在程序申请新对象的时候被循环使用了。   
![ScreenShot-00329](https://github.com/KissMyLady/Python/blob/master/Img/oop/ScreenShot-00329.jpg)   



### 13. Ruby2.1基于代的GC机制
从2.1版本开始，Ruby的GC代码增加了一些附加步骤：它将留下来的活跃对象晋升(promote)到成熟代(mature generation)中。(在MRI的C源码中使用了old这个词而不是mature)，接下来的图展示了两个Ruby2.1对象代的概念图:    
![ScreenShot-00330](https://github.com/KissMyLady/Python/blob/master/Img/oop/ScreenShot-00330.jpg)   
在左边是一个跟自由链不相同的场景，我们可以看到垃圾对象是用白色表示的，剩下的是灰色的活跃对象。 灰色的对象刚刚被标记    

一旦“标记清除”过程结束，Ruby2.1将剩下的标记对象移动到成熟区:   
![ScreenShot-00331](https://github.com/KissMyLady/Python/blob/master/Img/oop/ScreenShot-00331.jpg)   
跟Python中使用三代来划分不同，Ruby2.1只用了两代，左边是年轻的新一代对象，而右边是成熟代的老对象。一旦Ruby2.1标记了对象一次，它就会被认为是成熟的。Ruby会打赌剩下的活跃对象在相当长的一段时间内不会很快变成垃圾对象。

重要提醒：Ruby2.1并不会真的在内存中拷贝对象，这些代表不同代的区域并不是由不同的物理内存区域构成。(有一些别的编程语言的GC实现或是Ruby的其他实现，可能会在对象晋升的时候采取拷贝的操作)。Ruby2.1的内部实现不会将在标记&清除过程中预先标记的对象包含在内。一旦一个对象已经被标记过一次了，那么那将不会被包含在接下来的标记清除过程中。

现在，假定你的Ruby程序接着运行着，创造了更多新的，更年轻的对象。则GC的过程将会在新的一代中出现，如图：
![ScreenShot-00332](https://github.com/KissMyLady/Python/blob/master/Img/oop/ScreenShot-00332.jpg)   
如同Python那样，Ruby的垃圾收集器将大部分精力都放在新一代的对象之上。它仅仅会将自上一次GC过程发生后创建的新的、年轻的对象包含在接下来的标记清除过程中。这是因为很多新对象很可能马上就会变成垃圾(白色标记)。Ruby不会重复标记右边的成熟对象。因为他们已经在一次GC过程中存活下来了，在相当长的一段时间内不会很快变成垃圾。因为只需要标记新对象，所以Ruby 的GC能够运行得更快。它完全跳过了成熟对象，减少了代码等待GC完成的时间。   

偶然的Ruby会运行一次“全局回收”，重标记(re-marking)并重清除(re-sweeping)，这次包括所有的成熟对象。Ruby通过监控成熟对象的数目来确定何时运行全局回收。当成熟对象的数目双倍于上次全局回收的数目时，Ruby会清理所有的标记并且将所有的对象都视为新对象。   


### 14. 白 障
这个算法的一个重要挑战是值得深入解释的: 假定你的代码创建了一个新的年轻的对象，并且将其作为一个已存在的成熟对象的子嗣加入。举个例子，这种情况将会发生在，当你往一个已经存在了很长时间的数组中增加了一个新值的时候：   
![ScreenShot-00333](https://github.com/KissMyLady/Python/blob/master/Img/oop/ScreenShot-00333.jpg)   
让我们来看看图，左边的是新对象，而成熟的对象在右边。在左边标记过程已经识别出了5个新的对象目前仍然是活跃的(灰色)。但有两个对象已经变成垃圾了(白色)。但是如何处理正中间这个新建对象？这是刚刚那个问题提到的对象，它是垃圾还是活跃对象呢？    

当然它是活跃对象了，因为有一个从右边成熟对象的引用指向它。但是我们前面说过已经被标记的成熟对象是不会被包含在标记清除过程中的(一直到全局回收)。这意味着类似这种的新建对象会被错误的认为是垃圾而被释放，从而造成数据丢失。    

Ruby2.1 通过监视成熟对象，观察你的代码是否会添加一个从它们到新建对象的引用来克服这个问题。Ruby2.1 使用了一个名为白障(white barriers)的老式GC技术来监视成熟对象的变化 – 无论任意时刻当你添加了从一个对象指向另一个对象的引用时(无论是新建或是修改一个对象)，白障就会被触发。白障将会检测是否源对象是一个成熟对象，如果是的话则将这个成熟对象添加到一个特殊的列表中。随后，Ruby2.1会将这些满足条件的成熟对象包括到下一次标记清除的范围内，以防止新建对象被错误的标记为垃圾而清除。    

Ruby2.1 的白障实现相当复杂，主要是因为已有的C扩展并未包含这部分功能。Koichi Sasada以及Ruby的核心团队使用了一个比较巧妙的方案来解决这个问题。如果想了解更多的内容，请阅读这些相关材料：Koichi在EuRuKo 2013上的演讲Koichi’s fascinating presentation。    




### 15. 站在巨人的肩膀上
乍眼一看，Ruby和Python的GC实现是截然不同的，Ruby使用John-MaCarthy的原生“标记并清除”算法，而Python使用引用计数。 但是仔细看来，可以发现Python使用了些许标记清除的思想来处理循环引用，  

而两者同时以相似的方式使用基于代的垃圾回收算法。Python划分了三代，而Ruby只有两代。

这种相似性应该不会让人感到意外。 两种编程语言都使用了几十年前的计算机科学研究成果来进行设计，这些成果早在语言成型之前就已经被做出来了。我比较惊异的是当你掀开不同编程语言的表面而深入底层，你总能够发现一些相似的基础理念和算法。  

现代编程语言应该感激那些六七十年代由麦卡锡等计算机先贤所作出的计算机科学开创性研究  




