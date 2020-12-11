# Django日常总结

## 1 字符串与类名转换两种方法

### Way one:

 from django.util.models_loading  import import_string

example

```python
from django.utils.module_loading import import_string
ValidationError = import_string('django.core.exceptions.ValidationError')
```

等同于

`from django.core.exceptions import ValidationError`

总结：可以直接把字符串转化为类名

#### Way two:

使用globals()函数，用法如下：

xxx= globals()[字符串]

就可以把指定的字符串转化为类

![image-20200623161528253](/Users/coder_li/Library/Application Support/typora-user-images/image-20200623161528253.png)

### 2 querysetApi 

#### values(*fields) --[参考资料](https://www.cnblogs.com/rgxx/p/10382664.html)，[官方文档](https://docs.djangoproject.com/zh-hans/3.0/ref/models/querysets/#values)

​    返回一个ValuesQuerySet(QuerySet的子类)，迭代时返回字典而不是模型实例对象，每个字典表示一个对象，键对应模型的属性名称------通俗说就是把queryset变为字典

   values() 接收可选的位置参数*fields，它指定SELECT 应该限制哪些字段。如果指定字段，每个字典将只包含指定的字段的键/值。如果没有指定字段，每个字典将包含数据库表中所有字段的键和值。

注意点：如果你有一个字段`foo` 是一个`ForeignKey`，默认的`values()` 调用返回的字典将有一个叫做`foo_id` 的键，因为这是保存实际的值的那个隐藏的模型属性的名称（`foo` 属性引用关联的模型）。当你调用`values()` 并传递字段的名称，传递`foo` 或`foo_id` 都可以，得到的结果是相同的（字典的键会与你传递的字段名匹配）。

#### Values_list(*fields,flat=False,named=False)

与values() 类似，只是在迭代时返回的是元组而不是字典。每个元组包含传递给values_list() 调用的字段的值 —— 所以第一个元素为第一个字段，以此类推.

如果只传递一个字段，你还可以传递flat 参数。如果为True，它表示返回的结果为单个值而不是元组,

example:

```
>>> Entry.objects.values_list('id').order_by('id')
[(1,), (2,), (3,), ...]

>>> Entry.objects.values_list('id', flat=True).order_by('id')
[1, 2, 3, ...]
```



`如果有多个字段，传递`flat` 将发生错误。

如果你不传递任何值给`values_list()`，它将按照字段在模型中定义的顺序, 返回模型中的所有字段。

注意，这个方法返回`ValuesListQuerySet`。这个类的行为类似列表。大部分时候它足够用了，但是如果你需要一个真实的Python 列表对象，可以对它调用`list()`，这将会对查询集求值。

例如：`school.objects.filter(school_id=1).calues_list('id',"flat=True")`

named参数如下：

![image-20200714201611155](/Users/coder_li/DayDayUp/dayup/value_list.png)

上述orm解释：

查找School表中school_id为1的id，这将返回一个id列表，而不是单个id元组列表。差异巨大，values_list速度更快。flat = true使得它更快，因为python不需要实例化列表中的所有对象，只返回数据库值。为了证明它更快，因为Django认识到我们使用查询集作为查询集的参数，因此它将它们组合到一个查询中 - 它不会首先将查询集计算values_list为列表,有一点需要注意的是，列表理解中values / values_list的行为有所不同：

  + 如果该键是一个外键，并且在模型中设置里适当的关系，则列表理解将体用外键引用对象。

  +  values/values_list将产生存储在该字段中的实际值  

    #### Model.objects.bulk_create() 

    批量生成数据

    

    

    

    