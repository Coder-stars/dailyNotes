1 Python 中单下划线与双下划线的特殊用法

[参考一](https://www.jb51.net/article/168807.htm)，[参考二](https://www.jb51.net/article/160280.htm)

``` bash
函数使用单下划线_开头
　　使用单下划线(_)开头的函数_func不能被模块外部以: from module import *形式导入。
　　但可以用：from module import _func形式单独导入。
类属性和类方法使用单下划线_开头
　　_开头为保护类型的属性和方法，仅允许类内部和子类访问，类实例无法访问此属性和方法。
类属性和类方法使用双下划线__开头
　　__开头为私有类型属性和方法，仅允许类内部访问，类实例和派生类均不能访问此属性和方法。
　　所以双划线比单划线权限更严格。
补充说明
	对于__开头的属性和方法如果派生类一定要访问，使用单下划线+基类名+双下划线开头的属性和方法的形式，且双下划线开头的属性和方法后面最多只能以一个单下划线结束，否则也无法访问。
```

2 collection.defaultdict()方法研究

3 取交集高级操作

list(set(值2).intersection(set(值1)))

defaultdicy()与dict()  https://www.jianshu.com/p/bbd258f99fd3

[类中的魔法方法](https://www.cnblogs.com/dachenzi/p/8185792.html)

