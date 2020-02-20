timedelta的换算

    data['DATEDIFF']=data['DATEDIFF'].dt.days

## busday_count的使用

#### 日期计算
np.busday_count常规使用
    
    #将B的日期+时间的格式改为日期格式
    data['B']=pd.to_datetime(data['B']).dt.normalize()
    data['A']=pd.to_datetime(data['A'])
    data['C']=np.busday_count(data['A'].values.astype('datetime64[D]'),data['B'].values.astype('datetime64[D]'))
    
np.busday_count，使用holidays参数

    holidays_list=['2020-02-20','2020-02-21']
    data['C']=np.busday_count(data['A'].values.astype('datetime64[D]'),data['B'].values.astype('datetime64[D]'),holidays=holidays_list)
    
np.busday_count，使用weekmask,holidays参数处理调休问题 (常规weekmask='1111100')

    holidays_list=['2020-02-20']
    data['C']=np.busday_count(data['A'].values.astype('datetime64[D]'),data['B'].values.astype('datetime64[D]'),weekmask='1111111',holidays=holidays_list)
    
    
