### 地址的读取

可以输入r，\

### 指定sheet

    pd.read_excel("",sheet_name='')

### 选取多列

两个中括号

    df2=df1[['列名1'，‘列名2’]]

### 列的条件选择

    df3=df1[df1.工资>3000]
  
    df3=df1[(df1.工资>3000)&(df1.教育程度)=='大学']
  
### 隐形筛选

不需要工资一列，注意双中括号

    df3=df1[df1.工资>3000][['姓名','性别','教育程度']]
  
### 反向筛选

    df3=df1.drop('性别',1)---操作列，取消性别列，0操作-行
  
### 去掉多列

    df3=df1.drop(['性别','教育程度'],1)
  
### loc/iloc

0到5行

    df.loc[0:5] 

取1，3，5行

    df.loc[[1,3,5]]  

取1，3，5行的姓名、年龄、教育程度，列只能用列名，不能用序号，与iloc相反

    df.loc[[1,3,5],['姓名','年龄','教育程度']] 

1到5，不包含5，0，1，2列，不包含3，左闭右开。<=      <

    df.iloc[1:5,0:3] 

指定

    df.iloc[[0,5,10],[0,5,8]] 
  
### 数据透视表

班组 y轴  教育程度x轴

    tatble=pd.pivot_table(mydata,index='班组',columns='教育程度'，values='工资',fill_value=0).round(2)

    tatble=pd.pivot_table(mydata,index=['班组','性别'],columns=['教育程度','居住地']，values='工资',fill_value=0).round(2)

查看value的平均数 aggfunc

    tatble=pd.pivot_table(mydata,index=['班组','性别']，values='工资',aggfuuc='mean',fill_value=0).round(2)

    tatble=pd.pivot_table(mydata,index=['班组','性别']，values=['工资','在职时长'],aggfuuc='mean',fill_value=0).round(2)

    tatble=pd.pivot_table(mydata,index=['班组','性别']，values=['工资','在职时长'],aggfuuc=['mean','max'],fill_value=0).round(2)

两对

    tatble=pd.pivot_table(mydata,index=['班组','性别']，values=['工资','在职时长'],aggfuuc={'工资':'mean','在职市场':'max'},fill_value=0).round(2)

注意里面的单双引号以及双等号

    tabble.query('性别=="女"')


### groupby

    table=mydata.groupby('班组')

如何查看

    for 班组,班组_df in table:

        print(班组)
            
        print（班组_df）

求均值
            
    table=mydata.groupby('班组') .mean().round(2)
          
多层

    table2=mydata.groupby(['班组','性别']) .mean().round(2)
        
单独某列、两列数据

    table3=mydata.groupby(['班组','性别']) .质检成绩.mean().round(2)

    table4=mydata.groupby(['班组','性别']) .['质检成绩','月度接听量'].mean().round(2)         
          
    table5=mydata.groupby(['班组','性别']) .质检成绩.agg(functions)
    
生成柱形图
    
    table6=mydata.groupby(['班组','性别']) .质检成绩.mean().plot(kind='bar')
    
    
### 相关性分析的一个思路
      
    import pandas as pd

    df = pd.DataFrame([ ["hello there", 100],
                        ["hello kid",   95],
                        ["there kid",   5]
                      ], columns = ['Sentence','Score'])

    s_corr = df.Sentence.str.get_dummies(sep=' ').corrwith(df.Score/df.Score.max())
    print (s_corr)
    
hello    0.998906
kid     -0.539949
there   -0.458957

### 快速解决百分比格式的方法

    data.A.apply(lambda x:format(x,'.2f%'))

### Pandas Query的查询用法

    data.query('班组==1 & 性别=="男"')
    #输入互动查询的一种方法
    group=input('请输入班组：')
    gender=input('请输入性别：')
    data.query('班组==@group & 性别==@gender')
    
