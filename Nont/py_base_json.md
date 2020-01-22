JSON的序列化
=========

相关知识引导说明:    
01. 序列化和反序列化:     
序列化:  将 `字典`或者`数组`等OC对象 转换成`二进制数据`准备发送给服务器     
反序列化:  从服务器接收到`二进制数据`转换成`字典`或者`数组`等OC对象      

02. 什么是Json:    
* 1. JavaScript Object Notation，`数据交换格式`   
* 2. JSON字符集必须是UTF-8，表示多语言就没有问题了。
* 3. 为了统一解析，JSON的字符串规定必须用双引号`”“`，Object的键也必须用双引号`”“`     
* 4. 一种轻量级的数据交换格式，它是JavaScript的子集，易于人阅读和编写。
![ScreenShot-00335](https://github.com/KissMyLady/Python/blob/master/Img/json/ScreenShot-00335.jpg)   


03. json中常用的方法:     
`json.dumps()`: 将 Python 对象编码成 JSON 字符串    
`json.loads()`: 将已编码的 JSON 字符串解码为 Python 对象   
`json.dump()` : 将Python内置类型序列化为json对象后写入文件   
`json.load()` : 读取文件中json形式的字符串元素转化为Python类型   



把任何JavaScript对象变成json，就是把这个对象序列化成一个JSON格式的字符串, 这样才能够通过网络传递给其他计算机   

#### 重 点: 如果我们收到一个JSON格式的字符串，只需要把它反序列化成一个JavaScript对象，就可以在JavaScript中直接使用这个对象了     


不同的编程语言有不同的数据类型; 比如说:
1. Python的数据类型有(dict、list、string、int、float、bool、None) 请注意原作者有写long, 但我删除了它, 因为在python3中没有这个数据类型了   
2. Java的数据类型有(bool、char、byte、short、int、long、float、double)     
3. C的数据类型有(bit、bool、char、int、short、long、unsigned、double、float)     
4. Tcl的数据类型(int、bool、float、string)     
5. Ruby的数据类型(Number、String、Ranges、Symbols、true、false、Array、Hash)     
...   
他们的共同特点是，都有字符串类型！

所以要实现不同的编程语言之间`对象的传递`，就必须把对象`序列化`为`标准格式`，比如XML，但更好的方法是序列化为JSON   
 
因为JSON表示出来就是一个字符串，可以被所有语言读取，也可以方便地存储到磁盘或者通过网络传输   

JSON不仅是标准格式，并且比XML更快，而且可以直接在Web页面中读取，非常方便   
JSON类型-----Python类型实例 
`{}`-----dict` 
`[]`-----list`  
`"string"`-----str` 
`1234.56`-----int或float` 
`true`------`True`
`false`-----`False`
`null`------`None` 
 
Python类型抽象-----JSON类型抽象    
`dict`-----object 
`list, tuple`------array 
`str, unicode`-----string 
`int, long, float`-----number 
`True`------true
`False`-----false 
`None`------null 


Python内置的json模块提供了非常完善的Python对象到JSON格式的转换   

`json.dumps()`: 将Python中的对象转换为JSON中的字符串对象   
`json.loads()`: 将JSON中的字符串对象转换为Python中的对象   

先看, 把Py对象变成一个Json, 转换后的Json对象，最后都是字符串型     
![ScreenShot-00334](https://github.com/KissMyLady/Python/blob/master/Img/json/ScreenShot-00334.jpg)  
```Python
In [1]: import json
In [1]: import json

In [2]: py_obj = {'name':'Tom', 'age':30}

In [3]: js_obj = json.dumps(py_obj)

In [4]: js_obj
Out[4]: '{"name": "Tom", "age": 30}'

In [5]: type(js_obj)
Out[5]: str

In [6]: py_obj2 = [1,2,3,4,5]

In [7]: js_obj2 = json.dumps(py_obj2)

In [8]: js_obj2; type(js_obj2)
Out[8]: str

In [9]: js_obj2
Out[9]: '[1, 2, 3, 4, 5]'

In [10]: py_obj3 = True

In [11]: js_obj3 = json.dumps(py_obj3)

In [12]: js_obj3
Out[12]: 'true'
```

## [类转换](https://blog.csdn.net/Jerry_1126/article/details/76409042)
但是如果是类，是不是可以可以直接用json.dumps(obj)来处理呢？ 比如这个:   
```Python
import json
class OneMan(object):
    def __init__(self, name, age):
        self.name = name
        self.age = age
		
tom = OneMan('Tom', 22)
print(json.dumps(tom))
```
This is a Error: 
```
raise TypeError(f'Object of type {o.__class__.__name__} '  
TypeError: Object of type OneMan is not JSON serializable   
```
se ria li zable: 可序列化      
错误的原因是: 对象`不是一个可序列化为JSON的对象`        

如果连class的实例对象都无法序列化为JSON，这肯定不合理！   

我们仔细看看dumps()方法的参数列表，可以发现，除了第一个必须的obj参数外, dumps()方法还提供了一大堆的可选参数：   
help(json.dumps)   
```Python
def dumps(obj, *, skipkeys=False, ensure_ascii=True, check_circular=True,
        allow_nan=True, cls=None, indent=None, separators=None,
        default=None, sort_keys=False, **kw):
```
| :---: | --- |
| 函数作用:       | 将Python的对象转变成JSON对象|
| skipkeys:      | 如果为True的话，则只能是字典对象，否则会TypeError错误, 默认False|
| ensure_ascii:  | 确定是否为ASCII编码|
| check_circular:| 循环类型检查，如果为True的话|
| allow_nan:     | 确定是否为允许的值|
| indent:        | 会以美观的方式来打印，呈现|
| separators:    | 对象分隔符，默认为, |
| encoding:      | 编码方式,默认为utf-8   |  
| sort_keys:     | 如果是字典对象，选择True的话，会按照键的ASCII码来排序|    


这些可选参数就是让我们来定制JSON序列化。 前面的代码之所以无法把Man类实例序列化为JSON     
#### 原因: 默认情况下，dumps()方法不知道如何将Man实例变为一个JSON的{}对象    

可选参数`default`就是把任意一个对象变成一个可序列为JSON的对象，
#### 办法1: `我们只需要为Man专门写一个转换函数，再把函数传进去即可`:  
```Python
import json

class OneMan(object):
    def __init__(self, name, age):
        self.name = name
        self.age = age
		
def TwoChange(obj):
    return {
        "name": obj.name,
        "age": obj.age}

o = OneMan('Tom', 22)
print(json.dumps(o, default=TwoChange))
```
输出内容:  
```
{"name": "Tom", "age": 22}
```

#### 办法2: 者通过一种简单的方式，用lambda方式来转换任意一个类对象为JSON形式:
```Python
import json

class TwoMan(object):
    def __init__(self, name, age):
        self.name = name
        self.age = age

t = TwoMan('Jack', 22)
print(json.dumps(t, default  = lambda obj: obj.__dict__,  # 将任意的对象，转换成字典的方式
	                sort_keys= True, # 按照字典中的键来按照ASCII方式来排序
	                indent   = 4 ))  # 按照键值对以间隔4来直观的显示
```

## 反序列化  
同样的道理，如果要将`Json对象`反序列化，也可以写个函数来转换:     
```Python
import json

class Three(object):
    def __init__(self, name, age):
        self.name = name
        self.age = age
		
json_str = '{"age":22, "name":"Dome"}'

def handle(someone):
    return Three(someone['name'], someone['age'])

m = json.loads(json_str, object_hook=handle)

print(m)
print(m.name)
print(m.age)
```
输出结果:   
```Python
<__main__.Three object at 0x04F0CB38>
Dome
22
```


常见问题  
## 1. Json转中文时乱码: 
```Python
import json

data = [{
    "name": "Tom",
    "gender": "male"
}, {
    "name": "杰克",
    "gender": "男"
}]

#将json格式转为字符串
print(type(data))
str = json.dumps(data, indent=2)  # indent=2按照缩进格式
print(type(str))
print(str)

content = json.dumps(data, indent=2, ensure_ascii=False)
print('><'*20)
print(content)
print('><'*20)

# 存json格式文件
# with open('data.json', 'w', encoding='utf-8') as f:
#     f.write(json.dumps(data, indent=2, ensure_ascii=False))  # ensure_ascii=False可消除json包含中文的乱码问题
```
