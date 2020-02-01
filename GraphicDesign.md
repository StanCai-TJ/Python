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
