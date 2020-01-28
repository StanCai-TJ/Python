# Python学习笔记

##  1,缺失值的处理

---统计各列缺失值的数量

data.isnull().sum()

---查看是否存在缺失值

data.isnull().any()

若缺失值是null，则需要先进行替换

data=data.replace('null',np.NaN)

注：replace语法

data.replace(preivous,now,times)

times即最多替换次数

