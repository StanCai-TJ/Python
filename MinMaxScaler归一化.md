##归一化处理

(N-MIN)/(MAX-MIN)

MinMaxScaler方法

    import pandas as pd
    from sklearn.preprocessing import MinMaxScaler

    data = pd.read_excel('./jan.xlsx')

    scaler_2 = MinMaxScaler()

    data['A_Z'] = scaler_2.fit_transform(data['A'].values.reshape(-1,1))

    print(data['A_Z'])
