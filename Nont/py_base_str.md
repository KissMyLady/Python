数据类型--字符串
====

## 1. Python中的基本数据类型?     
Python中有6种标准的对象数据类型, [Python中的数据类型](https://github.com/KissMyLady/Python/blob/master/Nont/py_base_num.md)      
Number, String, List, Tuple, Sets, Dict


## 2. [如何区别可变数据类型和不可变数据类型](https://blog.csdn.net/dan15188387481/article/details/49864613)     
让我们从一句话开始: 一切皆为对象，一切皆为对象的引用     
> 可变数据类型  ：list 和 dict      
> 不可变数据类型：int、 float、 string 和 tuple    
![ScreenShot00-233](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot-00233.jpg)  

![ScreenShot00-234](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot-00234.jpg)  

### 为什么叫不可变?  
当改变赋值时, 原先的对象一定要被丢弃, 然后在内存中再创造一个新对象   
* 变就意味着丢弃原先的数据, 所以叫不可变   
* python中的不可变数据类型，不允许变量的值发生变化  

如果改变了变量的值，相当于是新建了一个对象，而对于相同的值的对象，在内存中则只有一个对象，内部会有一个引用计数来记录有多少个变量引用这个对象   

### 可变数据类型:  
允许变量的值发生变化，即如果对变量进行append、`+=`等这种操作后，只是改变了变量的值，而不会新建一个对象，变量引用的对象的地址也不会变化  
![ScreenShot-00235](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot-00235.jpg)  
不过对于相同的值的不同对象，在内存中则会存在不同的对象，即每个对象都有自己的地址，相当于内存中对于同值的对象保存了多份，这里不存在引用计数，是实实在在的对象   
[列表List与元祖Tuple](https://github.com/KissMyLady/Python/blob/master/Nont/py_base_listtrup.md)  
[Python小数据池，代码块深入剖析](https://www.cnblogs.com/jin-xin/articles/9439483.html)  


## 3.将"hello world"转换为首字母大写"Hello World"  
#### 第一种方法: 直接换  
```Python
a = "hello world"
new_str = ''
for i in a:
    if i == 'h' or i == 'w':
        c = i.upper()
        new_str += c
    else:
        new_str += i
print(new_str)

```
#### 第二种方法: 列表索引  
```Python
a = "hello world"
b = a.split()
a1 = b[0][0]
a2 = b[1][0]

new_str = ''
for i in a:
    if i == '{}'.format(a1) or i == '{}'.format(a2):
        c = i.upper()
        new_str += c
    else:
        new_str += i
print(new_str)
```
#### 第三种方法: capitalize方法       
```Python
a = "hello world"
b = a.split()
new_str = ''

for i in b:
    new_str += i.capitalize()
    new_str += ' '
print(new_str)
```
#### 第四种方法: 切 片      
```Python
a = "hello world"
new_str = ''
for s in a.split():
    c = s[:1].upper() + s[1:].lower()
    new_str += c
    new_str += ' '
print(new_str)
```


## 4. 如何检测字符串中只含有数字 ?    
第一种方法:   
```Python
a = '人生苦短, 我用python'
b = '13488885685'
c = 'Big brother is watching you'

import re
for i in [a, b, c]:
    try:
        c = re.match(r'[0-9].*', i)
        print('匹配的结果是:', c.group())
    except:
        print('对不起, 这个字符串不全是数字')
```
第二种方法: 使用列表成员判断   
```Python
a = '人生苦短, 我用python'
b = '13488885685'
c = 'Big brother is watching you'

list_dict = ['0','1','2','3','4','5','6','7','8','9']
for new_srt in [a, b, c]:
    lens = len(new_srt)
    n = 1
    for i in new_srt:
        if i not in list_dict:
            print('这个字符串: {} 不是'.format(new_srt))
            break
        elif lens == n:
            print('这个字符串{}是全数字'.format(new_srt))
        n +=1
```

## 5. 将字符串"ilovechina"进行反转  
第一种方法: pop   
```
a = "ilovechina"
new_str = list(a)

new = ''
for i in range(len(a)):
    c = new_str.pop()
    new += c
    
print(new)
```
第二种方法:  
```Python
a = "ilovechina"
new_str = list()

for i in a:
    new_str.insert(0, i)
    
new = ''
for y in new_str:
    new += y
print(new)
```
第三种方法:  
```Python
class Stack(object):
    def __init__(self):
        self.items = list()

    def is_empty(self):
        return self.items == []
	
    def push(self, item):
        self.items.append(item)

    def pop(self):
        return self.items.pop()
	
    def peek(self):
        last = len(self.items)-1
        return self.items[last]
	
    def size(self):
        return len(self.items)

s = Stack()
for i in 'hello world':
    s.push(i)
	
new_str = ''
for i in range(s.size()):
    new_str += s.pop()
	
print(new_str)
```


## 6. 有一个字符串开头和末尾都有空格    
比如“ adabdw ”, 要求写一个函数把这个字符串的前后空格都去掉    
第一种方法, str自带函数  
```Python
def main(output_set):
    print(output_set.strip())

if __name__ == '__main__':
    a = "  ilovechina  "
    main(a)
```
第二种方法:  if判断   
```
a = "  ilovechina  "
new_str = ''
for i in a:
    if i == ' ':
        pass
    else:
        new_str +=i
print(new_str)
```


## 7. 获取字符串'123456'最后的两个字符   
第一种方法: 
```
a= '123456'
print(a[-2:-1])
```

## 8. 一个编码为 GBK的字符串S，要将其转成UTF-8编码的字符串，应如何操作？  
```Python
c = 's'
utf_8 = c.decode('utf-8')
```

## 9. Re
(1)s="info：xiaoZhang 33 shandong"，用正则切分字符串输出['info', 'xiaoZhang', '33', 'shandong']

(2) a = "你好 中国 "，去除多余空格只留一个空格。
Re匹配使用:   
```Python
import re
a = "info xiaoZhang 33 shandong"
b = "你好 中国 "

c = re.match(r'([0-9a-zA-Z].*)', a)
new = c.group()
print(new)

```
str内置strip方法使用   
```Python 
a = "你好 中国 "
c= a.strip()
print(c)
```


