# 图形图标

## 柱形图

matplotlib

基础导入及中文文字设置

    import matplotlib.pyplot as plt
    from matplotlib import style
    ---中文字体问题
    plt.rcParams['font.sans-serif']='SimHei'
    plt.rcParams[‘axes.unicode_minus']=False
    plt.style.use('ggplot')
    
x轴，y轴，align对齐方式

    plt.bar(mydata.姓名,mydata.月度接听量)
    plt.bar(mydata.姓名,mydata.月度接听量，color='grey',width=0.5,align='center')
    -横向
    plt.barh(mydata.姓名,mydata.月度接听量，color='grey',height=0.5,align='center')
    ---横轴，纵轴，表名，图例
    plt.xlabel('姓名')
    plt.ylabel('月度接听量')
    plt.title('月度接听量',fontsize=16)
    ---注意图例的特殊括号及逗号标记！！！
    plt.legend(('月度接听量',)loc='upper left')
    
    
## 簇状柱形图

    import matplotlib.pyplot as plt
    from matplotlib import style
    ---中文字体问题
    plt.rcParams['font.sans-serif']='SimHei'
    plt.rcParams[‘axes.unicode_minus']=False
    plt.style.use('ggplot')
---    
    mydata=pd.read_excel('...')
    
 ---第一种方法(推荐)
 
    mydata.plot.bar(x='Month',y=['Year2018','Year2019'],color=['green','orange'],title='年度对比')
    
---第二种方法

    plt.bar(np.arange(len(mydata.Month)),mydata.Year2018,color='green',width=0.25)
    plt.bar(np.arange(len(mydata.Month))+0.25,mydata.Year2019,color='grey',width=0.25)
    更改横轴标签，生成12个点位，铺上12个月份
    plt.xticks(arange(12),mydata.Month,rotation=75)

## 堆积柱形图/条形图

    plt.bar(np.arange(len(mydata.Month)),mydata.Year2018,color='green',width=0.5)
    
    #bottom是以谁为底

    plt.bar(np.arange(len(mydata.Month)),mydata.Year2019,color='grey',width=0.5，bottom=mydata.Year2018)
    plt.xticks(arange(12),mydata.Month,rotation=75)
    
---横向
        
    plt.barh(np.arange(len(mydata.Month)),mydata.Year2018,color='green',height=0.5)
    plt.barh(np.arange(len(mydata.Month)),mydata.Year2019,color='grey',height=0.5，left=mydata.Year2018)
    plt.yticks(arange(12),mydata.Month,rotation=75)
    
## 饼图
 
labeldistance默认是1，0.8在饼内部,radius默认大小是1,startangle角度,counterclock默认顺序,explode第一块默认取出来,shadow阴影,colors颜色,axis修正坐标轴

    x=data.groupby('班组').姓名.count()
    plt.pie(x,labels=['一组','二组','三组','四组','五组'],autopct='%.2f%%',labeldistance=0.8，radius=0.8,startangle=-270,counterclock=False,explode=[0.1,0,0,0,0],shadow=True,colors=['r','g','b','grey','y'])
    plt.axis('equal')
    
## 圆环图

edgecolor边缘颜色，pctdistance在饼的内部还是外部显示，width越小，孔径越大

    plt.pie(x,labels=['一组','二组','三组','四组','五组'],autopct='%.2f%%',wedgeprops=dict(width=0.5,edgecolor='w'),radius=1,pctdistance=0.85)
    
## 两个圆环图

    plt.pie(x,labels=['一组','二组','三组','四组','五组'],autopct='%.2f%%',wedgeprops=dict(width=0.5,edgecolor='w'),radius=1,pctdistance=0.85)
    plt.pie(x,autopct='%.2f%%',wedgeprops=dict(width=0.7,edgecolor='w'),radius=0.7,pctdistance=0.75)  
    
## 折线图

maker指点的形状,linestyle线的形式，linewidth宽度,gca-get current axis

    plt.plot(mydata.Month,mydata.Year2018,color='red',marker='o',markersize=6,linestyle='--',linewidth=5)
    plt.plot(mydata.Month,mydata.Year2019,color='green',marker='o',markersize=6,linestyle='--',linewidth=5)
    
----画在两张图上，4个图，第三个数字1-4

    plt.subplot(2,1,1)
    plt.plot(mydata.Month,mydata.Year2018,color='red',marker='o',markersize=6,linestyle='--',linewidth=5)
    plt.ylim(0,3100)
    ax=plt.gca()
    ax.yaxis.set_major_locator(MultipleLocator(500))
    #为点添加数值标记a,b,b,第三个表示要标签要加的数值，即Year2018
    for a,b in zip(mydata.Month,mydata.Year2018)
        plt.text(a,b,b,ha='left',va='bottom',fontsize=10)
    plt.subplot(2,1,2)
    plt.plot(mydata.Month,mydata.Year2019,color='green',marker='o',markersize=6,linestyle='--',linewidth=5)
    plt.ylim(0,3100)
    ax=plt.gca()
    ax.yaxis.set_major_locator(MultipleLocator(500))
    for a,b in zip(mydata.Month,mydata.Year2019)
        plt.text(a,b,b,ha='left',va='bottom',fontsize=10)
        
---get current axis 给坐标轴设置坐标间隔

    #取出坐标轴
    ax=plt.gca()
    ax.yaxis.set_major_locator(MultipleLocator(500))
    
## 散点图
    
    import matplotlib.pyplot as plt
    from matplotlib import style
    ---中文字体问题
    plt.rcParams['font.sans-serif']='SimHei'
    plt.rcParams[‘axes.unicode_minus']=False
    plt.style.use('ggplot')
    plt.scatter(mydata.Year2018,mydata.Year2019,marker='o',color='b',edgecolor='r')
    ---为图上的点添加数值标记
    for a,b,c in zip(mydata.Year2018,mydata.Year2019,mydata.Month)
    ---va字和点的位置,加c的数值，即mydata.Month
        plt.text(a,b,c,ha='left',va='bottom',fontsize=11)

## 直方图叠加正太分布曲线

    import pandas as pd
    import numpy as np
    import matplotlib.pyplot as plt
    from matplotlib import style
    ---中文字体问题
    plt.rcParams['font.sans-serif']='SimHei'
    plt.rcParams[‘axes.unicode_minus']=False
    plt.style.use('ggplot')
    from scipy.stats import norm
    #生成数据，normal第一个是均值，第二个是标准差,第三个是数据量
    data=np.random.normal(180,5,1000)
    #直方图,bins几个柱子,rwidth柱子间的间隙,默认是1，没有间隔,density，如果要正太分布曲线，就必须添加
    #或者bins=[160,170,180,190,200]或者bins='auto'
    plt.hist(data,bins=30,rwidth=0.95,color='grey',density=True)
    #取最小最大值,pdf概率密度函数
    xmin,xmax=plt.xlim()
    #切100个点
    x=np.linspace(xmin,xmax,100)
    #均值180，间隔5
    p=norm.pdf(x,180,5)
    plt.plot(x,p,color='r',linwidth=2)
    
    
## 箱线图
    
    import pandas as pd
    import numpy as np
    import matplotlib.pyplot as plt
    from matplotlib import style
    ---中文字体问题
    plt.rcParams['font.sans-serif']='SimHei'
    plt.rcParams[‘axes.unicode_minus']=False
    plt.style.use('ggplot')
    from scipy.stats import norm
    #boxprops箱子设计,字典形式
    plt.boxplot(mydata.月度接听量,patch_artist=True,boxprops=dict(linestyle='-',linewidth=1,color='black',facecolor='orange'))

几种不同的数据

    plt.boxplot([mydata.客户满意率,mydata.首解率,mydata.工时利用率],patch_artist=True,boxprops=dict(linestyle='-',linewidth=1,color='black',facecolor='orange'))
        
生成5张图
        
    newdata=np.random.normal(180,20,[1000,4])
    plt.boxplot(newdata,patch_artist=True,boxprops=dict(linestyle='-',linewidth=1,color='black',facecolor='orange')) 
     
    #直接生成5个班组的箱线图，最实用！
    mydata.boxplot('月度接听量',by='班组',patch_artist=True,boxprops=dict(linestyle='-',linewidth=1,color='black',facecolor='orange'))
     
     
    #箱子变形，中间窄notch=True
    plt.boxplot([mydata.客户满意率,mydata.首解率,mydata.工时利用率],notch=True,patch_artist=True,boxprops=dict(linestyle='-',linewidth=1,color='black',facecolor='orange'))
    
