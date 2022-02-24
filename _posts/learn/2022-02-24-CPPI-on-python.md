---
layout: single
title: "[Python] CPPI 실습 on Python"
categories: learn
toc: true
---



# CPPI 실습 on Python

신한-KAIST 자산관리전문가과정

## 1. Parameter 설정


```python
initial_budget=10000
protection_floor=0.85
m=4 #multiplier
floor=initial_budget*protection_floor
rate=0.02 # yearly
```

## 2. Stock Price 데이터 불러오기 (S&P500)


```python
import pandas as pd
df=pd.read_excel('CPPI(data).xlsx', index_col=0)
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>sp500</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2000-01-31</th>
      <td>1394.46</td>
    </tr>
    <tr>
      <th>2000-02-29</th>
      <td>1366.42</td>
    </tr>
    <tr>
      <th>2000-03-31</th>
      <td>1498.58</td>
    </tr>
    <tr>
      <th>2000-04-28</th>
      <td>1452.43</td>
    </tr>
    <tr>
      <th>2000-05-31</th>
      <td>1420.60</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>2021-08-31</th>
      <td>4522.68</td>
    </tr>
    <tr>
      <th>2021-09-30</th>
      <td>4307.54</td>
    </tr>
    <tr>
      <th>2021-10-29</th>
      <td>4605.38</td>
    </tr>
    <tr>
      <th>2021-11-30</th>
      <td>4567.00</td>
    </tr>
    <tr>
      <th>2021-12-31</th>
      <td>4766.18</td>
    </tr>
  </tbody>
</table>
<p>264 rows × 1 columns</p>
</div>



## 3. 주식 수익률 계산


```python
stock_profit=[0]
for i in range(1, len(df)):
    stock_profit.append(df['sp500'][i]/ df['sp500'][i-1] -1)
    
df['stock_profit']=stock_profit
```


```python
stock_only_budget=[initial_budget]
for i in range(1, len(df)):
    stock_only_budget.append(stock_only_budget[i-1]*(1+df['stock_profit'][i]))
    
df['stock_only_budget']=stock_only_budget
```


```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>sp500</th>
      <th>stock_profit</th>
      <th>stock_only_budget</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2000-01-31</th>
      <td>1394.46</td>
      <td>0.000000</td>
      <td>10000.000000</td>
    </tr>
    <tr>
      <th>2000-02-29</th>
      <td>1366.42</td>
      <td>-0.020108</td>
      <td>9798.918578</td>
    </tr>
    <tr>
      <th>2000-03-31</th>
      <td>1498.58</td>
      <td>0.096720</td>
      <td>10746.668961</td>
    </tr>
    <tr>
      <th>2000-04-28</th>
      <td>1452.43</td>
      <td>-0.030796</td>
      <td>10415.716478</td>
    </tr>
    <tr>
      <th>2000-05-31</th>
      <td>1420.60</td>
      <td>-0.021915</td>
      <td>10187.456076</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2021-08-31</th>
      <td>4522.68</td>
      <td>0.028990</td>
      <td>32433.199948</td>
    </tr>
    <tr>
      <th>2021-09-30</th>
      <td>4307.54</td>
      <td>-0.047569</td>
      <td>30890.380506</td>
    </tr>
    <tr>
      <th>2021-10-29</th>
      <td>4605.38</td>
      <td>0.069144</td>
      <td>33026.261062</td>
    </tr>
    <tr>
      <th>2021-11-30</th>
      <td>4567.00</td>
      <td>-0.008334</td>
      <td>32751.029072</td>
    </tr>
    <tr>
      <th>2021-12-31</th>
      <td>4766.18</td>
      <td>0.043613</td>
      <td>34179.395608</td>
    </tr>
  </tbody>
</table>
<p>264 rows × 3 columns</p>
</div>



## 4. CPPI 계산


```python
budget=[initial_budget]
logs_cushion=[]
logs_stock=[]
logs_cma=[]

for i in range(len(df)):
    cushion=budget[i]-floor
    logs_cushion.append(cushion)
    
    stock_invest=min(budget[i], m*cushion)
    logs_stock.append(stock_invest)
    
    cma_invest=budget[i]-stock_invest
    logs_cma.append(cma_invest)
    
    if i != len(df)-1:
        budget.append(stock_invest*(1+df['stock_profit'][i+1]) + cma_invest*(1+rate/12))
```


```python
df['CPPI budget']=budget
df['floor']=floor
df['cusihon']=logs_cushion
df['stock_invest']=logs_stock
df['cma_invest']=logs_cma
df['stock_prop']=df['stock_invest']/df['CPPI budget']
```

## 5. 결과 시각화 및 파일 저장


```python
df # show final calculated data table
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>sp500</th>
      <th>stock_profit</th>
      <th>stock_only_budget</th>
      <th>CPPI budget</th>
      <th>floor</th>
      <th>cusihon</th>
      <th>stock_invest</th>
      <th>cma_invest</th>
      <th>stock_prop</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2000-01-31</th>
      <td>1394.46</td>
      <td>0.000000</td>
      <td>10000.000000</td>
      <td>10000.000000</td>
      <td>8500.0</td>
      <td>1500.000000</td>
      <td>6000.000000</td>
      <td>4000.000000</td>
      <td>0.600000</td>
    </tr>
    <tr>
      <th>2000-02-29</th>
      <td>1366.42</td>
      <td>-0.020108</td>
      <td>9798.918578</td>
      <td>9886.017813</td>
      <td>8500.0</td>
      <td>1386.017813</td>
      <td>5544.071253</td>
      <td>4341.946560</td>
      <td>0.560799</td>
    </tr>
    <tr>
      <th>2000-03-31</th>
      <td>1498.58</td>
      <td>0.096720</td>
      <td>10746.668961</td>
      <td>10429.476385</td>
      <td>8500.0</td>
      <td>1929.476385</td>
      <td>7717.905539</td>
      <td>2711.570846</td>
      <td>0.740009</td>
    </tr>
    <tr>
      <th>2000-04-28</th>
      <td>1452.43</td>
      <td>-0.030796</td>
      <td>10415.716478</td>
      <td>10196.316439</td>
      <td>8500.0</td>
      <td>1696.316439</td>
      <td>6785.265758</td>
      <td>3411.050682</td>
      <td>0.665462</td>
    </tr>
    <tr>
      <th>2000-05-31</th>
      <td>1420.60</td>
      <td>-0.021915</td>
      <td>10187.456076</td>
      <td>10053.302441</td>
      <td>8500.0</td>
      <td>1553.302441</td>
      <td>6213.209764</td>
      <td>3840.092677</td>
      <td>0.618027</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2021-08-31</th>
      <td>4522.68</td>
      <td>0.028990</td>
      <td>32433.199948</td>
      <td>31834.844961</td>
      <td>8500.0</td>
      <td>23334.844961</td>
      <td>31834.844961</td>
      <td>0.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>2021-09-30</th>
      <td>4307.54</td>
      <td>-0.047569</td>
      <td>30890.380506</td>
      <td>30320.488751</td>
      <td>8500.0</td>
      <td>21820.488751</td>
      <td>30320.488751</td>
      <td>0.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>2021-10-29</th>
      <td>4605.38</td>
      <td>0.069144</td>
      <td>33026.261062</td>
      <td>32416.964783</td>
      <td>8500.0</td>
      <td>23916.964783</td>
      <td>32416.964783</td>
      <td>0.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>2021-11-30</th>
      <td>4567.00</td>
      <td>-0.008334</td>
      <td>32751.029072</td>
      <td>32146.810505</td>
      <td>8500.0</td>
      <td>23646.810505</td>
      <td>32146.810505</td>
      <td>0.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>2021-12-31</th>
      <td>4766.18</td>
      <td>0.043613</td>
      <td>34179.395608</td>
      <td>33548.825333</td>
      <td>8500.0</td>
      <td>25048.825333</td>
      <td>33548.825333</td>
      <td>0.000000</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
<p>264 rows × 9 columns</p>
</div>




```python
from matplotlib import pyplot as plt
```


```python
plt.figure(figsize=(16,9))

plt.plot(df.index, df['stock_only_budget'])
plt.plot(df.index, df['CPPI budget'])
plt.plot(df.index, df['floor'])

plt.show()
```


​    ![output_15_0](../../assets/images/2022-02-24-CPPI-on-python/output_15_0.png)



```python
plt.figure(figsize=(16,9))

plt.plot(df.index, df['stock_prop'])

plt.show()
```

 

 ![output_16_0](../../assets/images/2022-02-24-CPPI-on-python/output_16_0.png)



```python
df.to_excel('CPPI_calculated.xlsx')
```

## FAQ

코드에 대한 질문은 본 포스팅 아래 댓글로 남겨주시면 최대한 답변드릴 수 있도록 하겠습니다.
