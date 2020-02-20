timedelta的换算

    data['DATEDIFF']=data['DATEDIFF'].dt.days

busday_count的使用

    #Pandas日期计算
    data['B']=pd.to_datetime(data['B']).dt.normalize()
    data['A']=pd.to_datetime(data['A'])
      data['DATEDIFF']=np.busday_count(data['DATE_DETECT'].values.astype('datetime64[D]'),data['DTIME_IV_LAST_MODIFIED'].values.astype('datetime64[D]'))
