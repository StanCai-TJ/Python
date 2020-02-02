    import pandas as pd
    import numpy as np
    import matplotlib.pyplot as plt
    from scipy import stats
    plt.rcParams['font.sans-serif']='SimHei'
    plt.rcParams[‘axes.unicode_minus']=False
    import seaborn as sns
    sns.set(font='LiSu')

    mydata=pd.read_excel('地址')

## 散点图

relplot 默认散点图,style不同班组显示不同形状,hue颜色饱和度

    sns.relplot(x='质检成绩',y='平均处理时长',data=mydata,style='班组',hue='班组')

\t分隔符,sizes把点由小到大显示

    newdata=pd.read_csv('iris.txt',sep='\t')
    sns.relplot(x='sepal.length',y='sepal.width',data=newdata,sytle='class',hue='class',sizes=(10,100))


## 抖动图---柱形散点图

    df=pd.read_excel('地址')
    sns.catplot(x='组别',y='月度接听量',data=df)

### 关闭抖动，一条直线

    df=pd.read_excel('地址')
    sns.catplot(x='组别',y='月度接听量',data=df,jitter=False)
    
### 每一个点都不重复，全部散开

    df=pd.read_excel('地址')
    sns.catplot(x='组别',y='月度接听量',data=df,hue='性别',kind='swarm')


