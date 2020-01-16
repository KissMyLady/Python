[代码风格规范(PEP8)](https://github.com/CyC2018/CS-Notes/blob/master/notes/%E4%BB%A3%E7%A0%81%E5%8F%AF%E8%AF%BB%E6%80%A7.md)   
====
<!-- GFM-TOC -->
* [一、可读性的重要性](#一可读性的重要性)
* [二、用名字表达代码含义](#二用名字表达代码含义)
* [三、名字不能带来歧义](#三名字不能带来歧义)
* [四、良好的代码风格](#四良好的代码风格)
* [五、为何编写注释](#五为何编写注释)
* [六、如何编写注释](#六如何编写注释)
* [七、提高控制流的可读性](#七提高控制流的可读性)
* [八、拆分长表达式](#八拆分长表达式)
* [九、变量与可读性](#九变量与可读性)
* [十、抽取函数](#十抽取函数)
* [十一、一次只做一件事](#十一一次只做一件事)
* [十二、用自然语言表述代码](#十二用自然语言表述代码)
* [十三、减少代码量](#十三减少代码量)
* [参考资料](#参考资料)
<!-- GFM-TOC -->

# [Python官网PEP-8规范](https://www.python.org/dev/peps/pep-0008/)    
# [PythonPython PEP-8编码风格指南中文版](https://alvinzhu.xyz/2017/10/07/python-pep-8/)    
# 一、可读性的重要性

编程有很大一部分时间是在阅读代码，不仅要阅读自己的代码，而且要阅读别人的代码。因此，可读性良好的代码能够大大提高编程效率。

可读性良好的代码往往会让代码架构更好，因为程序员更愿意去修改这部分代码，而且也更容易修改。

只有在核心领域为了效率才可以放弃可读性，否则可读性是第一位。

# 二、用名字表达代码含义

一些比较有表达力的单词：

|  单词 |  可替代单词 |
| :---: | --- |
| send | deliver、dispatch、announce、distribute、route  |
| find  |  search、extract、locate、recover |
| start| launch、create、begin、open|
| make | create、set up、build、generate、compose、add、new |

使用 i、j、k 作为循环迭代器的名字过于简单，user_i、member_i 这种名字会更有表达力。因为循环层次越多，代码越难理解，有表达力的迭代器名字可读性会更高。

为名字添加形容词等信息能让名字更具有表达力，但是名字也会变长。名字长短的准则是：作用域越大，名字越长。因此只有在短作用域才能使用一些简单名字。

# 三、名字不能带来歧义

起完名字要思考一下别人会对这个名字有何解读，会不会误解了原本想表达的含义。

布尔相关的命名加上 is、can、should、has 等前缀。

- 用 min、max 表示数量范围；
- 用 first、last 表示访问空间的包含范围；

- begin、end 表示访问空间的排除范围，即 end 不包含尾部。

<div align="center"> <img src="https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot-00277.jpg"/> </div><br>

# 四、良好的代码风格

适当的空行和缩进。

排列整齐的注释：

```java
int a = 1;   // 注释
int b = 11;  // 注释
int c = 111; // 注释
```

语句顺序不能随意，比如与 html 表单相关联的变量的赋值应该和表单在 html 中的顺序一致。

# 五、为何编写注释

阅读代码首先会注意到注释，如果注释没太大作用，那么就会浪费代码阅读的时间。那些能直接看出含义的代码不需要写注释，特别是不需要为每个方法都加上注释，比如那些简单的 getter 和 setter 方法，为这些方法写注释反而让代码可读性更差。

不能因为有注释就随便起个名字，而是争取起个好名字而不写注释。

可以用注释来记录采用当前解决办法的思考过程，从而让读者更容易理解代码。

注释用来提醒一些特殊情况。

用 TODO 等做标记：

| 标记 | 用法 |
|---|---|
|TODO| 待做 |
|FIXME| 待修复 |
|HACK| 粗糙的解决方案 |
|XXX| 危险！这里有重要的问题 |

# 六、如何编写注释

尽量简洁明了：

```java
// The first String is student's name
// The Second Integer is student's score
Map<String, Integer> scoreMap = new HashMap<>();
```

```java
// Student's name -> Student's score
Map<String, Integer> scoreMap = new HashMap<>();
```

添加测试用例来说明：

```java
// ...
// Example: add(1, 2), return 3
int add(int x, int y) {
    return x + y;
}
```

使用专业名词来缩短概念上的解释，比如用设计模式名来说明代码。

# 七、提高控制流的可读性

条件表达式中，左侧是变量，右侧是常数。比如下面第一个语句正确：

```java
if (len < 10)
if (10 > len)
```

只有在逻辑简单的情况下使用 ? : 三目运算符来使代码更紧凑，否则应该拆分成 if / else；

do / while 的条件放在后面，不够简单明了，并且会有一些迷惑的地方，最好使用 while 来代替。

如果只有一个 goto 目标，那么 goto 尚且还能接受，但是过于复杂的 goto 会让代码可读性特别差，应该避免使用 goto。

在嵌套的循环中，用一些 return 语句往往能减少嵌套的层数。

# 八、拆分长表达式

长表达式的可读性很差，可以引入一些解释变量从而拆分表达式：

```python
if line.split(':')[0].strip() == "root":
    ...
```
```python
username = line.split(':')[0].strip()
if username == "root":
    ...
```

使用摩根定理简化一些逻辑表达式：

```java
if (!a && !b) {
    ...
}
```
```java
if (!(a || b)) {
    ...
}
```

# 九、变量与可读性

**去除控制流变量**  。在循环中通过使用 break 或者 return 可以减少控制流变量的使用。

```java
boolean done = false;
while (/* condition */ && !done) {
    ...
    if ( ... ) {
        done = true;
        continue;
    }
}
```

```java
while(/* condition */) {
    ...
    if ( ... ) {
        break;
    }
}
```

**减小变量作用域**  。作用域越小，越容易定位到变量所有使用的地方。

JavaScript 可以用闭包减小作用域。以下代码中 submit_form 是函数变量，submitted 变量控制函数不会被提交两次。第一个实现中 submitted 是全局变量，第二个实现把 submitted 放到匿名函数中，从而限制了起作用域范围。

```js
submitted = false;
var submit_form = function(form_name) {
    if (submitted) {
        return;
    }
    submitted = true;
};
```

```js
var submit_form = (function() {
    var submitted = false;
    return function(form_name) {
        if(submitted) {
            return;
        }
        submitted = true;
    }
}());  // () 使得外层匿名函数立即执行
```

JavaScript 中没有用 var 声明的变量都是全局变量，而全局变量很容易造成迷惑，因此应当总是用 var 来声明变量。

变量定义的位置应当离它使用的位置最近。

**实例解析**  

在一个网页中有以下文本输入字段：

```html
<input type = "text" id = "input1" value = "a">
<input type = "text" id = "input2" value = "b">
<input type = "text" id = "input3" value = "">
<input type = "text" id = "input4" value = "d">
```

现在要接受一个字符串并把它放到第一个空的 input 字段中，初始实现如下：

```js
var setFirstEmptyInput = function(new_alue) {
    var found = false;
    var i = 1;
    var elem = document.getElementById('input' + i);
    while (elem != null) {
        if (elem.value === '') {
            found = true;
            break;
        }
        i++;
        elem = document.getElementById('input' + i);
    }
    if (found) elem.value = new_value;
    return elem;
}
```

以上实现有以下问题：

- found 可以去除；
- elem 作用域过大；
- 可以用 for 循环代替 while 循环；

```js
var setFirstEmptyInput = function(new_value) {
    for (var i = 1; true; i++) {
        var elem = document.getElementById('input' + i);
        if (elem === null) {
            return null;
        }
        if (elem.value === '') {
            elem.value = new_value;
            return elem;
        }
    }
};
```

# 十、抽取函数

工程学就是把大问题拆分成小问题再把这些问题的解决方案放回一起。

首先应该明确一个函数的高层次目标，然后对于不是直接为了这个目标工作的代码，抽取出来放到独立的函数中。

介绍性的代码：

```java
int findClostElement(int[] arr) {
    int clostIdx;
    int clostDist = Interger.MAX_VALUE;
    for (int i = 0; i < arr.length; i++) {
        int x = ...;
        int y = ...;
        int z = ...;
        int value = x * y * z;
        int dist = Math.sqrt(Math.pow(value, 2), Math.pow(arr[i], 2));
        if (dist < clostDist) {
            clostIdx = i;
            clostDist = value;
        }
    }
    return clostIdx;
}
```

以上代码中循环部分主要计算距离，这部分不属于代码高层次目标，高层次目标是寻找最小距离的值，因此可以把这部分代替提取到独立的函数中。这样做也带来一个额外的好处有：可以单独进行测试、可以快速找到程序错误并修改。

```java
public int findClostElement(int[] arr) {
    int clostIdx;
    int clostDist = Interger.MAX_VALUE;
    for (int i = 0; i < arr.length; i++) {
        int dist = computDist(arr, i);
        if (dist < clostDist) {
            clostIdx = i;
            clostDist = value;
        }
    }
    return clostIdx;
}
```

并不是函数抽取的越多越好，如果抽取过多，在阅读代码的时候可能需要不断跳来跳去。只有在当前函数不需要去了解某一块代码细节而能够表达其内容时，把这块代码抽取成子函数才是好的。

函数抽取也用于减小代码的冗余。

# 十一、一次只做一件事

只做一件事的代码很容易让人知道其要做的事；

基本流程：列出代码所做的所有任务；把每个任务拆分到不同的函数，或者不同的段落。

# 十二、用自然语言表述代码

先用自然语言书写代码逻辑，也就是伪代码，然后再写代码，这样代码逻辑会更清晰。

# 十三、减少代码量

不要过度设计，编码过程会有很多变化，过度设计的内容到最后往往是无用的。

多用标准库实现。

# 参考资料

- Dustin, Boswell, Trevor, 等. 编写可读代码的艺术 [M]. 机械工业出版社, 2012.


# 为什么要规范?  
正规军与杂牌军的区别  
[PEP8编码规范](https://blog.csdn.net/qq_33591055/article/details/99581791)    
[PEP8编码规范--此文模板知识来源](https://www.cnblogs.com/liangmingshen/p/9273413.html)


## 一 代码编排
1 缩进:  4个空格的缩进（编辑器都可以完成此功能），不要使用Tap，更不能混合使用Tap和空格   

2 每行最大长度79，换行可以使用反斜杠，最好使用圆括号,  换行点要在操作符的后边敲回车     

3 类和top-level函数定义之间空两行   
> 类中的方法定义之间空一行    
>  函数内逻辑无关段落之间空一行    
> 其他地方尽量不要再空行      

## 二 文档编排
1 模块内容的顺序: 模块说明和`docstring—import—globals&constants`—其他定义。 其中import部分，又按标准、三方和自己编写顺序依次排放，之间空一行     

2 不要在一句import中多个库，比如`import os, sys`不推荐       

3 如果采用`from XX import XX`引用库，可以省略`module.`，都是可能出现命名冲突，这时就要采用import XX   


## 三 空格的使用
* 总体原则，避免不必要的空格     
1 各种右括号前不要加空格          
2 逗号、冒号、分号前不要加空格          

3 函数的左括号前不要加空格。如Func(1)     
4 序列的左括号前不要加空格。如list[2]     
5 操作符左右各加一个空格，不要为了对齐增加空格     

6 函数默认参数的赋值符左右省略空格     
7 不要将多句语句写在同一行，尽管使用‘；’允许     
8 `if/for/while`语句中，即使执行语句只有一句，也必须另起一行     

## 四 注释
总体原则，错误的注释不如没有注释。 所以当一段代码发生变化时，第一件事就是要修改注释！     
注释必须使用英文，最好是完整的句子，首字母大写，句后要有结束符，结束符后跟两个空格，开始下一句。如果是短语，可以省略结束符。  

1 块注释，在一段代码前增加的注释。在`#`后加一空格。段落之间以只有‘#’的行间隔。     

2 行注释，在一句代码后加注释。比如：x = x + 1 # Increment x     
但是这种方式尽量少使用。     
3 避免无谓的注释。     

## 五 文档描述     
1 为所有的共有模块、函数、类、方法写docstrings；非共有的没有必要，但是可以写注释（在def的下一行）     
2 如果docstring要换行，参考如下例子     
"""
Return a foobang
Optional plotz says to frobnicate the bizbaz first.
"""
## 六 命名规范     
总体原则，新编代码必须按下面命名风格进行，现有库的编码尽量保持风格      
1 尽量单独使用小写字母‘l’，大写字母‘O’等容易混淆的字母      
2 模块命名尽量短小，使用全部小写的方式，可以使用下划线        
3 包命名尽量短小，使用全部小写的方式，不可以使用下划线     

4 类的命名使用CapWords的方式，模块内部使用的类采用_CapWords的方式      
5 异常命名使用CapWords+Error后缀的方式        
6 全局变量尽量只在模块内有效，类似C语言中的static。实现方法有两种，一是`__all__`机制; 二是前缀一个下划线  
7 函数命名使用全部小写的方式，可以使用下划线       
8 常量命名使用全部大写的方式，可以使用下划线       

9 类的属性（方法和变量）命名使用全部小写的方式，可以使用下划线      
9 类的属性有3种作用域`public、non-public`和`subclass API`，可以理解成C++中的public、private、protected，non-public属性前，前缀一条下划线       
11 类的属性若与关键字名字冲突，后缀一下划线，尽量不要使用缩略等其他方式      
12 为避免与子类属性命名冲突，在类的一些属性前，前缀两条下划线。比如：类Foo中声明`__a`,访问时，只能通过`Foo._Foo__a`，避免歧义。  如果子类也叫Foo，那就无能为力了          

13 类的方法第一个参数必须是self，而静态方法第一个参数必须是cls   

## 七 编码建议
1 编码中考虑到其他python实现的效率等问题，比如运算符`+`在CPython（Python）中效率很高，但JPython中却非常低，所以应该采用`.join()`的方式     
2 尽可能使用`‘is’‘is not’`取代`==`，比如`if x is not None`要优于`if x`       
3 使用基于类的异常，每个模块或包都有自己的异常类，此异常类继承自Exception      
4 异常中不要使用裸露的except，except后跟具体的exceptions     
5 异常中try的代码尽可能少。比如：     
```Python
try:
value = collection[key]
except KeyError:
return key_not_found(key)
else:
return handle_value(value)
```
要优于     
```Python
try:
# Too broad!
return handle_value(collection[key])
except KeyError:
# Will also catch KeyError raised by handle_value()
return key_not_found(key)
```

6 使用`startswith()` and `endswith()`代替切片进行序列前缀或后缀的检查, 如     
```
Yes: if foo.startswith(‘bar’):优于
No:  if foo[:3] == ‘bar’:
```

7 使用isinstance()比较对象的类型, 如     
```
Yes: if isinstance(obj, int):  
No: if type(obj) is type(1):
```
8 判断序列空或不空，有如下规则     
```
Yes: if not seq:
if seq:
优于
No: if len(seq)
if not len(seq)
```
9 字符串不要以空格收尾       
10 二进制数据判断使用` if boolvalue`的方式         
