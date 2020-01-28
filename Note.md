# Python学习笔记

##  缺失值的处理

---统计各列缺失值的数量

data.isnull().sum()

---查看是否存在缺失值

data.isnull().any()

若缺失值是null，则需要先进行替换

data=data.replace('null',np.NaN)

注：replace语法

data.replace(preivous,now,times)

times即最多替换次数

## 销售数据分析20200128

---open certain sheet
xls.parse('sheet1')

---step 1,2,3...

data.shape

data.index

data.columns

data.count()

## 数据清洗

数据清洗过程包括：选择子集、列名重命名、缺失数据处理、数据类型转换、数据排序及异常值处理

### 选择子集
