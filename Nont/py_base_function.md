函数的一些定论:  
======
 
# 1. 函数的引用: 
```Python
def test(num):
    print("在函数内部 %d 对应的内存地址是 %d" % (num, id(num)))
    result = "hello"
    print("函数要返回数据的内存地址是 %d" % id(result))
    return result  # 返回的是引用，而不是数据本身

a = 10  # 数据的地址本质上就是一个数字
print("a 变量保存数据的内存地址是 %d" % id(a))

r = test(a)
print("%s 的内存地址是 %d" % (r, id(r)))
```
输出结果:   
```
a 变量保存数据的内存地址是 1748559936
在函数内部 10 对应的内存地址是 1748559936
函数要返回数据的内存地址是 82140704
hello 的内存地址是 82140704
```
说明:  
>  调用 test 函数，本质上传递的是实参保存数据的引用，而不是实参保存的数据!      
> 注意：如果函数有返回值，但是没有定义变量接收   
> 程序不会报错，但是无法获得返回结果   


# 2. 函数不能直接修改全局变量  
```Python
num = 10
def demo1():
    global num
    num = 99
    print("demo1 ==> %d" % num)

def demo2():
    print("demo2 ==> %d" % num)


demo1()
demo2()
```
输出结果:  
```
demo1 ==> 99
demo2 ==> 99
```
说  明:    
1. 希望修改全局变量的值, 使用global声明一下变量即可      
2. 这是声明它是全局变量, 可以看到, 现在是个地方都可以改动num了   


# 3. 多个返回值   
第一种方法: 
```Python
def measure():
    temp = 39
    wetness = 50
    return temp, wetness

# 元组
result = measure()
print('Print resule: ', result)
print('result[0]: ', result[0])
print('result[1]: ', result[1])

```
输出结果:  
```
Print resule:  (39, 50)
result[0]:  39
result[1]:  50
```
说  明:　
1. 元组-可以包含多个数据，因此可以使用元组让函数一次返回多个值     
2. 如果函数返回的类型是元组，小括号可以省略    
3. `return (temp, wetness)`    

第二种方法:    
```Python
def measure():
    temp = 39
    wetness = 50
    return temp, wetness

gl_temp, gl_wetness = measure()

print('gl_temp: ', gl_temp)
print('gl_wetness: ', gl_wetness)
```
输出结果: 
```
gl_temp:  39
gl_wetness:  50
```
说  明:
1. 如果函数返回的类型是元组，同时希望单独的处理元组中的元素      
2. 可以使用多个变量，一次接收函数的返回结果        
3. #### 使用多个变量接收结果时，变量的个数应该和元组中元素的个数保持一致   


# 4. 可变参数与不可变参数   
```Python
def demo(num, num_list):

    num = 1
    num_list = [7, 5, 3]

    print(num)
    print(num_list)
    print("函数执行完成")


gl_num = 999
gl_list = [40, 50, 60]
demo(gl_num, gl_list)
print(gl_num)
print(gl_list)
```
输出结果:   
```Python
1
[7, 5, 3]
函数执行完成
999
[40, 50, 60]
```
#### 结论: 在函数内部, 针对参数使用赋值语句, 不会修改到外部的实参变量     


# 5. 函数内部通过方法修改可变参数   
```Python
def demo(num_list):
    num_list.append(9)
    print(num_list)
    print("函数执行完成")

gl_list = [1, 2, 3]
demo(gl_list)
print(gl_list)
```
输出结果:   
```Python
[1, 2, 3, 9]
函数执行完成
[1, 2, 3, 9]
```

#### 结论: list是可变参数   


# 6. 缺省参数   
```Python
def print_info(name, gender=True):
    gender_text = "男生"

    if not gender:
        gender_text = "女生"

    print("%s 是 %s" % (name, gender_text))

print_info("小明")
print_info("老王")
print_info("小美", False)
```
输出结果:  
```
小明 是 男生
老王 是 男生
小美 是 女生
```
注意: 在指定缺省参数的默认值时，应该使用最常见的值作为默认值!     


# 7. 多个参数(不定长参数)     
```Python
def demo(num, *nums, **person):
    print(num)
    print(nums)
    print(person)

demo(1, 2, 3, 4, 5, name="小明", age=18)
```
输出结果:  
```
1
(2, 3, 4, 5)
{'name': '小明', 'age': 18}
```
说  明:   
num 对应 第一个参数   
`*nums` 对应 后面的几个参数, 
`**person` 对应 字典形式的传值  

可以看到, 叫什么并不重要   

### 不定长参数传递, 求和   
```Python
def sum_numbers(*args):
    num = 0;  print(args)
    for n in args:
        num += n
    return num

result = sum_numbers(1, 2, 3, 4, 5)
print(result)
```
输出结果:  
```
(1, 2, 3, 4, 5)
15
```

### 不定长参数的拆包解包  
```Python
def demo(*args, **kwargs):
    print(args)
    print(kwargs)

gl_nums = (1, 2, 3)
gl_dict = {"name": "小明", "age": 18}

print('><'*20)
demo(gl_nums, gl_dict)
print('><'*20)


demo(*gl_nums, **gl_dict)

demo(1, 2, 3, name="小明", age=18)
```
输出结果:  
```
><><><><><><><><><><><><><><><><><><><><
((1, 2, 3), {'name': '小明', 'age': 18})
{}
><><><><><><><><><><><><><><><><><><><><

(1, 2, 3)
{'name': '小明', 'age': 18}

(1, 2, 3)
{'name': '小明', 'age': 18}
```
可以看到, 这种形式的传值不可取:  
```Python
def demo(*args, **kwargs):
	pass
demo(gl_nums, gl_dict)
```
第一个args为元祖形式, 后面逗号全是args的状态     

在如这种简便方法:  
```Python
demo(*gl_nums, **gl_dict)

# 输出:
# (1, 2, 3)
# {'name': '小明', 'age': 18}
```

# 8. 递归  
```Python
def sum_number(num):
    print(num)

    if num == 1:
        return 
    sum_number(num - 1)

sum_number(3)
```
特点:  
1. 自己调用自己    
2. 递归的出口，当参数满足某个条件时，不再执行函数    


递归求和:　
```Python
def sum_numbers(num):
    if num == 1:
        return 1

    temp = sum_numbers(num - 1)
    print(temp)
    return num + temp


result = sum_numbers(10)
print(result)
```
