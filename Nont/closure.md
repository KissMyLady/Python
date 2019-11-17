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



