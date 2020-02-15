    import pandas as pd
    import numpy as np
    import matplotlib.pyplot as plt
    from scipy import stats
    plt.rcParams['font.sans-serif']=['SimHei']
    plt.rcParams['axes.unicode_minus']=False
    import seaborn as sns
    sns.set(font='LiSu')


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
    
## 箱线图与提琴图

    import pandas as pd
    import numpy as np
    import matplotlib.pyplot as plt
    from scipy import stats
    plt.rcParams['font.sans-serif']=['SimHei']
    plt.rcParams['axes.unicode_minus']=False
    import seaborn as sns
    sns.set(font='LiSu')
    
### 箱线图,hue用来区分，例如男女
    df=read_excel('')
    sns.catplot(x='班组',y='月度接听量',kind='box',hue='性别')
### 提琴图,split不分成两张图，在一张图上用两种颜色区分
    sns.catplot(x='班组',y='月度接听量',kind='violin',hue='性别',split=True)
    
## 柱形图

ci-confidence interval,默认是均值,estimator可以改为max,min,sum

    sns.catplot(x='班组',y='月度接听量',data=df,kind='bar',ci=None,estimator=min,color='r',hue='性别')
    
## 条形图
orient='h'横

    sns.catplot(x='月度接听量',y='班组',data=df,kind='bar',ci=None,estimator=min,color='r',hue='性别',orient='h')
    
## 点图

    sns.catplot(x='班组',y='月度接听量',data=df,kind='point',ci=None,hue='性别')
    
## 多重图表
画布多个子图
2张图表

    sna.catplot(x='组别',y='月度接听量',data=df,kind='swarm',col='性别')
    
3张图表

    sna.catplot(x='组别',y='月度接听量',data=df,kind='swarm',col='客户满意度')
    
6张图表:height*aspect=宽
    
    sna.catplot(x='组别',y='月度接听量',data=df,kind='swarm',col='客户满意度'，row='性别',height=2,aspect=2)
    
## 折线图

    import pandas as pd
    import numpy as np
    import matplotlib.pyplot as plt
    from scipy import stats
    plt.rcParams['font.sans-serif']=['SimHei']
    plt.rcParams['axes.unicode_minus']=False
    import seaborn as sns
    sns.set(font='LiSu')
    #dashes虚线
    sns.relplot(x='日期',y='话量',data=df,kind='line'，ci=None,hue='话型',style='话型',dashes=True,markers,markers=True)
    
## 直方图和密度图

hist是否有柱子,kde是否有折线,rug=True密度情况，fit正态分布曲线

    sns.distplot(df.月度接听量,bins=25,hist=True,kde=True,rug=False,color='g',fit=ststs.norm)
    
密度情况,shade面积情况,alpha透明情况
两组数据

    sns.kdeplot(df.月度接听量[df.组别==1],shade=True,color='r',alpha=0.3,label='班组1')
    sns.kdeplot(df.月度接听量[df.组别==2],shade=True,color='g',alpha=0.3,label='班组2')
    
两个数据量,cbar增加颜色指示条

    sns.kdeplot(df.月度接听量,df.平均处理时长,shade=True,color='blue',alpha=0.8,cbar=True)
    
## 热力图

annot显示具体数据,.0f没有小数点,cmap配色

    sns.heatmap(df,annot=True,fmt='.0f',cmpa='rainbow')
    sns.heatmap(df,annot=True,fmt='.0f',cmpa='Greens')
    
透视

    df1=pd.read_excel('D:/Software/Project1/质检数据分析.xlsx')
    df2=df1.pivot_table(index='组别',columns='差错量',values='月度接听量',aggfunc='max')
    sns.heatmap(df2,annot=True,fmt='.0f',cmap='summer')
    
相关系数热力图

    sns.heatmap(df1.corr(),cmap='blues')
    
## 雷达图

    import pandas as pd
    import numpy as np
    import matplotlib.pyplot as plt
    from scipy import stats
    plt.rcParams['font.sans-serif'] = ['SimHei']
    plt.rcParams['axes.unicode_minus'] = False
    import seaborn as sns
    sns.set(font='LiSu')
    df = pd.read_excel('./质检数据分析.xlsx')
    df1 = df.groupby('组别').月度接听量.mean().astype('int')
    #准备标签和数据
    labels=np.array(['一组','二组','三组','四组','五组'])
    values=np.array(df1)
    #endpoint 没有终点
    angles=np.linspace(0,2*np.pi,len(labels),endpoint=False)
    axises=np.concatenate((angles,[angles[0]]))
    values=np.concatenate((values,[values[0]]))
    #projection投射,lw线的宽度,alpha透明度
    ax=plt.subplot(111,projection='polar')
    ax.plot(axises,values,'m-',lw=1,alpha=0.5)
    #填充
    ax.fill(axises,values,'b',alpha=0.5)
    #axises*180/np.pi定位度数，贴上标签
    ax.set_thetagrids(axises*180/np.pi,labels)
    #调整y轴刻度
    ax.set_ylim(0,3000)
    #调整起始点位置，从正北开始
    ax.set_theta_zero_location('N')
    #pad标题的距离
    ax.set_title('月度接听量均值对比',fontsize=20,pad=20)
    #图要显示全部
    plt.tight_layout()
