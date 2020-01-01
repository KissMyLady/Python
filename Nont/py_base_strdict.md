字符串与字典
====


## 字符串的基本操作  
Python中的转义字符     
`\ `   (在行尾时)续行符   
`\a`	响铃   
`\b`	退格(Backspace)   
`\e`	转义     
`\000`	空    
`\n`	换行   
`\v`	纵向制表符   
`\t`	横向制表符   
`\r`	回车   
`\f`	换页   
`\oyy`	八进制数，yy代表的字符，例如：\o12代表换行  
`\xyy`	十六进制数，yy代表的字符，例如：\x0a代表换行  
`\other` 其它的字符以普通格式输出    

### Python字符串运算符
`a = Hello`,  `b = Python`   
基本与通用方法一致   
r/R	原始字符串 - 原始字符串：所有的字符串都是直接按照字面的意思来使用，没有转义特殊或不能打印的字符。   
原始字符串除在字符串的第一个引号前加上字母"r"（可以大小写）以外，与普通字符串有着几乎完全相同的语法。	  
`print(r'\n')` 输出 `\n`  
`print(R'\n')` 输出 `\n`  

## 字符串的格式化  
将一个值插入到一个有字符串格式符`%s`的字符串中     
`print("My name is %s and weight is %d kg!" % ('Lee', 21))`   
输出: `My name is Lee and weight is 21 kg!`   

常用高频方法:  
### 1. `%f`方法  
![ScreenShot00-220](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00220.jpg)    

### 2. `%d`方法: 格式化整数   

### 3. `%s`方法: 格式化字符串  

### 4. 偏方  
在Python3.6开始, 引入了一种新字符串: `_f-srting_`格式化字符串  
例子:   
![ScreenShot00-221](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00221.jpg)   
替换字段是表达式, 在运行时计算, 然后使用format()协议格式化  



## 字符串的一些方法  
### 1.find() 
找str, 返回的是索引最左端地址   
里面三参数: 1. 要找的str  2.起始地址.  3. 终点    
   
### 2.join() 
常用地方: 找路径  
![ScreenShot00-222](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00222.jpg)    

### 3.lower() : 将所有大写转小写   

### 4.upper() : 将所有小写转大写    

### 5.swapcase()  : 大小写置换  

### 6.replace()   
爬虫中简单数据清洗的常用方法         
![ScreenShot00-223](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00223.jpg)     
在`this`后面可加数字, 指定替换多少次

### 7.split()  
爬虫中简单数据清洗的常用方法   
join的逆向方法  
![ScreenShot00-224](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00224.jpg)     
可以看到, 如果加入指定条件, 就按指定的来, 默认切片就是空格  

### 8.strip()  
移除字符串头和尾的空格, 同上, 可以按指定的符号来     

### 9. translate()  
![ScreenShot00-225](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00225.jpg)      
这个东西我想密码学用的会很多, 二战期间德国人发明的英格玛机就是采用的这种字母对应加密方式   
[阿兰图灵破解英格玛机](https://github.com/KissMyLady/Computer/blob/master/Note/early_com3.md)    
[密码学--移位加密](https://github.com/KissMyLady/Computer/blob/master/Note/Noteworks_of_password.md)  

字  典  
====
dict的实质是用空间换取时间   
1. 处理速度极快, 不会随着数据量变大而变慢  
2. 占用大量内存, 浪费多  

字典的格式化   
![ScreenShot00-226](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00226.jpg)   


## 字典的方法 
### 1.clear()   
清空字典, 但是不会删除字典    

### 2.copy()  : 属于浅拷贝     

### 3.fromkeys()   
引用创建新字典   
![ScreenShot00-227](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00227.jpg)    

### 4. get()     
`dict.get('key')`, 查找键, 没有返回None       

### 5.items()  
![ScreenShot00-228](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00228.jpg)    
返回一个可迭代对象  
![ScreenShot00-229](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00229.jpg)   

### 7.keys()      
dict.keys()
![ScreenShot00-230](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00230.jpg)    
里面不传参  

### 8.setdefault()   
![ScreenShot00-231](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00231.jpg)  
同get方法, 如果没有就更新, value默认为None   

### 9.update()    
合并字典  
![ScreenShot00-232](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00232.jpg)    

### 10.values()     
同keys, 返回所有values值    

