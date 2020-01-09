常用命令   
====


### locale   
说明: 显示当前语系

改英文语系:  
```Linux
LANG=en_US.utf8
export LC_ALL=en_US.utf8
```
![ScreenShot-00285]()   
这里我使用的是Ubuntu18.04Server版本, 是纯英文界面   
但是这里Lang没有显示, 有点奇怪   

### date
说明: 显示日期
![ScreenShot-00286]()   

查看date使用方法: `man date`, or `info date`   

查看时间: 类似于: 2015-10-16-20:03   
`date +%Y-%m-%d-%H:%M`   
![ScreenShot-00288]()   


### cal
说明: 显示日历   
![ScreenShot-00287]()  


### bc
说明: 计算器      
但是用这个命令不如用python计算, python简单又强大   

bc仅预设输出整数, 使用scale=number 来设置小数点位数(精度)  


### nano
说明: 使用少, 用的都是vim    
使用用vim, 命令后跟文件名   


### shutdown  
我想让电脑在今天的1:30 自己关系, 要怎么弄?   
`shutdown -h 1:30`   



### chgrp   
说明: 改变文件所属群组    
改变文件群组为user所属   
`chgrp user today.txt`

### chown   
说明: 改变文件的拥有者   

### chmod   
说明: 改变文件权限, 常用  

`r: 4, w:2 , x: 1`   
改变文件为所有人都能访问的通用状态:   
`chmod 777 demo.txt`    


