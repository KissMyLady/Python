Python传参是传值还是传址?  
=====

# [第一种观点: 在python中讨论值传递还是引用传递是没有意义的](https://blog.csdn.net/liudongdong19/article/details/79594705)
要真正对这些情况作出解释，其实是应该搞明白python(对可变对象和不可变对象的)赋值过程中是如何分配内存地址的。   
```Python
l1=[1,2,3]
l2=[1,2,3]
a=1
b=1

print(id(l1))
print(id(l2))
print(id(a))
print(id(b))
```
输出结果:  
```
81511496
82879048
1765795760
1765795760
```
可以看到: 对于可变list来说，即便内容一样，Python也会给它们分配新的不同的地址    

然而，对于不可变int来说，内存里只有一个1。 即便再定义一个变量c=1，也是指向内存中同一个1。 换句话说: 不可变对象1的地址是共享的    

接下来让我们看看在函数中调用`可变对象`和`不可变对象`，并修改他们的值，会是一个什么情况。   

对于`不可变对象`int，我们来看看最简单的情况:   
```Python
a = 1; print(id(a))

def x(a):
  print(id(a))
  b = a
  print(id(b))
  
x(a)
```
输出结果: 
```
1765795760
1765795760
1765795760
```
这看起来就是一个引用传递, 函数外、里都指向了同一个地址   

但我们再来看一个极端情况:   
```Python
a = 1; print(id(a))

def x():
  b = 1
  print(id(b))
  
x()
```
输出结果: 
```
1765795760
1765795760
```
很神奇?(不生气, 笑哭): 函数外定义的a和函数内定义的b没有任何关系, 它们指向同一个地址     

所以你说如何判断它是值传递还是引用传递？     
讨论这个问题根本没有意义，因为内存里只有一个1  

当我把值1传递给函数里的某一个变量的时候，我实际上也传递了地址，因为内存里只有一个1     

甚至于说直接给函数里的b赋值1, 都可以让函数外的a和函数内的b指向同一个地址   



## 下面来看看传递可变对象list的情况:   
```Python
l = [1,2,3]; print(id(l))

def a(x):
  print(id(x))
  x.pop()
  print(x)
  print(id(x))
  x = x + [3]
  print(x)
  print(id(x))
  
a(l)
```
输出结果: 
```
52675656
52675656
[1, 2]
52675656
[1, 2, 3]
82422088
```
#### 只要创建一个新的可变对象，Python就会分配一个新的地址。 就算我们创建的新可变对象和已存在的旧可变对象完全一样, Python依旧会分配一个新的地址

而pop并不是创建新的可变对象，pop是对已有的可变对象进行修改   
	
所以可以总结为:   
 
1. 在Python中，不可变对象是共享的，创建可变对象永远是分配新地址  

2. 这个时候我们再回过头来思考值传递和引用传递的问题，就会发现在Python里讨论这个确实是没有意义。  

3. 我们可以说: #### Python有着自己的一套特殊的传参方式，这是由Python动态语言的性质所决定的  


# [第二种观点: `传对象引用`的方式](https://www.cnblogs.com/loleina/p/5276918.html)  
结 论: #### Python不允许程序员选择采用传值还是传引用       
#### Python参数传递采用的肯定是`传对象引用`的方式      

这种方式相当于传值和传引用的一种综合。 如果函数收到的是一个可变对象(比如字典或者列表)的引用       
就能修改对象的原始值－－相当于通过`传引用`来传递对象。  
如果函数收到的是一个不可变对象（比如数字、字符或者元组）的引用, 就不能直接修改原始对象--相当于通过`传值`来传递对象     
```Python
def test(c):
    print(id(c))
    c += 2
    print(id(c))
    return c

if __name__=="__main__":
    a = 2
    print('第一次打印a id: ', id(a))
    n = test(a)
    
    print('打印a: ', a)
    print('打印a id: ', id(a))

'''
第一次打印a id:  1784604608
1784604608
1784604640
打印a:  2
打印a id:  1784604608
'''
```
先看一个例子:   
![ScreenShot-00348](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot-00348.jpg)   

id函数可以获得对象的内存地址.很明显从上面例子可以看出，将a变量作为参数传递给了test函数，传递了a的一个引用    
   
把a的地址传递过去了，所以在函数内获取的变量C的地址跟变量a的地址是一样的，但是在函数内，对C进行赋值运算，C的值从2变成了4  
   
实际上2和4所占的内存空间都还是存在的，赋值运算后，C指向4所在的内存。而a仍然指向2所在的内存，所以后面打印a，其值还是2     


那python函数传参就是传引用？   
然后传参的值在被调函数内被修改也不影响主调函数的实参变量的值？  
```
>>> list1=[1,2]
>>> id(list1)
64185208

>>> list1[0]=[0]
>>> list1
[[0], 2]

>>> id(list1)
64185208
```
