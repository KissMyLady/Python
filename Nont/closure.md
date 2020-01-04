闭包的概念  
=====

## 我们先来看一个小例子:  
```Python
a, b = 1, 2
print(id(a), id(b))

def line1(x):
    print('函数line1: ',id(a), id(b), a * x + b)

line1(2)
print(a)
```   
#### 问题一:  a, b并未在函数导入, 这样执行会不会有毛病?   
#### 问题二:  a, b地址在函数内部会不会发生什么变化?  
输出:   
```
140715192980288 140715192980320
函数line1:  140715192980288 140715192980320 4
1
```
我们会发现:  
#### 1. a, b在函数内部导入了, 并且没毛病  
#### 2. a, b在函数内部与在函数外部id地址相同, 说明python这里引用的是同一个对象  

究竟想说什么 ?  
#### 1. a, b是全局变量   
等等, a, b没有加global怎么变成了全局变量?  
* 因为a, b为[不可变数据类型](https://github.com/KissMyLady/Python/blob/master/Nont/py_base_str.md)      
>  让我们从一句话开始: 一切皆为对象，一切皆为对象的引用  
> 可变数据类型 ：list 和dict  
> 不可变数据类型：int、 float、 string 和 tuple  

#### 2. 函数内部引用不可变数据类型的全局变量没问题, 但修改就有问题  
像这样:  
```Python
a, b = 1, 2
print(id(a), id(b))

def line1(x):
    a += 1
    print('函数line1: ',id(a), id(b), a * x + b)

line1(2)
print(a)
```
我们在函数内部定义了赋值, 这里会报错:     
> 赋值之前引用了局部变量a   
在函数内部, a并未被定义, 所以这里错误  

## 闭  包  
什么是闭包, 我们先看一个实例:   
```Python
def line_6(k, b):
    def create_y(x):
        print(k*x + b)
    return create_y

line_6_1 = line_6(1, 2)

line_6_1(0)
line_6_1(2)
line_6_1(4)
```
定 义:  
#### 我们把这种函数内部定义函数, 且函数引用了外部函数变量, 将这个函数以及用到的变量叫`闭包`     
事实上, 我们有多种办法可以实现上面传递的参数并保存的功能:   
1. 其中一种就是面向对象   
```Python
class Get(object):
    def __init__(self, a, b):
        self.a = a
        self.b = b

    def method(self, x):
        print(self.a*x + self.b)

    def __call__(self, x):
        print(self.a*x  + self.b)

b = Get(2, 5)
# b.method(5)
# b.method(8)
b(5)
b(10)
```
任务可以实现, 但这是其中最浪费资源的创建对象保存值方法      
### 看下闭包里的细节:   
```Python
def line6(a, b):
    pass

c = line6(7, 8)
print(c)
```
打印: `None`
```Python
def line6(a, b):
    def create(x):
        pass
    return create
c = line6(7, 8)
print(c)
```
打印: `<function line6.<locals>.create at 0x0000026BF78C4400>`   
可以看到, 我们打印c的值, 它指向了`def create`函数   

像c语言里面, 只有函数, 没有类, 没有匿名,等等   
但Python更任意, 更灵活, 问题来了:  
## Python中的类, 匿名, 函数, 各有什么特点?  
#### 1. 函数   
函数就是一坨代码, 他不会数据传过去
它们封装功能, 通过函数名就可以调用 


#### 2. [匿名函数](https://www.cnblogs.com/xiao-apple36/p/8577727.html)       
匿名函数也是函数, 可以封装一部分代码, 可以想到, Python中已经有了函数为什么还要有匿名函数?  
因为简单,  能够完成小功能的编写, 非常方便    
```Python
f = lambda a,b,c:a+b+c

t = lambda : True

c = lambda x,y,z: x*y*z
c(2,3,4)

(lambda x, y: x if x> y else y)(101,102)
```
![ScreenShot-00253]()  

#### 3. 闭包  
比函数要高端,  不仅可以给代码, 还可以给代码要用到的数据   
通过闭包, 我们可以只传需要的一部分数据,  而且里面有执行的代码  

#### 4. 对象  
功能庞大, 数据全, 但有些功能我们不需要     
 
其他存在语言: Js, java也有 


装饰器的正确打开方式      
====
## 装饰器实例1--刷新:    
```Python
@retry(stop_max_attempt_number=5, wait_fixed=60)
def get_response(input_url, Referer):
    data = (requests.get(input_url, headers=heade(Referer))).content.decode()
    response = etree.HTML(data)
    return response
```
例如这段爬虫代码, 请求函数, 通过请求url, 获得response   
但是, 很多时候, 因为网速, 因为服务器打开资源错误, 导致这个数据一次性打不开, 而再次试图请求的时候是有很大几率能成功的  
就像我们打开一个网页,  有时候得刷新几次才能打开一个网页   

我们看看这段代码:   
```Python
@retry(stop_max_attempt_number=5, wait_fixed=60)
```
通过`@`一个名字, 就可以起到装饰的作用, 这里作用: 如果请求不到数据, 就重新请求, 每次间隔60s   

## 装饰器实例2--路由:    
```Python
URL_FUNC_DICT = dict()
def route(url):
    def set_func(func):
        URL_FUNC_DICT[url] = func
        def call_func(*args, **kwargs):
            return func(*args, **kwargs)
        return call_func
    return set_func

@route('/index.py')
def index():
    with open('./index.html', 'r', encoding='utf-8') as f:
        return f.read()
```
这是装饰器在Web网络框架中的具体应用   
我们再看看如下代码:  
```Python
def index():
    with open('./templates/index.html','r',encoding='utf-8') as  f:
        return f.read()

def login():
    with open('./templates/center.html', 'r', encoding='utf-8') as  f:
        return f.read()

def application(env, start_response):
    start_response('200 OK', [('Content-Type', 'text/html;charset=utf-8')])
    file_name = env['PATH_INFO']
    # file_name = "/index.py"
    if file_name == "/index.py":
        return index()
    elif file_name == "/center.py":
        return login()
    else:
        return '404 Not Found'
```
这里写了两个返回网页的函数, 加一个WSGI接口   
当网页数量上千, 上万时, 你肯定不希望手写一千, 一万次的if-elif语句    

于是, 我们使用字典传递了该调用什么函数  
```Python
...
env = dict()
env['PATH_INFO'] = file_name
body = self.application(env, self.set_response_header)
...

URL_FUNC_DICT = {
    "/index.py":index,
    "/center.py":center
}
def application(env, start_response):
    start_response('200 OK', [('Content-Type', 'text/html;charset=utf-8')])
    file_name = env['PATH_INFO']
    
    func = URL_FUNC_DICT[file_name]
    return func()
```
这样, 就不用写if-else,  但是, 我我们仍需要手动在字典添加`"/center.py":center`像这样的说明  

## 更好的办法?  
```Python
URL_FUNC_DICT = dict()

def route(url):
    def set_func(func):
        URL_FUNC_DICT[url] = func
        def call_func(*args, **kwargs):
            return func(*args, **kwargs)
        return call_func
    return set_func

@route('/index.html')
def index():
    with open('./index.html','r',encoding='utf-8') as f:
        return f.read()

def application(env, start_response):
    start_response('200 OK', [('Content-Type', 'text/html;charset=utf-8')])
    file_name = env['PATH_INFO']
    return URL_FUNC_DICT[file_name]()
```
这就是服务器中路由的由来     

## 细节步骤  
#### 1. 当执行`.py`时, 装饰器先执行获取`索引`, 将`@route('/yyy.html')`中的`/yyy.html`放入字典  
```
def route(url):
    def set_func(func):
        URL_FUNC_DICT[url] = func
    return set_func
```


### 怎么放入字典的?  
```
def rout('/index.html')
    def set_func(func):
        URL_FUNC_DICT[url] = func
    return set_func
```
#### 1. 执行`rout`函数. 请注意: 装饰器在文件导入就会执行, 而不是等到被装饰函数执行才执行  
#### 2. 中间函数跳过, 不执行     
#### 3. 执行到: return `set_func`     
#### 4. 跳到 `def set_func(func):` 此时`func = index`   
#### 5. `URL_FUNC_DICT['/index.html'] = index`
#### 6. 
``` Python
def call_func(*args, **kwargs):
        return func(*args, **kwargs)
    return call_func
```
#### 7. 返回`func()`

#### 核心细节:  
这里属于装饰器的设置外部变量, 比较有挑战, 希望多看几遍, 不理解也最好背下来  

装饰器一般不带参数, 但是带参数的装饰器功能更强大, 因为可以更加灵活调整装饰功能, 像上面的爬虫装饰器一样, 通过调整参数可以得到不同的效果  

于是, 这里有结论:  
## 通用装饰器与通用带参数的装饰器
``` Python
def lv_1(faciont_output):
    lv_2(*args, **kwargs):
        print('The func in a hat')
        return faciont_output(*args, **kwargs)
    return lv_2(*args, **kwagrs)
```

## 高级装饰器: 设置外部变量  
```Python
def lv_1(date):
    def lv_2(func):
        def lv_3():
            print('The func in a hat ', date)
            return func
        return lv_3
    return lv_2
```
```Python
@lv_1('This is my decorator')
def Mylady():
    print('Kiss My Lady')
```


闭 包
====

## 1. 函数引用  
```Python
def test1():
    print("--- in test1 func----")

# 调用函数
test1()

# 引用函数
ret = test1

print(id(ret))
print(id(test1))

#通过引用调用函数
ret()
```
运行结果:
Python
```Python
--- in test1 func----
140212571149040
140212571149040
--- in test1 func----
````

## 2. 什么是闭包  

> 在函数内部再定义一个函数，并且这个函数用到了外边函数的变量，那么将这个函数以及用到的一些变量称之为闭包  
# 定义一个函数
```Python
def test(number):

    # 在函数内部再定义一个函数，并且这个函数用到了外边函数的变量，那么将这个函数以及用到的一些变量称之为闭包
    def test_in(number_in):
        print("in test_in 函数, number_in is %d" % number_in)
        return number+number_in
    # 其实这里返回的就是闭包的结果
    return test_in


# 给test函数赋值，这个20就是给参数number
ret = test(20)

# 注意这里的100其实给参数number_in
print(ret(100))

#注 意这里的200其实给参数number_in
print(ret(200))
```

运行结果：
```Python
in test_in 函数, number_in is 100
120

in test_in 函数, number_in is 200
220


## 3. 看一个闭包的实际例子：  
def line_conf(a, b):
    def line(x):
        return a*x + b
    return line

line1 = line_conf(1, 1)
line2 = line_conf(4, 5)
print(line1(5))
print(line2(5))
```
这个例子中，函数line与变量a,b构成闭包。在创建闭包的时候，我们通过line_conf的参数a,b说明了这两个变量的取值，  
这样，我们就确定了函数的最终形式(y = x + 1和y = 4x + 5)。我们只需要变换参数a,b，就可以获得不同的直线表达函数。  
由此，我们可以看到，闭包也具有提高代码可复用性的作用。  

如果没有闭包，我们需要每次创建直线函数的时候同时说明a,b,x。  
这样，我们就需要更多的参数传递，也减少了代码的可移植性。  

注意点:  

由于闭包引用了外部函数的局部变量，则外部函数的局部变量没有及时释放，消耗内存  

## 4. 修改外部函数中的变量  
python3的方法
```Python
def counter(start=0):
    def incr():
        nonlocal start
        start += 1
        return start
    return incr

c1 = counter(5)
print(c1())
print(c1())

c2 = counter(50)
print(c2())
print(c2())

print(c1())
print(c1())

print(c2())
print(c2())
```
python2的方法
```Python
def counter(start=0):
    count=[start]
    def incr():
        count[0] += 1
        return count[0]
    return incr

c1 = closeure.counter(5)
print(c1())  # 6
print(c1())  # 7
c2 = closeure.counter(100)
print(c2())  # 101
print(c2())  # 102
```
 ## 函数，匿名函数，闭包，对象，当做实参时，有什么区别？  
 - 1、匿名函数能够完成基本的简单功能，传递的是函数的应用，只有功能  
 - 2、普通函数能够完成较为复杂的功能，，传递的是这个函数的引用，只有功能  
 - 3、闭包能够完成较为复杂的功能，传递的是这个闭包中的函数以及数据，，因此传递的功能+数据  
 - 4、对象能够完成最为复杂的功能，传递的是很多数据+很多功能， 因此传递的是功能+数据  

装饰器  
====

装饰器是程序开发中经常会用到的一个功能，用好了装饰器，开发效率如虎添翼，  
所以这也是Python面试中必问的问题，但对于好多初次接触这个知识的人来讲，

这个功能有点绕，自学时直接绕过去了，然后问到了就挂了，  
因为装饰器是程序开发的基础知识，这个都不会，别跟人家说你会Python, 看了下面的文章，保证你学会装饰器。  

## 1、先明白这段代码  
```Python
#### 第一波 ####
def foo():
    print('foo')

foo  # 表示是函数
foo()  # 表示执行foo函数

#### 第二波 ####
def foo():
    print('foo')

foo = lambda x: x + 1

foo()  # 执行lambda表达式，而不再是原来的foo函数，
因为foo这个名字被重新指向了另外一个匿名函数
```
函数名仅仅是个变量，只不过指向了定义的函数而已，  
所以才能通过 函数名()调用，如果 函数名=xxx被修改了，那么当在执行 函数名()时，调用的就不知之前的那个函数了  

## 2、需求来了  
初创公司有N个业务部门，基础平台部门负责提供底层的功能，  
如：数据库操作、redis调用、监控API等功能。业务部门使用基础功能时，只需调用基础平台提供的功能即可。如下：  
```Python
##  基础平台提供的功能如下  ##  
def f1():
    print('f1')

def f2():
    print('f2')

def f3():
    print('f3')

def f4():
    print('f4')

## 业务部门A 调用基础平台提供的功能 ##
f1()
f2()
f3()
f4()

## 业务部门B 调用基础平台提供的功能 ##
f1()
f2()
f3()
f4()
```
目前公司有条不紊的进行着，但是，以前基础平台的开发人员在写代码时候没有关注验证相关的问题，  
即：基础平台的提供的功能可以被任何人使用。现在需要对基础平台的所有功能进行重构，为平台提供的所有功能添加验证机制，  
即：执行功能前，先进行验证。  

## 老大把工作交给 Low B，他是这么做的：  
> 跟每个业务部门交涉，每个业务部门自己写代码，调用基础平台的功能之前先验证。  
> 诶，这样一来基础平台就不需要做任何修改了。太棒了，有充足的时间泡妹子...  
当天Low B 被开除了…

## 老大把工作交给 Low BB，他是这么做的：  
```Python
## 基础平台提供的功能如下 ##
def f1():
    # 验证1
    # 验证2
    # 验证3
    print('f1')

def f2():
    # 验证1
    # 验证2
    # 验证3
    print('f2')

def f3():
    # 验证1
    # 验证2
    # 验证3
    print('f3')

def f4():
    # 验证1
    # 验证2
    # 验证3
    print('f4')

###  业务部门不变 ### 
### 业务部门A 调用基础平台提供的功能 ### 
f1()
f2()
f3()
f4()

### 业务部门B 调用基础平台提供的功能 ### 
f1()
f2()
f3()
f4()
```
过了一周 Low BB 被开除了…  

## 老大把工作交给 Low BBB，他是这么做的：   
> 只对基础平台的代码进行重构，其他业务部门无需做任何修改  
```Python
##  基础平台提供的功能如下  ## 
def check_login():
    # 验证1
    # 验证2
    # 验证3
    pass

def f1():
    check_login()
    print('f1')

def f2():
    check_login()
    print('f2')

def f3():
    check_login()
    print('f3')

def f4():
    check_login()
    print('f4')
```
老大看了下Low BBB 的实现，嘴角漏出了一丝的欣慰的笑，语重心长的跟Low BBB聊了个天：  

### 老大说：  
写代码要遵循开放封闭原则，虽然在这个原则是用的面向对象开发，但是也适用于函数式编程，  
简单来说，它规定已经实现的功能代码不允许被修改，但可以被扩展，即：  

- 封闭：已实现的功能代码块  
- 开放：对扩展开发  
如果将开放封闭原则应用在上述需求中，那么就不允许在函数 f1 、f2、f3、f4的内部进行修改代码，  
老板就给了Low BBB一个实现方案：  
```Python
def w1(func):
    def inner():
        # 验证1
        # 验证2
        # 验证3
        func()
    return inner

@w1
def f1():
    print('f1')
@w1
def f2():
    print('f2')
@w1
def f3():
    print('f3')
@w1
def f4():
    print('f4')
```
对于上述代码，也是仅仅对基础平台的代码进行修改，就可以实现在其他人调用函数  
 f1 f2 f3 f4 之前都进行【验证】操作，并且其他业务部门无需做任何操作。    

Low BBB心惊胆战的问了下，这段代码的内部执行原理是什么呢？  

老大正要生气，突然Low BBB的手机掉到地上，恰巧屏保就是Low BBB的女友照片，  
老大一看一紧一抖，喜笑颜开，决定和Low BBB交个好朋友。  
 
详细的开始讲解了：  

单独以f1为例：  
```Python
def w1(func):
    def inner():
        # 验证1
        # 验证2
        # 验证3
        func()
    return inner

@w1
def f1():
    print('f1')
```

python解释器就会从上到下解释代码，步骤如下：  

1、def w1(func): ==>将w1函数加载到内存  
2、@w1
没错， 从表面上看解释器仅仅会解释这两句代码，因为函数在 没有被调用之前其内部代码不会被执行。  

从表面上看解释器着实会执行这两句，
但是 @w1 这一句代码里却有大文章， @函数名 是python的一种语法糖。  

## 上例@w1内部会执行一下操作：  
### 执行w1函数  

> 执行w1函数 ，并将 @w1 下面的函数作为w1函数的参数，即：@w1 等价于 w1(f1) 所以，内部就会去执行：  
```Python
def inner(): 
    #验证 1
    #验证 2
    #验证 3
    f1()       # func是参数，此时 func 等于 f1 
return inner   # 返回的 inner，inner代表的是函数，
               #   非执行函数 ,其实就是将原来的 f1 函数塞进另外一个函数中
```
### w1的返回值  
> 将执行完的w1函数返回值 赋值 给@w1下面的函数的函数名f1 即将w1的返回值再重新赋值给 f1，即：  
```Python
新f1 = def inner(): 
            #验证 1
            #验证 2
            #验证 3
            原来f1()
        return inner
```
> 所以，以后业务部门想要执行 f1 函数时，就会执行 新f1 函数，在新f1 函数内部先执行验证，  
> 再执行原来的f1函数，然后将原来f1 函数的返回值返回给了业务调用者。  

如此一来， 即执行了验证的功能，又执行了原来f1函数的内容，并将原f1函数返回值  返回给业务调用着  
Low BBB 你明白了吗？要是没明白的话，我晚上去你家帮你解决吧！！！  


## 3. 再议装饰器  
### 3.1最简单的装饰器  
```Python    
def funcl():
    print("the day is a fun day today")

def outer():
    print("+++++++++++++++++")
    funcl()   
outer()
```
### 3.2装饰器概念  
```Python    
# 装饰器概念： 是一个闭包，把一个函数当做参数返回一个代替版的函数，
#  本质上就是一个返回函数的函数
def func1():
    print("the day is a good day")

def outer(func):
    print("+++++++++++++++++")
    func()   
    
func1 = outer(func1)
```
### 3.3装饰器本质  
```Python
# 本质是函数的函数
def func1():
    print("the day is a fun day today")

def outer(x):                             #  func1在 outer里面后，  x = func1
    def inner():                          #  定义inner()函数，
        print("+++++++++++++++++")        #     封装功能
        x()                               #  执行x()函数，，也就是执行：func1函数
    return inner()  # 返回inner(化妆)结果  #  返回inner函数的执行情况

# f是函数func1的加强版本   
# ↘负责化妆
f = outer(func1)                          #  对象化装饰结果
f
```
### 3.4加强版装饰器  
```Python
# 稍微复杂装饰器
# 使用@符号将装饰器应用到函数
# @ python2.4支持使用@符号

@outer                          # 相当于 say = outer(say)  
def say(age):
    print("Bonnie is %d years old girl" % (age))
      
# 不需要做任何代码变动的前提下增加额外功能
# 这种参数只能修饰有一个参数的函数，并且不通用
def outer(x):                   # 创建装饰器
    def inner(age):             #   创建函数的函数
        if age < 0:             #      封装
            age = 0             #         
        x(age)                  #    ← 调say函数
    return inner                #   返回 inner

#   ↘装饰器  ↓被装饰对象
# say = outer(say)  

say(-10)
```
### 3.5通用装饰器  
```Python
# 通用装饰器
def outer(func):
    def inner(*args, **kwargs):
        # 添加修饰的功能
        print("+++++++++")
        func(*args, **kwargs)        
    return inner

@outer
def say(name, age):  
    # 函数参数理论上是无限制的，但实际上最好不要超过6到7个
    print("my name is %s, I am %d years old" % (name, age))
    
say("christine",18)
```
### 3.6有return的通用装饰器  
```Python
def set_func(faction_input):
    def call_me(*args, **kwargs):
        print('帽子')
        print('衣服')
        return faction_input(*args, **kwargs)
    return call_me

@set_func
def test1(num, *args, **kwargs):
    print('------test1------%d'% num)
    print('------test1------', args)
    print('------test1------', kwargs)
    return 'ok'

ret = test1(100)
print(ret)
```
## 3.7装饰器使用  
```Python
# 定义函数：完成包裹数据
def makeBold(fn):
    def wrapped():
        return "<b>" + fn() + "</b>"
    return wrapped

# 定义函数：完成包裹数据
def makeItalic(fn):
    def wrapped():
        return "<i>" + fn() + "</i>"
    return wrapped

@makeBold
def test1():
    return "hello world-1"

@makeItalic
def test2():
    return "hello world-2"

@makeBold
@makeItalic
def test3():
    return "hello world-3"

print(test1())
print(test2())
print(test3())
```
Result  
```Pthon
<b>hello world-1</b>
<i>hello world-2</i>
<b><i>hello world-3</i></b>
```

## 4. 装饰器(decorator)功能  
- 1、引入日志
- 2、函数执行时间统计
- 3、执行函数前预备处理
- 4、执行函数后清理功能
- 5、权限校验等场景
- 6、缓存


## 5. 装饰器示例  

## 例1:无参数的函数  
```Python
from time import ctime, sleep

def timefun(func):
    def wrapped_func():
        print("%s called at %s" % (func.__name__, ctime()))
        func()
    return wrapped_func

@timefun
def foo():
    print("I am foo")

foo()
sleep(2)
foo()
```
上面代码理解装饰器执行行为可理解成  
```Pthon
foo = timefun(foo)
# foo先作为参数赋值给func后,foo接收指向timefun返回的wrapped_func
foo()
# 调用foo(),即等价调用wrapped_func()
# 内部函数wrapped_func被引用，所以外部函数的func变量(自由变量)并没有释放
# func里保存的是原foo函数对象
```

## 例2:被装饰的函数有参数  
 ```Python
from time import ctime, sleep
def timefun(func):
    def wrapped_func(a, b):
        print("%s called at %s" % (func.__name__, ctime()))
        print(a, b)
        func(a, b)
    return wrapped_func

@timefun
def foo(a, b):
    print(a+b)

foo(3,5)
sleep(2)
foo(2,4)
 ```
 
## 例3:被装饰的函数有不定长参数  
```Python
from time import ctime, sleep
def timefun(func):
    def wrapped_func(*args, **kwargs):
        print("%s called at %s"%(func.__name__, ctime()))
        func(*args, **kwargs)
    return wrapped_func

@timefun
def foo(a, b, c):
    print(a+b+c)

foo(3,5,7)
sleep(2)
foo(2,4,9)
```

## 例4:装饰器中的return  
```Python
from time import ctime, sleep
def timefun(func):
    def wrapped_func():
        print("%s called at %s" % (func.__name__, ctime()))
        func()
    return wrapped_func

@timefun
def foo():
    print("I am foo")

@timefun
def getInfo():
    return '----hahah---'

foo()
sleep(2)
foo()

print(getInfo())
```
resule  
```Python
foo called at Fri Nov  4 21:55:35 2016
I am foo
foo called at Fri Nov  4 21:55:37 2016
I am foo
getInfo called at Fri Nov  4 21:55:37 2016
None
```
如果修改装饰器为`return func()`，则运行结果：  
```Python
foo called at Fri Nov  4 21:55:57 2016
I am foo
foo called at Fri Nov  4 21:55:59 2016
I am foo
getInfo called at Fri Nov  4 21:55:59 2016
----hahah---
```
总 结：  
- 一般情况下为了让装饰器更通用，可以有return  

## 例5:装饰器带参数,在原有装饰器的基础上，设置外部变量  
```Python
#decorator2.py
from time import ctime, sleep

def timefun_arg(pre="hello"):
    def timefun(func):
        def wrapped_func():
            print("%s called at %s %s" % (func.__name__, ctime(), pre))
            return func()
        return wrapped_func
    return timefun

# 下面的装饰过程
# 1. 调用timefun_arg("itcast")
# 2. 将步骤1得到的返回值，即time_fun返回， 然后time_fun(foo)
# 3. 将time_fun(foo)的结果返回，即wrapped_func
# 4. 让foo = wrapped_fun，即foo现在指向wrapped_func
@timefun_arg("itcast")
def foo():
    print("I am foo")

@timefun_arg("python")
def too():
    print("I am too")

foo()
sleep(2)
foo()

too()
sleep(2)
too()
```
可理解为  
```Python
foo()==timefun_arg("itcast")(foo)()
```

## 例6：类装饰器（扩展，非重点）  
装饰器函数其实是这样一个接口约束，它必须接受一个callable对象作为参数，  
然后返回一个callable对象。在Python中一般callable对象都是函数，但也有例外。  
只要某个对象重写了 __call__() 方法，那么这个对象就是callable的。  
```Python
class Test():
    def __call__(self):
        print('call me!')

t = Test()
t()  # call me
```
类装饰器demo  
```Python
class Test(object):
    def __init__(self, func):
        print("---初始化---")
        print("func name is %s"%func.__name__)
        self.__func = func
    def __call__(self):
        print("---装饰器中的功能---")
        self.__func()
#说明：
#1. 当用Test来装作装饰器对test函数进行装饰的时候，首先会创建Test的实例对象
#   并且会把test这个函数名当做参数传递到__init__方法中
#   即在__init__方法中的属性__func指向了test指向的函数
#
#2. test指向了用Test创建出来的实例对象
#
#3. 当在使用test()进行调用时，就相当于让这个对象()，因此会调用这个对象的__call__方法
#
#4. 为了能够在__call__方法中调用原来test指向的函数体，
#     所以在__init__方法中就需要一个实例属性来保存这个函数体的引用
#     所以才有了self.__func = func这句代码，从而在调用__call__方法中能够调用到test之前的函数体
@Test
def test():
    print("----test---")
test()
showpy()#如果把这句话注释，重新运行程序，依然会看到"--初始化--"
```
result  
```Python
---初始化---
func name is test
---装饰器中的功能---
----test---
```



