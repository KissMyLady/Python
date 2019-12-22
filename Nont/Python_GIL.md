GIL全局解释器锁  
===

## GIL含义     
* 每个线程在执行的过程都需要先获取GIL，同一时刻只有一个线程可以执行代码   
* 同一时刻, 只有一个线程干活  


### 说  明  
![gil-1](https://github.com/KissMyLady/Python/blob/master/Img/Python/gil-1.jpg)   
先作如下推理:  
1. 如果cpu全满, 说明线程之间没有关系;  
2. 如果cpu没有全满, 说明线程之间还是有关系的;  

 
### 多线程现象:   
![gil-2](https://github.com/KissMyLady/Python/blob/master/Img/Python/gil-2.jpg)      
> 1. 两个cpu只有一半执行了      
> 2. 加起来才只有一个满CPU  
   
### 多进程现象:    
![gil-3](https://github.com/KissMyLady/Python/blob/master/Img/Python/gil-3.jpg)     
![gil-4](https://github.com/KissMyLady/Python/blob/master/Img/Python/gil-4.jpg)     


### 结 论:    
1. (一个进程内)线程之间有关系     
  

### 推论(结论):      
1. 由于有GIL锁的存在, `同一时刻, 只有一个线程在执行`         
2. 多线程本身是假的, 单位时间内, 看似两个线程在同时执行, `本质上只干了一半的活`    

  

## 为什么Python的线程是假的?    
因为GIL(全局解释器锁)的存在,  `同一时刻, 只有一个干活`     

  

## 为什么Python中线程这么low, 还用它?  
1. GIL的问题不是Python语言的问题, 而是执行代码解释器的问题     
![gil-5](https://github.com/KissMyLady/Python/blob/master/Img/Python/gil-5.jpg)    
> Python官网推荐的解释器是C语言的解释器, 这个解释器称为cPython解释器        
> java-----jPython  
>   
>> c语言写的解释器, 由于历史原因, 导致了今天解释器缺点有GIL, 而jPython是没有的     
>> 只有c语言有这个      
>>  
>>> 因为:  Python作者很久之前, 没有考虑到电脑多核, 多任务     
>>> ![6](https://github.com/KissMyLady/Python/blob/master/Img/Python/gil-6.jpg)    
>>> 有考虑移除, 最终的效率不高, 所以一直有保留    
作者说:    
如果你想要发挥多核的效率, 请使用进程   



## 爬虫多线程   
多线程爬取是否比单线程爬取快 ? 是的    

原因:  
> 1. 网络有延迟  
> 2. 等待网络延迟数据的时间, 抽出来, 请求下一个目标(见缝插针)   



## 实际应用领域:   
计算密集型/ IO密集型

### 计算密集型:   
* 活很多(计算量大)    
* 只干一半的活, 剩下的活谁来干 ? 等我来干?    



### IO密集型:    
* 完成时间 = 一些的活(计算量) + 一些等待时间(读写/请求/延迟)    
* 真的只用干一点点的活, 见缝插针的干活, 时间就省下来了   



## 克服GIL问题  
1. 换解释器  

2. 用其他的语言实现  



## 一分钟学会C语言  
#### 1. vim c_test.c   
```C
#include<stdio.h>
void test()
{
	printf("----test-----");

}

int main(int argc, char **argv)
{
	pritnf("Hello World\n");
	test();
	return 0:
}   
```
- 1. c语言里面必须有main函数(Python不必须)  
- 2. #include<stdio.h>必须写, 相当于import     
- 3. {} 相当于定义函数    
  
#### 2. gcc c_test.c     
>>> ls查看, 可以看到输出了a.out文件  
  
#### 3. ./a.out  
#### 4. Hello World  
    

### 说 明  
C语言是编译型语言, 如果打开a.out文件, 可以看到是二进制  
这个文件, CPU是可以直接执行的  
![7](https://github.com/KissMyLady/Python/blob/master/Img/Python/gil-7.jpg)  



  
## Python是胶水语言  
我们先看一个C程序   
```C
void DeadLoop() 
{
	while(1)
	{
		;
	}

}
```
![gil-10](https://github.com/KissMyLady/Python/blob/master/Img/Python/gil-10.jpg)   
![gil-8](https://github.com/KissMyLady/Python/blob/master/Img/Python/gil-8.jpg)   
 
这时候的CPU:  
![gil-11](https://github.com/KissMyLady/Python/blob/master/Img/Python/gil-11.jpg)     


只要思想不滑坡, 办法总比困难多  
