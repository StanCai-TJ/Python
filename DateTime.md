timedelta的换算

    data['DATEDIFF']=data['DATEDIFF'].dt.days

## busday_count的使用

#### Pandas日期计算
    
    #将B的日期+时间的格式改为日期格式
    data['B']=pd.to_datetime(data['B']).dt.normalize()
    data['A']=pd.to_datetime(data['A'])
    data['DATEDIFF']=np.busday_count(data['A'].values.astype('datetime64[D]'),data['B'].values.astype('datetime64[D]'))
    
