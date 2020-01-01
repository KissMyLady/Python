Python中的数据类型   
====
Python中有6种标准对象类型:  
> 1. Number,  2. String,  3. List,  4. Tuple,  5. Sets,  6. Dict    
  
## Number  
### 1. int
![ScreenShot00-177](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00177.jpg)   

### 2. float
![int-1](https://github.com/KissMyLady/Python/blob/master/Img/int-1.jpg)  

### 3. complex
知识描述:   
> complex() 函数用于创建一个值为`real + imag * j`的复数或者转化一个字符串或数为复数。 如果第一个参数为字符串，则不需要指定第二个参数    
![ScreenShot00-178](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00178.jpg)  

### 4. 常量与变量 
![ScreenShot00-179](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00179.jpg)    

Python有两个比较常见的常量: PI和E  
![ScreenShot00-180](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00180.jpg)  

### 5. 关键字(保留字)  
在Python中的保留字, 这些保留字不能用作常数或变数，或任何其他标识符名称   
所有 Python的关键字只包含小写字母   
![ScreenShot00-181](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00181.jpg)  

## 常见Python类型转换知识描述
[整理来源菜鸟教程--点击进入](https://www.runoob.com/python/python-variable-types.html)        
* int(x [,base]):   将x转换为一个整数    
* long(x [,base] ): 将x转换为一个长整数  
* float(x):  将x转换到一个浮点数   
* complex(real [,imag]):  创建一个复数  

* repr(x):  将对象 x 转换为表达式字符串  
* eval(str): 用来计算在字符串中的有效Python表达式,并返回一个对象   

* str(x):   将对象 x 转换为字符串  
* tuple(s): 将序列 s 转换为一个元组  
* list(s):  将序列 s 转换为一个列表  
* set(s):   转换为可变集合  
* dict(d):  创建一个字典, d 必须是一个序列 (key,value)元组    
* frozenset(s):  转换为不可变集合   

* chr(x):  将一个整数转换为一个字符    
* unichr(x):  将一个整数转换为Unicode字符      
* ord(x):  将一个字符转换为它的整数值     
* hex(x):  将一个整数转换为一个16进制字符串  
* oct(x):  将一个整数转换为一个8进制字符串  


Python中的运算符和操作对象    
====
### 算数运算符     
* `+`  :加 - 两个对象相加	  
** `a + b` 输出结果 30  

* `-`  :减 - 得到负数或是一个数减去另一个数	    
** `a - b` 输出结果 -10  
  
*  `*` :乘 - 两个数相乘或是返回一个被重复若干次的字符串  	
** `a * b` 输出结果 200  

* `/`  :除 - x除以y	
** `b / a` 输出结果 2    

* `%`  :取模 - 返回除法的余数	  
** `b % a` 输出结果 0    

* `**`  :幂 - 返回x的y次幂	  
** `a**b` 为10的20次方， 输出结果 100000000000000000000  

* `//`  :取整除 - 返回商的整数部分（向下取整）       
** `9//2`  : `4`      
** `-9//2` : `-5`     

  
### 比较运算符   
这个比较简单, 直接给例子就可以理解了    
`a == b` 返回 False  
`a != b` 返回 true  
`a <> b` 返回 true, 这个运算符类似`!=`  
注意:  在很多程序中, 这个不怎么用    
![ScreenShot00-182](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00182.jpg)  
`a > b`  返回 False    
`a < b`  返回 true    
`a >= b` 返回 False  
`a <= b` 返回 true  

### 赋值运算符  
这也容易理解, 直接给例子  
`c = a + b`  `a + b` 的运算结果赋值为 `c`
`c += a` 等效于 `c = c + a`    
`c -= a` 等效于 `c = c - a`   
`c *= a` 等效于 `c = c * a`   
`c /= a` 等效于 `c = c / a`   
`c %= a` 等效于 `c = c % a`   
`c **= a` 等效于 `c = c ** a`   
`c //= a` 等效于 `c = c // a`   
注 意:  
区分C语言的自增运算, Python的赋值是容易理解的    
[关于自增自减运算符的一些问题](https://blog.csdn.net/lianghui0811/article/details/48736109)   
[++自增与--自减](https://blog.csdn.net/sunxiwang/article/details/78553933)      
  
### 位运运算符     
按位运算符是把数字看作二进制来进行计算       
[菜鸟教程--点击进入](https://www.runoob.com/python/python-operators.html)          
很多教程, 市面上针对基础的书都基本一样,  互相借鉴, 连数字都没改,  菜鸟教程应该是范文          
我们让`a = 60`,  `b = 13`    
![ScreenShot00-183](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00183.jpg)      
![ScreenShot00-184](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00184.jpg)  
> `a = 0011 1100` 
> `b = 0000 1101`  
-----------------  
`a&b = 0000 1100` :如果都为1, 则该位的结果为1, 否则为0    

`a|b = 0011 1101` :只要对应的二个二进位有一个为1时，结果位就为1    

`a^b = 0011 0001` :当两对应的二进位相异时，结果为1   

`~a  = 1100 0011` :对数据的每个二进制位取反, 即把1变为0,把0变为1    
![ScreenShot00-185](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00185.jpg)  

`a << 2 == 240`   :二进位全部左移`1111 0000` ,高位丢弃，低位补0   

`a >> 2 == 15`   :二进位全部右移`0000 1111`    

### 逻辑运算符  
`a and b` :返回 20      
`a or b`  :返回 10      
`not(a and b` :返回 False   
![ScreenShot00-186](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00186.jpg)    
实际在判断中用的多, 用if语句来配合`and or not`判断条件与否      

### 身份运算符    
`is`与 `==`区别:    
> `is`用于判断两个变量引用对象是否为同一个(同一块内存空间),  `==`用于判断引用变量的值是否相等     
![ScreenShot00-187](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00187.jpg)    

### 成员运算符   
`in`和`not in`     
![ScreenShot00-188](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00188.jpg)  

### 优先级  
1. `**`     
2. `~ + -`    
3. `* / % //`    
4. `+ -`  
5. `>> <<`	    
6. `&`    
7. `^ |`   
8. `<= < > >=`    
9. `<> == !=`  
10. `= %= /= //= -= += *= **=`    
11. `is is not`	    
12. `in not in`	    
13. `not and or`	  



## Python标识符    
1. Python里，标识符由字母、数字、下划线组成   
2. Python中，所有标识符可以包括英文、数字以及下划线(_)，但不能以数字开头   
3. 区分大小写的。  
4. 以下划线开头的标识符是有特殊意义的。
> 以单下划线开头 _foo 的代表不能直接访问的类属性，需通过类提供的接口进行访问，不能用 from xxx import * 而导入   
> 以双下划线开头的 __foo 代表类的私有成员  
> 以双下划线开头和结尾的 __foo__ 代表 Python 里特殊方法专用的标识，如 __init__() 代表类的构造函数  
  
5. Python 可以同一行显示多条语句，方法是用分号 ; 分开，如：    
```Python
>>> print ('hello');print ('runoob');
hello
runoob
```


