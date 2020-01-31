# 图形图标

##柱形图

matplotlib

    import matplotlib.pyplot as plt
    from matplotlib import style
    ---中文字体问题
    plt.rcParams['font.sans-serif']='SimHei'
    plt.rcParams[‘axes.unicode_minus']=False
    plt.style.use('ggplot')
    
x轴，y轴，align对齐方式

    plt.bar(mydata.姓名,mydata.月度接听量)
    plt.bar(mydata.姓名,mydata.月度接听量，color='grey',width=0.5,align='center')
    ---横轴，纵轴，表名，图例
    plt.xlabel('姓名')
    plt.ylabel('月度接听量')
    plt.title('月度接听量',fontsize=16)
    ---注意图例的特殊括号及逗号标记！！！
    plt.legend(('月度接听量',)loc='upper left')
    
    
