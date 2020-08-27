### 1 loc与iloc函数

pandas中操作DataFrame时候，经常用到**loc,iloc,at,iat,ix**

loc函数通过行索引“index"中具体的值来去行的数据（如取”index“为'A'的行）

iloc函数：通过行数来去行的数据（如取第二行的数据）

```python
import numpy as np
import pandas as pd
#创建一个Dataframe
data=pd.DataFrame(np。arange(16).reshape(4,4),index=list('abcd'),columns=list('ABCD'))
In [16]: data
Out[16]:
    A   B   C   D
a   0   1   2   3
b   4   5   6   7
c   8   9  10  11
d  12  13  14  15
```

##### 1.1  利用loc与iloc取行数据

```python
data.loc['a']#取索引为a的行
In [17]: data.loc['a']
Out[17]:
A    0
B    1
C    2
D    3
Name: a, dtype: int64
    
data.iloc[0]#取第一行数据,索引为'a'的行就是第一行，所以结果相同
In [18]: data.iloc[0]
Out[18]:
A    0
B    1
C    2
D    3
Name: a, dtype: int64

```



##### 1.2   利用loc,iloc取列数据

```python
data.loc[:,['A']] #取A列所有行，取多列的格式为data.loc[:,['A'，‘B’，‘C’，...]]

In [19]: data.loc[:,['A']]
Out[19]:
    A
a   0
b   4
c   8
d  12
Data.iloc(:,[0])#取第0列的所有行，索取几列的格式为data.iloc[:,[0,1,2..]]
In [20]: data.iloc[:,[0]]
Out[20]:
    A
a   0
b   4
c   8
d  12
```

##### 1.3  利用loc,iloc提取指定行、指定列数据

```python
In [22]: data.loc[['a','b'],['A','B']]#提取index为‘a’,‘b’，列名为‘A’，‘B’的数据
Out[22]:
   A  B
a  0  1
b  4  5

In [23]: data.iloc[[0,1],[0,1]]#提取0,1行，第0，1列中的数据
Out[23]:
   A  B
a  0  1
b  4  5

```

##### 1.4  利用loc,iloc提取所有数据

```python
In [25]: data.loc[:,:]#提取A,B,C,D列的所有行
Out[25]:
    A   B   C   D
a   0   1   2   3
b   4   5   6   7
c   8   9  10  11
d  12  13  14  15

In [26]: data.iloc[:,:]#提取0,1,2,3列的所有行
Out[26]:
    A   B   C   D
a   0   1   2   3
b   4   5   6   7
c   8   9  10  11
d  12  13  14  15
```

##### 1.5  利用loc函数，根据某个数据来提取数据所在的行

```python
In [28]: data.loc[data['A']==0]#提取data数据（筛选条件：A列中数字为0所在的行数据）
Out[28]:
   A  B  C  D
a  0  1  2  3

In [32]: data.loc[(data['A']==0)&(data['B']==1)]#提取data数据（多个筛选条件）
Out[32]:
   A  B  C  D
a  0  1  2  3
```



利用loc函数的时候，当index相同时，会将index全部提取出来，优点：如果index是人名，数据框为所有人的数据，那么我可以将某人的多条数据提取分析；缺点：如果index不具有特定意义，而且重复，那么提取数据需要进一步处理，可以用.reset_index()函数重置index.