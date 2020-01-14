继承/封装/多态  
=====

## 什么是OOP ?  
一个小程序很容易写, 而且代码很短，不必用专门工具, 记事本就够了，真的！  
    
举个例子，微软的Office大约有4000万代码    
4000万！  
我们可以把重用的部分封装成一个个对象, 需要的时候调用    
[点击进入--软件工程-OOP](https://github.com/KissMyLady/Computer/blob/master/Note/Software_Engineering.md)


## 封  装
封装有两层含义  
我们先看一个简单例子   
#### 1. 封装的第一层含义: 将对象和方法集中在一个地方   
```Python
class Rectangle(object):
    def __init__(self, w, l):
        self.width = w
        self.len = l

    def area(self):    # 封装
        return self.width * self.len 
``` 
#### 2. 隐藏复杂度  
```Python
class Data(object):
    def __init__(self):
        self.nums = [1, 2, 3, 4, 5, 6]

    def change_data(self, index, n):
        self.nums[index] = n
``` 
我们可以看到, 数据内部很复杂, 但是改数据很简单  
> 只需要输入地址(index), 输入想要改成什么数据(n) 
> 对于外界来说. 这很简单, 我们隐藏了复杂度  
```Python
data = Data()
one = data.num[0] = 123
print(one.nums)

# >>> [123, 2, 3, 4, 5, 6]
```
### 如果`[]`改成了元祖?   
* 这样代码将无法运行     
许多编程语言允许程序员定义私有变量和私有方法来解决这个问题：   
> 对象可以访问这些变量和方法，但是客户端代码不行    
 
私有变量和方法适用于如下场景：     
> 有一个类内部使用的方法或变量，并且希望后续调整代码实现（或保留选项的灵活）   
>> 但不想让任何使用该类的人依赖这些方法或变量，因为后续代码可能会调整（到时会导致客户端代码无法执行）     

私有变量是封装包含的第二个概念的一种范例     
> 私有变量隐藏了类的内部数据，避免客户端代码直接访问    
> 公有变量则相反，它是客户端代码可以直接访问的变量    

> Python 中没有私有变量，所有的变量都是可以公开访问的    
> Python 通过另一种方法解决了私有变量应对的问题：使用命名约定   
>> 在Python中，如果有调用者不应该访问的变量或方法，则应在名称前加下划线   
>>> Python 程序员看见某个方法或变量以下划线开头时，就会知道它们不应该被使用（不过实际仍然是可以使用的）   
[点击进入--私有化](https://github.com/KissMyLady/Python/blob/master/Nont/oop_private.md)    
我们看这个例子:    
```Python    
class PublicPrivate(object):  
    def __init__(self): 
        self.public = "safe"  
        self._unsafe = "unsafe"  
  
    def public_method(self):  
        # 客户端可以使用  
        pass  
  
    def _unsafe_method(self):  
        # 客户端不能使用    
        pass  
```  
编写客户端代码的我们看到上述代码后，会知道变量self.public是可以安全使用的     
> 但是不应该使用变量self._unsafe，因为其以下划线开头     
> 如果非要使用，后续可能会有风险      
>> 维护上述代码的程序员，没有义务一直保留self._unsafe，因为调用者本不应该访问该变量    
>> 客户端程序员也能确认public_method是可以放心使用的，而_unsafe_method则不然，因为其名称同样以下划线开头    

  
## 继  承  
继承: 君君臣臣父父子子       
我们先来看一个简单代码块      
```Python   
class Shape():   
    def __init__(self, w, l):  
        self.width = w  
        self.len = l 
  
    def print_siez(self):   
        pritn(self.width ,"by", self.len) 
```  
```Python  
my_shape = Shape(20, 25) 
# >>> 20 by 25    
```  
这是简单的实例化对象, 并调用方法, 接下来我们来定义一个子类         
> 在创建子类时，将父类的变量名传入子类，即可继承父类的属性        
```Python  
class Shape(object):  
    def __init__(self, w, l):  
        self.width = w 
        self.len = l  
  
    def print_siez(self):  
        pritn(self.width ,"by", self.len)   
  
class Square(Shape): 
    pass   
```  
```Python  
a_S = Square(20, 20) 
# >>> 20 by 20  
```  
* 因为我们将Shape类作为参数传给了Square类，后者就继承了Shape类的变量和方法     
Sqaure类中定义的代码只有pass，表示不执行任何操作  

> 由于继承了父类，我们可以创建Square对象，传入宽度和长度参数， 
>> 并在其上调用print_size方法，而不需要再写任何代码（除pass）   
>>> 由此带来的代码量缩减很重要，因为避免代码重复可以让程序更精简、更可控  

子可继承父, 可以有自己的性格, 思想, 人格, 不会影响父  
当子继承父的'性格', '思想', '人格', 我们可以定义子'重新找回自己(重新做人)'  
#### 继承实例  
```Python
class Shape(object):  
    def __init__(self, w, l):  
        self.width = w 
        self.len = l  
  
    def print_siez(self):  
        pritn(self.width ,"by", self.len)   
  
class Square(Shape): 
    def area(self):
        return self.width * self.len

    def print_size(self):
        print("I'm",self.width ,"by", slef.len)   
```
```Python
a_square = Square(20, 20)
a_square.print_siez()

# >>> I'm 20 by 20
```


## 多  态  
多态: 为不同的基础形态(数据类型)提供相关接口的能”   
生物学多肽: 由10~100个氨基酸分子脱水缩合而成的化合物叫多肽。    

生物学上的多肽, 是很多氨基酸分子脱水缩和后, 拼接在一起, 有很多数量(种类/肽)的意思   
我们程序上的多态, 是接口有多种, 多种-接口状态 
> 接口，指的是函数或方法
我们来看这个简单例子:   
```Python
print('Hello OOP')
print(2050)
print(2050.01.01) 
```
print函数为字符串、整数和浮点数这3种不同的数据类型提供了相同的接口       
我们不必定义并调用3个不同的函数    
> 如调用print_string打印字符串   
>> 调用print_int 打印整数    
>>> print_float打印浮点数   
只需要调用print函数即可支持所有数据类型     

假设我们要画三角形, 正方形, 园   
于是我们可以定义三个类: Triangle, Square, Circle   
画画很简单, 我们只要调方法就可以了:   
```Python
Triangle.draw()   
Square.draw() 
Circle.drwa()  
```      
每个对象都有一个draw接口    
这样就为3个不同的数据类型提供了相同接口          
  
如果没有多态, 每个图形就需要一个新的方法:    
```Python 
draw_triangel  
draw_square  
draw_circle 
```     
如果程序有上百万,上千万的图形要画, 这会发生什么?  
> 程序规模大, 更难阅读, 更难编写, 也更加脆弱  
> 更难以优化:   
>> 每添加一个新图形，必须要找到代码中所有要画出图形的地方  
>> 并为新图形添加检查代码(以便确定使用哪个方法)  
>> 而且还需再调用新的画图函数    

下面我们再看看使用了多态与没有使用(伪)代码对比:  
```Python

# 未使用多态的代码画图
shapes = [trl, sql, crl]
for a_shape in shapes:
    if type(a_shape) == "Triangle":
        a_shape.draw_triangle()
    if type(a_shape) == "Square":
        a_shape.draw_square()
    if type(a_shape) == "Circle":
        a_shape.draw_cirlce()


# 使用多态的代码画图
shapes = [trl, swl, crl]
for a_shape in shapes:
    a_shape.draw()
```
> 如果在没有使用多态的代码中添加新图形  
> 则必须修改for循环中的代码，检查a_shape的类型并调用其画图方法  
>
>> 通过统一多态的接口，可以随意向shapes列表中添加新图形，
>> 不需要再添加额外的代码即可画出对应图形


## 抽  象   
抽象: 指的是“剥离事物的诸多特征，使其只保留最基本的特质”的过程   
我们常说的OOP三大特性是继承, 封装, 多态, 其实还有一个很重要的特性, 那就是抽象       
外国许多程序员都把抽象作为OOP的四大特性之一, 因为抽象能力对于程序编写来说是至关重要的   
>　我们存在的本质, 就是用二进制在另外一个平行世界抽象化这个宇宙   
>> 用抽象, 在电网中建立一个世界, 属于我们的世界
>>> 抽象用的好, 你就是上帝. 上帝说, 要有光, 于是就有了光, 你也可以  
```Python
c = C
```           

在面向对象编程中，使用类进行对象建模时就会用到抽象的技巧   
> 我们假设要对人进行建模  
>> 人的特征很复杂：头发, 眼睛颜色，还有身高、体重、性别等诸多特征。    

如要创建一个类代表人，有一些细节可能与要解决的问题并不相关。  
举个例子，我们创建一个Person类，但是忽略其眼睛颜色和身高等特征，这就是在进行抽象。  
Person对象是对人的抽象，代表的是只具备解决当前问题所需的基本特征的人




