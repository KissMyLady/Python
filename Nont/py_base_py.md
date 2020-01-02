
## Python与其他语言区别   
我们先来看一段[常规java代码](https://github.com/DuGuQiuBai/Java/blob/master/day18/code/day18_Map_HashMap_TreeMap/src/cn/itcast_02/HashMapDemo.java)  
```java
package cn.itcast_02;

import java.util.HashMap;
import java.util.Map;
import java.util.Set;

public class HashMapDemo {
	public static void main(String[] args) {
		HashMap<String, String> hm = new HashMap<String, String>();

		// 创建并添加元素
		hm.put("赵薇",   "安徽");
		hm.put("赵冰冰", "黑龙江");
		hm.put("钱冰冰", "山东");

		// 遍历
		// 方式1
		Set<String> keySet = hm.keySet();
		for (String key : keySet) {
			String value = hm.get(key);
			System.out.println(key + "---" + value);
		}
		System.out.println("---------------------");
	}
}
```
[Java学习个人文档](https://github.com/guanzhenxing/java_interview_manual)    
[Java学习个人文档--基础](https://github.com/guanzhenxing/java_interview_manual/blob/master/java-basic/basic.md)
Java节 选:  
* Java--String 是最基本的数据类型吗？
```
不是。  Java中的基本数据类型只有8个：byte、 short、 int、 long、 float、 double、 char、 boolean；
除了基本类型（primitive type）和枚举类型（enumeration type），剩下的都是引用类型（reference type）   
```
注意Python中的`long`:  
在Python3中,  int没有大小限制, 可以当做long类型使用,  所以python3中没有python2的long类型    

* Java--int和Integer有什么区别？   
```
Java是一个近乎纯洁的面向对象编程语言，但是为了编程的方便还是引入了基本数据类型，但是为了能够将这些基本数据类型当成对象操作   
Java为每一个基本数据类型都引入了对应的包装类型（wrapper class），int的包装类就是Integer，从Java 5开始引入了自动装箱/拆箱机制，使得二者可以相互转换    

Java 为每个原始类型提供了包装类型：

原始类型: boolean，char，byte，short，int，long，float，double
包装类型：Boolean，Character，Byte，Short，Integer，Long，Float，Double
```
* Java--列出一些你常见的运行时异常？
```
ArithmeticException（算术异常）
ClassCastException （类转换异常）
IllegalArgumentException （非法参数异常）
IndexOutOfBoundsException （下标越界异常）
NullPointerException （空指针异常）
SecurityException （安全异常）
```
[Php爬虫框架节选](https://github.com/owner888/phpspider)  
```php
$configs = array(
    'name' => '糗事百科',
    'domains' => array(
        'qiushibaike.com',
        'www.qiushibaike.com'
    ),
    'scan_urls' => array(
        'http://www.qiushibaike.com/'
    ),
    'content_url_regexes' => array(
        "http://www.qiushibaike.com/article/\d+"
    ),
    'list_url_regexes' => array(
        "http://www.qiushibaike.com/8hr/page/\d+\?s=\d+"
    ),
    'fields' => array(
        array(
            // 抽取内容页的文章内容
            'name' => "article_content",
            'selector' => "//*[@id='single-next-link']",
            'required' => true
        ),
        array(
            // 抽取内容页的文章作者
            'name' => "article_author",
            'selector' => "//div[contains(@class,'author')]//h2",
            'required' => true
        ),
    ),
);
$spider = new phpspider($configs);
$spider->start();
```

深入下去发现还是很多不一样, 但是作为语言来说, 一通百通    
有学过乐器的都有这种同感, 乐理是一样的, 不同的是手按的方式不一样   
不变的是对音乐整体的把握和节奏的把握,  实质的不一样就是乐器怎么发出声音不一样   
小提琴是马尾弦的摩擦产生声音,  吉他是拨弦, 钢琴是敲击, 萨克斯是空气在内腔的的震动...   

同样, 语言是为了操控了机器,  机器发展了百年,  底层CPU逻辑开关没怎么变, 算法没有变,,,   
程序语言的最终, 都是要往数学上靠, 语言只是第一层台阶   


## 来做下简单对比      
语言特点：简洁、优雅，省略了各种大括号和分号，还有一些关键字，类型说明    

语言类型：解释型语言，运行的时候是一行一行的解释，并运行，所以调试代码很方便，开发效率很高    

第三方库：python是开源的，并且python的定位时任由其发展，应用领域很多比如Web，运维，自动化测试，爬虫，数据分析，人工智能    
* Python具有非常完备的第三方库    

Python和Java相比:   
* Python比Java要简单        
* Python是函数为一等公民的语言，而Java是类为一等公民的语言。Python是弱类型语言，而Java是强类型语言    

Python和C相比    
* Python的类库齐全并且使用简洁，很少代码实现的功能用C可能要很复杂对于速度    
* Python的运行速度相较于C，绝对是很慢了。Python和CPython解释器都是C语言编写的    


## 详细区别      
[知识来源--CSDN](https://blog.csdn.net/zw0Pi8G5C1x/article/details/80754433)  
Java是一种严格的类型语言，这意味着必须显式声明变量名。相比之下,动态类型的Python则不需要声明变量。
在编程语言上有许多关于动态和静态类型的争论   
但有一点应该注意：Python是一种语法简单的功能强大的语言，能够通过编写脚本就提供优秀的解决方案，并能够快捷地部署在各个领域。

Java可以创建跨平台的应用程序，而Python几乎兼容当前所有操作系统   
对新手来讲， Python比Javaf更容易上手，而且代码易读性强，但是如果你想你的代码可以在任何地方都能执行的话, 那么还是选择Java吧   
不过Java的可移植性也是有代价的, 使用Java你需要购买更大的机器，消耗更多的内存，并且程序更加难以开发  

Java比Python更复杂，没有技术背景的人学起来并非易事。

[其他文章](https://blog.csdn.net/qiansg123/article/details/80129610)    
 
