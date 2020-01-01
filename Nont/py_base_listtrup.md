列表list与元祖tiple
====
Python中包含6种内建序列, list, tuple, srt, Unicode str, buffer对象, xrange对象  
我们这里讨论最常用的两种: 列表和元祖  

## 通用方法  
Python中所有序列都可以进行一些特定方法操作:    
1. indexing    
2. slicing   
3. adding  
4. multiplying    
5. 成员资格    
6. 长度len  
7. min 和max    

### 1. indexing索引   
![ScreenShot00-190](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00190.jpg) 
![ScreenShot00-191](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00191.jpg)  

### 2. 分片slicing  
常规分片  
![ScreenShot00-192](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00192.jpg)    
增加步数的分片     
![ScreenShot00-193](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00193.jpg)    
倒序切片  
![ScreenShot00-194](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00194.jpg)  

### 3. 序列相加  
![ScreenShot00-195](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00195.jpg) 

### 4. 乘法  
![ScreenShot00-196](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00196.jpg)    

### 5. 成员资格  
![ScreenShot00-197](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00197.jpg)    

### 6. 长度, 最大, 最小  
![ScreenShot00-198](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00198.jpg)  


## 列表  
列表是一个可迭代对象:    
![ScreenShot00-199](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00199.jpg)  
更新列表的几种常规方法:  
1. 元素赋值  
![ScreenShot00-201](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00201.jpg)    

2. 增加元素  
* insert方法:  
![ScreenShot00-202](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00202.jpg)       
* append方法:    
![ScreenShot00-203](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00203.jpg)  
* extent方法:  
![ScreenShot00-209](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00209.jpg)   
注意与`+`方法区分, extent方法是在原空间上直接添加, 而`+`是生成新空间, 不对原空间进行修改的  

3. 删除元素    
* del方法:    
![ScreenShot00-204](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00204.jpg)    
* pop方法:   
![ScreenShot00-205](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00205.jpg)    
* remove方法:    
![ScreenShot00-206](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00206.jpg)  
* clear方法:    
![ScreenShot00-207](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00207.jpg)    

4. 统计数量     
* len方法与count方法:    
![ScreenShot00-208](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00208.jpg)      

5. 整体方法  
* sort方法:  
对list排序, 从小到大排序  
* sort兄弟方法:    
sorted排序返回副本, 不对实体进行修改  

* 高级排序   
```Python
filee = ['study', 'python', 'java']
filee.sort(key=len, reverse=True)
filee
['python', 'study', 'java']
```

* copy方法:  
直接复制列表, 注意, 这里的复制是深拷贝    
![ScreenShot00-210](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00210.jpg)  
浅拷贝1:    
![ScreenShot00-211](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00211.jpg)  
浅拷贝2:    
![ScreenShot00-212](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00212.jpg)  

深拷贝与浅拷贝的区别:  
![ScreenShot00-213](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00213.jpg)    
可以发现, `new`与`ab`是完全两个独立空间  
![ScreenShot00-214](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00214.jpg)   
我们进一步发现, 就连`new`里面的元素与`ab`元素也不一样    

#### 但是, 这个又怎么解释 ?    
![ScreenShot00-215](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00215.jpg)    
真是奇了怪, 这里明明是深拷贝, 为什么里面的地址是一样的?    
![ScreenShot00-216](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00216.jpg)    
![ScreenShot00-217](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00217.jpg)  
再次查看id地址:   
![ScreenShot00-218](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00218.jpg)  



## 元祖
元祖是一个可迭代对象:    
![ScreenShot00-200](https://github.com/KissMyLady/Python/blob/master/Img/ScreenShot00200.jpg)     
1. 元祖拼接同上  
2. 元祖元素不可修改   
3. 元祖只能作为整体删除, 增加  

