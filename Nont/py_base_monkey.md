[猴子补丁今生前世](https://blog.csdn.net/yiliumu/article/details/77986090):    
猴子补丁是一个概念，不是python中发明的，其他动态语言也有这么个概念。

《松本行弘的程序世界》这本书，里面专门有一章讲了猴子补丁的设计      
所谓的猴子补丁的含义是: 指在动态语言中，`不去改变源码而对功能进行追加和变更`(装饰器也是这样)。    

猴子补丁的这个叫法起源于Zope框架，大家在修正Zope的Bug的时候经常在程序后面追加更新部分，  
这些被称作是`杂牌军补丁(guerilla patch)`，后来guerilla就渐渐的写成了gorllia(猩猩)，   
再后来就写了monkey(猴子)，所以猴子补丁的叫法是这么莫名其妙的得来的。      


很多时候要用到import json, 后来发现ujson性能更高, 
如果觉得把每个文件的import json改成 import ujson as json成本较高，

或者说想测试一下用ujson替换json是否符合预期，只需要在入口加上:  
```Python
import json
import ujson

def monkey_patch_json():
   json.__name__ = 'ujson'
   json.dump = ujson.dumps
   json.loads = ujson.loads

monkey_patch_json()
```
