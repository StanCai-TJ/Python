# 销售数据分析---学习笔记2020/01

## 获取数据、观察数据

---open certain sheet

xls.parse('sheet1')

---step 1,2,3...

data.shape

data.index

data.columns

data.count()

## 数据清洗

数据清洗过程包括：选择子集、列名重命名、缺失数据处理、数据类型转换、数据排序及异常值处理

### 1.选择子集

选择需要分析的列，去掉不需要分析的列，暂不需要

### 2.列名重命名

有一些列名容易有歧义，不好理解，对有歧义的列名重新命名。

data.rename(columns=('改动前':'改动后'),inplace=True)

### 3.缺失数据处理

处理方法：1，删除含有缺失值的数据；2，补全缺失记录。

---统计各列缺失值的数量

data.isnull().sum()

---查看是否存在缺失值

data.isnull().any()

若缺失值是null，则需要先进行替换

data=data.replace('null',np.NaN)

注：replace语法

data.replace(preivous,now,times)

times即最多替换次数

#### 删除缺失数据

data = data.dropna(subset=['列名1','列名2']，how='any')

####  缺失值填充

data.fillna('NULL') 用NULL补充

### 4.数据类型转换

原始保存数据是object结构，但某些列需要用到数字类型。




