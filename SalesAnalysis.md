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

原始保存数据是object结构，但某些列需要用到数字类型或分割数据。

#### 数据类型转换

    data['列名']=data['列名'].astype('float')

#### 分割数据

对某列进行特殊处理。

例：2020-01-01 星期一    只保留日期，取消星期一。

方法一：

    def split_time(timeadd):

        time_list=[]

        for v in time_add:
        
            data=v.spilt(' ')[0]

            time_list.append(data)
            
        time_series=Series(timelist)
        
        return time_series
        
    time=data.loc[:,'销售时间']
    
    data=split_time(time)
    
    data.loc[:,'销售时间']=data
    
方法二：

    f=lambda x:x.split(' ').[0]
    
    data[:,'销售时间']=data[:,'销售时间'].map(f)
    

#### 数据转换为日期格式

    data.loc[:,'销售时间']=pd.to_datatime(data.loc[:,'销售时间'],format='%Y-%m-%d',errors='coerce')
    
由于转换格式后，可能会出现不符合格式的日期，需要进行drop处理。

    data = data.dropna(subset=['列名1','列名2']，how='any')
    
### 5.数据排序

    data = data.sort_values(by='销售时间',ascending=True)
    
    #重置索引
    
    data = data.reset_index(drop=True)
    
### 6.异常值处理

    # 将"销售数量"这一列中小于0的数排除掉
    
    pop = data.loc[:,'销售数量'] > 0
    
    data = data.loc[pop,:]
    
    或
    
    above_zero= data['销售数量'].map(lambda x: x>0)
    
    data = data['销售数量'][above_zero]
    
## 数据分析

---在操作之前先复制一份数据，防止影响清洗后的数据

    groupDF = data
    
---以时间为轴进行分析，注意index问题
    
    groupDf.index = groupDf['销售时间']

---对列进行运算

    totalMoney = data.loc[:,'实收金额'].sum()
    
---画图时用于显示中文字符

    from pylab import mpl

    mpl.rcParams['font.sans-serif'] = ['SimHei'] # SimHei是黑体的意思
    
---将销售时间聚合按月分组
    
    gb = groupDf.groupby(groupDf.index.month)
    
    monthDf = gb.sum()
    
---groupby两列数据

    sales = groupDf[['商品名称','销售数量']]
    
    bk = sales.groupby('商品名称')[['销售数量']]
    
    re_medicine = bk.sum()
    
### 新增一列计算利润率

---对于两列运算，新增一列数据的运算

    data1 = data['利润额']/data['销售额']
    
    data['利润率'] = data1.apply(lambda x : format(x,'.2%'))
    
    
    
    
    
    
    
    

    
    

    


        
        
        
        


    
    

