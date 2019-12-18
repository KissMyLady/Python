Ubuntu 18.04安装心得体会
====

## 安装Ubuntu
* 安装系统过程一定要屏蔽网络，不然下载非常非常慢，海外源，即使科学上网也慢  


## 安装虚拟机增强包
VMware有增强包  
  Vbon有增强包  
安装后，复制粘贴，文件拖拽很方便(虚拟机具体可以谷歌)  


## 更新Ubuntu系统下载源  
进去这个文件后，里面内容全部删除  
* 进去后，按两下d就是全部删除，把d按住，就能全删  
```Linux
cd /etc/apt/
sudo vim /etc/apt/sources.list
```
接下来，在里面放入如下内容(也可换成别的源)   
```linux
deb http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse

deb-src http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse



deb http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse

deb-src http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse



deb http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse

deb-src http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse

deb http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse

deb-src http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse

deb http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse

deb-src http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
```


## 执行所有升级
```Linux
# sudo apt update
# sudo apt upgrade -y
```


## 安装Python3.8
### 1、下载Python3.8源程序压缩包
```Linux
wget https://www.python.org/ftp/python/3.8.0/Python-3.8.0.tgz
```
### 2、安装编译Python源程序所需的包   
```Linux
# sudo apt install build-essential -y
# sudo apt install libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev -y
# sudo apt-get install zlib1g-dev
```   
### 3、解压缩  
```Linux
# tar -xzvf Python-3.8.0.tgz
```

### 4、配置  
```Linux  
# cd Python-3.8.0  
# ./configure --enable-optimizations  
```  
> 执行上述语句将启用代码的发布版本，可以优化二进制文件以更好的更快的运行    
> 但是需要运行测试，编译时需要花费一些时间（大约半小时），也可以不进行这一项配置。    


## 5、编译和安装Python3.8    
```Linux  
# sudo make    
# sudo make install  
```  
花费时间最多  

### 6、配置环境变量及创建快捷方式    
[root@localhost bin]# echo "/usr/local/lib" > /etc/ld.so.conf.d/python3.8.conf  
[root@localhost bin]# ln -s /usr/local/bin/python3.8 python  
[root@localhost bin]# mv ~/.profile ~/.profile.bak  
[root@localhost bin]# vim ~/.profile  

export LD_LIBRARY_PATH="/usr/local/lib"  
alias python="/usr/local/bin/python3.8"  
alias python3.8="/usr/local/bin/python3.8" 
​

### 7. 查看Python版本  
```Linux  
python3   
pip3 -V
```  

## 恭喜，你已经完成了安装   
如果有问题，可加群QQ免费指导: 36877 9008
或者在GihHub向我提问  
