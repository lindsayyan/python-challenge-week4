
## Python week4 Homework
### Loading data in 


```python
filename = 'purchase_data.json.txt' 
df=open(filename,'r')
df_list = df.readline()
```


```python
import json
from pprint import pprint
df_json = json.loads(df_list)
pprint(df_json)
```


```python
import pandas as pd
df_json2=pd.DataFrame(df_json)
df_json2.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
    </tr>
  </tbody>
</table>
</div>




```python
Total_players=len(df_json2['SN'].value_counts())
number_unique_items=len(df_json2['Item ID'].value_counts())
avg_price=df_json2['Price'].mean()
total_revenue=df_json2['Price'].sum()
```

### Purchasing Analysis


```python
pur_ana=[Total_players,number_unique_items,avg_price,total_revenue]
pur_title=['Total_players','number_unique_items','avg_price','total_revenue']
pur_ana2=pd.DataFrame(pur_ana)
pur_title2=pd.DataFrame(pur_title)
pur_ana_final=pd.concat([pur_title2,pur_ana2],axis=1)
pur_ana_final
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Total_players</td>
      <td>573.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>number_unique_items</td>
      <td>183.000000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>avg_price</td>
      <td>2.931192</td>
    </tr>
    <tr>
      <th>3</th>
      <td>total_revenue</td>
      <td>2286.330000</td>
    </tr>
  </tbody>
</table>
</div>




```python
Male=df_json2[df_json2['Gender']=='Male']
Male2=len(Male['SN'].value_counts())
Female=df_json2[df_json2['Gender']=='Female']
Female2=len(Female['SN'].value_counts())
Other=df_json2[df_json2['Gender']=='Other / Non-Disclosed']
Other2=len(Other['SN'].value_counts())
```


```python
percent_male=Male2/Total_players*100
percent_female=Female2/Total_players*100
percent_other=Other2/Total_players*100
```


```python
##Male
male_purchase_count=len(Male)
male_avg_price=Male['Price'].mean()
male_total_purchase=Male['Price'].sum()
normalized_total_male=male_total_purchase/male_purchase_count
##Female
female_purchase_count=len(Female)
female_avg_price=Female['Price'].mean()
female_total_purchase=Female['Price'].sum()
normalized_total_female=female_total_purchase/female_purchase_count
```

### Gender Summary


```python
male=[male_purchase_count,male_avg_price,male_total_purchase,normalized_total_male]
female=[female_purchase_count,female_avg_price,female_total_purchase,normalized_total_female]
title=['purchase_count','avg_price','total_purchase','normalized_total']
male2=pd.DataFrame(male)
female2=pd.DataFrame(female)
title2=pd.DataFrame(title)
Gender_summary=pd.concat([title2,male2,female2],axis=1)
Gender_summary.columns=(['columns','male','female'])
Gender_summary
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>columns</th>
      <th>male</th>
      <th>female</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>purchase_count</td>
      <td>633.000000</td>
      <td>136.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>avg_price</td>
      <td>2.950521</td>
      <td>2.815515</td>
    </tr>
    <tr>
      <th>2</th>
      <td>total_purchase</td>
      <td>1867.680000</td>
      <td>382.910000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>normalized_total</td>
      <td>2.950521</td>
      <td>2.815515</td>
    </tr>
  </tbody>
</table>
</div>



### Age Demographics


```python
##binning
bins=[7,16,25,36,45]
group_names = ['7-16', '17-25', '26-36','37-45']
```


```python
df_json2['Buckets']=pd.cut(df_json2['Age'],bins,labels=group_names)
```


```python
count_items= df_json2.groupby('Buckets').count()['Age']
Avg_pur_Price= df_json2.groupby('Buckets').mean()['Price']
Sum_pur_Price= df_json2.groupby('Buckets').sum()['Price']
```


```python
Summary=pd.concat([count_items,Avg_pur_Price,Sum_pur_Price],axis=1)
Summary.columns=['Count','AvgPrice','TotalPrice']
Summary
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Count</th>
      <th>AvgPrice</th>
      <th>TotalPrice</th>
    </tr>
    <tr>
      <th>Buckets</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>17-25</th>
      <td>466</td>
      <td>2.941288</td>
      <td>1370.64</td>
    </tr>
    <tr>
      <th>26-36</th>
      <td>141</td>
      <td>2.966099</td>
      <td>418.22</td>
    </tr>
    <tr>
      <th>37-45</th>
      <td>40</td>
      <td>2.899750</td>
      <td>115.99</td>
    </tr>
    <tr>
      <th>7-16</th>
      <td>114</td>
      <td>2.859737</td>
      <td>326.01</td>
    </tr>
  </tbody>
</table>
</div>



### Top Spenders


```python
Total_price_bySN=df_json2.groupby('SN').sum()['Price']
Total_count_bySN=df_json2.groupby('SN').count()['Age']
Avg_price_bySN=Total_price_bySN/Total_count_bySN
Top_spender=[Total_price_bySN,Total_count_bySN,Avg_price_bySN]
Top_spender2=pd.DataFrame(Top_spender)
Top_spender3=Top_spender2.T
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Price</th>
      <th>Age</th>
      <th>Unnamed 0</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Adairialis76</th>
      <td>2.46</td>
      <td>1.0</td>
      <td>2.460000</td>
    </tr>
    <tr>
      <th>Aduephos78</th>
      <td>6.70</td>
      <td>3.0</td>
      <td>2.233333</td>
    </tr>
    <tr>
      <th>Aeduera68</th>
      <td>5.80</td>
      <td>3.0</td>
      <td>1.933333</td>
    </tr>
    <tr>
      <th>Aela49</th>
      <td>2.46</td>
      <td>1.0</td>
      <td>2.460000</td>
    </tr>
    <tr>
      <th>Aela59</th>
      <td>1.27</td>
      <td>1.0</td>
      <td>1.270000</td>
    </tr>
    <tr>
      <th>Aelalis34</th>
      <td>5.06</td>
      <td>2.0</td>
      <td>2.530000</td>
    </tr>
    <tr>
      <th>Aelin32</th>
      <td>3.14</td>
      <td>1.0</td>
      <td>3.140000</td>
    </tr>
    <tr>
      <th>Aeliriam77</th>
      <td>6.72</td>
      <td>2.0</td>
      <td>3.360000</td>
    </tr>
    <tr>
      <th>Aeliriarin93</th>
      <td>2.04</td>
      <td>1.0</td>
      <td>2.040000</td>
    </tr>
    <tr>
      <th>Aeliru63</th>
      <td>8.98</td>
      <td>2.0</td>
      <td>4.490000</td>
    </tr>
    <tr>
      <th>Aellyria80</th>
      <td>4.32</td>
      <td>1.0</td>
      <td>4.320000</td>
    </tr>
    <tr>
      <th>Aellyrialis39</th>
      <td>3.15</td>
      <td>1.0</td>
      <td>3.150000</td>
    </tr>
    <tr>
      <th>Aellysup38</th>
      <td>3.61</td>
      <td>1.0</td>
      <td>3.610000</td>
    </tr>
    <tr>
      <th>Aelollo59</th>
      <td>1.55</td>
      <td>1.0</td>
      <td>1.550000</td>
    </tr>
    <tr>
      <th>Aenarap34</th>
      <td>1.65</td>
      <td>1.0</td>
      <td>1.650000</td>
    </tr>
    <tr>
      <th>Aenasu69</th>
      <td>3.27</td>
      <td>1.0</td>
      <td>3.270000</td>
    </tr>
    <tr>
      <th>Aeral43</th>
      <td>2.72</td>
      <td>1.0</td>
      <td>2.720000</td>
    </tr>
    <tr>
      <th>Aeral85</th>
      <td>4.25</td>
      <td>1.0</td>
      <td>4.250000</td>
    </tr>
    <tr>
      <th>Aeral97</th>
      <td>2.35</td>
      <td>1.0</td>
      <td>2.350000</td>
    </tr>
    <tr>
      <th>Aeri84</th>
      <td>6.60</td>
      <td>2.0</td>
      <td>3.300000</td>
    </tr>
    <tr>
      <th>Aerillorin70</th>
      <td>1.88</td>
      <td>1.0</td>
      <td>1.880000</td>
    </tr>
    <tr>
      <th>Aerithllora36</th>
      <td>10.45</td>
      <td>3.0</td>
      <td>3.483333</td>
    </tr>
    <tr>
      <th>Aerithnucal56</th>
      <td>3.18</td>
      <td>2.0</td>
      <td>1.590000</td>
    </tr>
    <tr>
      <th>Aerithnuphos61</th>
      <td>1.69</td>
      <td>1.0</td>
      <td>1.690000</td>
    </tr>
    <tr>
      <th>Aerithriaphos45</th>
      <td>2.38</td>
      <td>1.0</td>
      <td>2.380000</td>
    </tr>
    <tr>
      <th>Aesty51</th>
      <td>1.82</td>
      <td>1.0</td>
      <td>1.820000</td>
    </tr>
    <tr>
      <th>Aesur96</th>
      <td>4.66</td>
      <td>1.0</td>
      <td>4.660000</td>
    </tr>
    <tr>
      <th>Aethe80</th>
      <td>2.32</td>
      <td>1.0</td>
      <td>2.320000</td>
    </tr>
    <tr>
      <th>Aethedru70</th>
      <td>2.97</td>
      <td>1.0</td>
      <td>2.970000</td>
    </tr>
    <tr>
      <th>Aidain51</th>
      <td>6.84</td>
      <td>2.0</td>
      <td>3.420000</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Undjaskla97</th>
      <td>4.57</td>
      <td>1.0</td>
      <td>4.570000</td>
    </tr>
    <tr>
      <th>Undjasksya56</th>
      <td>4.53</td>
      <td>1.0</td>
      <td>4.530000</td>
    </tr>
    <tr>
      <th>Undotesta33</th>
      <td>3.90</td>
      <td>1.0</td>
      <td>3.900000</td>
    </tr>
    <tr>
      <th>Wailin72</th>
      <td>2.04</td>
      <td>1.0</td>
      <td>2.040000</td>
    </tr>
    <tr>
      <th>Whaestysu86</th>
      <td>4.08</td>
      <td>1.0</td>
      <td>4.080000</td>
    </tr>
    <tr>
      <th>Yadacal26</th>
      <td>1.93</td>
      <td>1.0</td>
      <td>1.930000</td>
    </tr>
    <tr>
      <th>Yadaisuir65</th>
      <td>8.56</td>
      <td>2.0</td>
      <td>4.280000</td>
    </tr>
    <tr>
      <th>Yadanun74</th>
      <td>9.09</td>
      <td>3.0</td>
      <td>3.030000</td>
    </tr>
    <tr>
      <th>Yalaeria91</th>
      <td>1.88</td>
      <td>1.0</td>
      <td>1.880000</td>
    </tr>
    <tr>
      <th>Yaliru88</th>
      <td>3.71</td>
      <td>1.0</td>
      <td>3.710000</td>
    </tr>
    <tr>
      <th>Yalo71</th>
      <td>2.41</td>
      <td>1.0</td>
      <td>2.410000</td>
    </tr>
    <tr>
      <th>Yalostiphos68</th>
      <td>2.37</td>
      <td>1.0</td>
      <td>2.370000</td>
    </tr>
    <tr>
      <th>Yaralnura48</th>
      <td>4.19</td>
      <td>2.0</td>
      <td>2.095000</td>
    </tr>
    <tr>
      <th>Yararmol43</th>
      <td>1.55</td>
      <td>1.0</td>
      <td>1.550000</td>
    </tr>
    <tr>
      <th>Yarirarn35</th>
      <td>2.88</td>
      <td>1.0</td>
      <td>2.880000</td>
    </tr>
    <tr>
      <th>Yaristi64</th>
      <td>1.24</td>
      <td>1.0</td>
      <td>1.240000</td>
    </tr>
    <tr>
      <th>Yarithllodeu72</th>
      <td>2.19</td>
      <td>1.0</td>
      <td>2.190000</td>
    </tr>
    <tr>
      <th>Yarithphos28</th>
      <td>2.35</td>
      <td>1.0</td>
      <td>2.350000</td>
    </tr>
    <tr>
      <th>Yarithsurgue62</th>
      <td>4.81</td>
      <td>2.0</td>
      <td>2.405000</td>
    </tr>
    <tr>
      <th>Yarmol79</th>
      <td>2.91</td>
      <td>1.0</td>
      <td>2.910000</td>
    </tr>
    <tr>
      <th>Yarolwen77</th>
      <td>6.98</td>
      <td>2.0</td>
      <td>3.490000</td>
    </tr>
    <tr>
      <th>Yasriphos60</th>
      <td>10.40</td>
      <td>3.0</td>
      <td>3.466667</td>
    </tr>
    <tr>
      <th>Yasrisu92</th>
      <td>2.60</td>
      <td>1.0</td>
      <td>2.600000</td>
    </tr>
    <tr>
      <th>Yasur35</th>
      <td>2.78</td>
      <td>1.0</td>
      <td>2.780000</td>
    </tr>
    <tr>
      <th>Yasur85</th>
      <td>2.04</td>
      <td>1.0</td>
      <td>2.040000</td>
    </tr>
    <tr>
      <th>Yasurra52</th>
      <td>3.14</td>
      <td>1.0</td>
      <td>3.140000</td>
    </tr>
    <tr>
      <th>Yathecal72</th>
      <td>7.77</td>
      <td>2.0</td>
      <td>3.885000</td>
    </tr>
    <tr>
      <th>Yathecal82</th>
      <td>2.41</td>
      <td>1.0</td>
      <td>2.410000</td>
    </tr>
    <tr>
      <th>Zhisrisu83</th>
      <td>2.46</td>
      <td>2.0</td>
      <td>1.230000</td>
    </tr>
    <tr>
      <th>Zontibe81</th>
      <td>3.71</td>
      <td>1.0</td>
      <td>3.710000</td>
    </tr>
  </tbody>
</table>
<p>573 rows × 3 columns</p>
</div>




```python
Top_spender3=Top_spender3.rename(columns={'Unnamed 0':'Ave_spend'})
```


```python
Top_spender3=Top_spender3.sort_values('Price',ascending=False)
Top_spender_summary=Top_spender3.head()
```


```python
Top_spender_summary.columns=(['Total_spend','Total_items','Avg_spend'])
Top_spender_summary
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total_spend</th>
      <th>Total_items</th>
      <th>Avg_spend</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Undirrala66</th>
      <td>17.06</td>
      <td>5.0</td>
      <td>3.412000</td>
    </tr>
    <tr>
      <th>Saedue76</th>
      <td>13.56</td>
      <td>4.0</td>
      <td>3.390000</td>
    </tr>
    <tr>
      <th>Mindimnya67</th>
      <td>12.74</td>
      <td>4.0</td>
      <td>3.185000</td>
    </tr>
    <tr>
      <th>Haellysu29</th>
      <td>12.73</td>
      <td>3.0</td>
      <td>4.243333</td>
    </tr>
    <tr>
      <th>Eoda93</th>
      <td>11.58</td>
      <td>3.0</td>
      <td>3.860000</td>
    </tr>
  </tbody>
</table>
</div>



### Most popular items


```python
df_json2.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
      <th>Buckets</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
      <td>37-45</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
      <td>17-25</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
      <td>26-36</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
      <td>17-25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
      <td>17-25</td>
    </tr>
  </tbody>
</table>
</div>




```python
#item_count=df_json2.groupby('Item Name').count()['Item ID']
#item_Purchase_total=df_json2.groupby('Item Name').sum()['Price']
item=df_json2[['Item Name','Price','Item ID']]
item=item.drop_duplicates(subset=None, keep='first', inplace=False)
item.index=item['Item Name']
item
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item Name</th>
      <th>Price</th>
      <th>Item ID</th>
    </tr>
    <tr>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bone Crushing Silver Skewer</th>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>165</td>
    </tr>
    <tr>
      <th>Stormbringer, Dark Blade of Ending Misery</th>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>119</td>
    </tr>
    <tr>
      <th>Primitive Blade</th>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>174</td>
    </tr>
    <tr>
      <th>Final Critic</th>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>92</td>
    </tr>
    <tr>
      <th>Stormfury Mace</th>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>63</td>
    </tr>
    <tr>
      <th>Sleepwalker</th>
      <td>Sleepwalker</td>
      <td>1.73</td>
      <td>10</td>
    </tr>
    <tr>
      <th>Mercenary Sabre</th>
      <td>Mercenary Sabre</td>
      <td>4.57</td>
      <td>153</td>
    </tr>
    <tr>
      <th>Interrogator, Blood Blade of the Queen</th>
      <td>Interrogator, Blood Blade of the Queen</td>
      <td>3.32</td>
      <td>169</td>
    </tr>
    <tr>
      <th>Ghost Reaver, Longsword of Magic</th>
      <td>Ghost Reaver, Longsword of Magic</td>
      <td>2.77</td>
      <td>118</td>
    </tr>
    <tr>
      <th>Expiration, Warscythe Of Lost Worlds</th>
      <td>Expiration, Warscythe Of Lost Worlds</td>
      <td>4.53</td>
      <td>99</td>
    </tr>
    <tr>
      <th>Despair, Favor of Due Diligence</th>
      <td>Despair, Favor of Due Diligence</td>
      <td>3.81</td>
      <td>57</td>
    </tr>
    <tr>
      <th>Alpha, Reach of Ending Hope</th>
      <td>Alpha, Reach of Ending Hope</td>
      <td>1.55</td>
      <td>47</td>
    </tr>
    <tr>
      <th>Dreamkiss</th>
      <td>Dreamkiss</td>
      <td>4.06</td>
      <td>81</td>
    </tr>
    <tr>
      <th>Piety, Guardian of Riddles</th>
      <td>Piety, Guardian of Riddles</td>
      <td>3.68</td>
      <td>77</td>
    </tr>
    <tr>
      <th>Bonecarvin Battle Axe</th>
      <td>Bonecarvin Battle Axe</td>
      <td>2.46</td>
      <td>44</td>
    </tr>
    <tr>
      <th>Blood-Forged Skeletal Spine</th>
      <td>Blood-Forged Skeletal Spine</td>
      <td>4.77</td>
      <td>96</td>
    </tr>
    <tr>
      <th>Twilight's Carver</th>
      <td>Twilight's Carver</td>
      <td>1.14</td>
      <td>123</td>
    </tr>
    <tr>
      <th>Lightning, Etcher of the King</th>
      <td>Lightning, Etcher of the King</td>
      <td>1.65</td>
      <td>59</td>
    </tr>
    <tr>
      <th>Celeste</th>
      <td>Celeste</td>
      <td>3.71</td>
      <td>91</td>
    </tr>
    <tr>
      <th>Winterthorn, Defender of Shifting Worlds</th>
      <td>Winterthorn, Defender of Shifting Worlds</td>
      <td>4.89</td>
      <td>177</td>
    </tr>
    <tr>
      <th>Glimmer, Ender of the Moon</th>
      <td>Glimmer, Ender of the Moon</td>
      <td>2.33</td>
      <td>78</td>
    </tr>
    <tr>
      <th>Phantomlight</th>
      <td>Phantomlight</td>
      <td>1.79</td>
      <td>3</td>
    </tr>
    <tr>
      <th>Brimstone</th>
      <td>Brimstone</td>
      <td>2.52</td>
      <td>11</td>
    </tr>
    <tr>
      <th>Dragon's Greatsword</th>
      <td>Dragon's Greatsword</td>
      <td>2.36</td>
      <td>183</td>
    </tr>
    <tr>
      <th>Conqueror Adamantite Mace</th>
      <td>Conqueror Adamantite Mace</td>
      <td>1.96</td>
      <td>65</td>
    </tr>
    <tr>
      <th>Persuasion</th>
      <td>Persuasion</td>
      <td>3.90</td>
      <td>132</td>
    </tr>
    <tr>
      <th>Crying Steel Sickle</th>
      <td>Crying Steel Sickle</td>
      <td>2.29</td>
      <td>106</td>
    </tr>
    <tr>
      <th>The Oculus, Token of Lost Worlds</th>
      <td>The Oculus, Token of Lost Worlds</td>
      <td>4.23</td>
      <td>49</td>
    </tr>
    <tr>
      <th>Glinting Glass Edge</th>
      <td>Glinting Glass Edge</td>
      <td>2.46</td>
      <td>45</td>
    </tr>
    <tr>
      <th>War-Forged Gold Deflector</th>
      <td>War-Forged Gold Deflector</td>
      <td>3.73</td>
      <td>155</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Deadline, Voice Of Subtlety</th>
      <td>Deadline, Voice Of Subtlety</td>
      <td>3.62</td>
      <td>98</td>
    </tr>
    <tr>
      <th>Curved Axe</th>
      <td>Curved Axe</td>
      <td>1.35</td>
      <td>33</td>
    </tr>
    <tr>
      <th>Haunted Bronzed Bludgeon</th>
      <td>Haunted Bronzed Bludgeon</td>
      <td>4.12</td>
      <td>76</td>
    </tr>
    <tr>
      <th>Warped Iron Scimitar</th>
      <td>Warped Iron Scimitar</td>
      <td>4.08</td>
      <td>146</td>
    </tr>
    <tr>
      <th>Thirsty Iron Reaver</th>
      <td>Thirsty Iron Reaver</td>
      <td>4.25</td>
      <td>166</td>
    </tr>
    <tr>
      <th>Foul Titanium Battle Axe</th>
      <td>Foul Titanium Battle Axe</td>
      <td>4.33</td>
      <td>56</td>
    </tr>
    <tr>
      <th>Amnesia</th>
      <td>Amnesia</td>
      <td>3.57</td>
      <td>22</td>
    </tr>
    <tr>
      <th>Souleater</th>
      <td>Souleater</td>
      <td>3.27</td>
      <td>21</td>
    </tr>
    <tr>
      <th>Restored Bauble</th>
      <td>Restored Bauble</td>
      <td>3.11</td>
      <td>16</td>
    </tr>
    <tr>
      <th>Celeste, Incarnation of the Corrupted</th>
      <td>Celeste, Incarnation of the Corrupted</td>
      <td>2.31</td>
      <td>67</td>
    </tr>
    <tr>
      <th>Faith's Scimitar</th>
      <td>Faith's Scimitar</td>
      <td>3.82</td>
      <td>133</td>
    </tr>
    <tr>
      <th>Frenzy, Defender of the Harvest</th>
      <td>Frenzy, Defender of the Harvest</td>
      <td>1.06</td>
      <td>69</td>
    </tr>
    <tr>
      <th>Oathbreaker, Spellblade of Trials</th>
      <td>Oathbreaker, Spellblade of Trials</td>
      <td>3.01</td>
      <td>159</td>
    </tr>
    <tr>
      <th>Nirvana</th>
      <td>Nirvana</td>
      <td>1.11</td>
      <td>82</td>
    </tr>
    <tr>
      <th>Solitude's Reaver</th>
      <td>Solitude's Reaver</td>
      <td>2.67</td>
      <td>113</td>
    </tr>
    <tr>
      <th>Exiled Doomblade</th>
      <td>Exiled Doomblade</td>
      <td>1.92</td>
      <td>164</td>
    </tr>
    <tr>
      <th>Rusty Skull</th>
      <td>Rusty Skull</td>
      <td>1.20</td>
      <td>6</td>
    </tr>
    <tr>
      <th>Thunderfury Scimitar</th>
      <td>Thunderfury Scimitar</td>
      <td>3.02</td>
      <td>163</td>
    </tr>
    <tr>
      <th>Putrid Fan</th>
      <td>Putrid Fan</td>
      <td>1.32</td>
      <td>5</td>
    </tr>
    <tr>
      <th>Pursuit, Cudgel of Necromancy</th>
      <td>Pursuit, Cudgel of Necromancy</td>
      <td>3.98</td>
      <td>19</td>
    </tr>
    <tr>
      <th>Sun Strike, Jaws of Twisted Visions</th>
      <td>Sun Strike, Jaws of Twisted Visions</td>
      <td>2.64</td>
      <td>168</td>
    </tr>
    <tr>
      <th>Ghastly Adamantite Protector</th>
      <td>Ghastly Adamantite Protector</td>
      <td>3.30</td>
      <td>136</td>
    </tr>
    <tr>
      <th>Dreamsong</th>
      <td>Dreamsong</td>
      <td>3.81</td>
      <td>80</td>
    </tr>
    <tr>
      <th>Unholy Wand</th>
      <td>Unholy Wand</td>
      <td>1.88</td>
      <td>26</td>
    </tr>
    <tr>
      <th>Righteous Might</th>
      <td>Righteous Might</td>
      <td>4.36</td>
      <td>142</td>
    </tr>
    <tr>
      <th>Oathbreaker, Last Hope of the Breaking Storm</th>
      <td>Oathbreaker, Last Hope of the Breaking Storm</td>
      <td>2.41</td>
      <td>178</td>
    </tr>
    <tr>
      <th>Soul-Forged Steel Shortsword</th>
      <td>Soul-Forged Steel Shortsword</td>
      <td>1.16</td>
      <td>156</td>
    </tr>
    <tr>
      <th>Downfall, Scalpel Of The Emperor</th>
      <td>Downfall, Scalpel Of The Emperor</td>
      <td>3.20</td>
      <td>109</td>
    </tr>
    <tr>
      <th>Foul Edge</th>
      <td>Foul Edge</td>
      <td>2.38</td>
      <td>43</td>
    </tr>
    <tr>
      <th>Bloodlord's Fetish</th>
      <td>Bloodlord's Fetish</td>
      <td>2.28</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
<p>183 rows × 3 columns</p>
</div>




```python
pop_item=[item_count,item_Purchase_total]
pop_item2=pd.DataFrame(pop_item)
pop_item2=pop_item2.T
pop_item2=pop_item2.reset_index()
item=item.merge(pop_item2,how='inner',on='Item Name')
```


```python
#item.columns=(['Item_name','Price','Item_ID','purchase_count','Total_amount_purchased'])
item=item.sort_values('purchase_count',ascending=False)
Item_summary=item.iloc[0:7,:]
Item_summary
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item_name</th>
      <th>Price</th>
      <th>Item_ID</th>
      <th>purchase_count</th>
      <th>Total_amount_purchased</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>92</td>
      <td>14.0</td>
      <td>38.60</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Final Critic</td>
      <td>4.62</td>
      <td>101</td>
      <td>14.0</td>
      <td>38.60</td>
    </tr>
    <tr>
      <th>53</th>
      <td>Betrayal, Whisper of Grieving Widows</td>
      <td>2.35</td>
      <td>39</td>
      <td>11.0</td>
      <td>25.85</td>
    </tr>
    <tr>
      <th>90</th>
      <td>Arcane Gem</td>
      <td>2.23</td>
      <td>84</td>
      <td>11.0</td>
      <td>24.53</td>
    </tr>
    <tr>
      <th>82</th>
      <td>Stormcaller</td>
      <td>2.78</td>
      <td>180</td>
      <td>10.0</td>
      <td>34.65</td>
    </tr>
    <tr>
      <th>81</th>
      <td>Stormcaller</td>
      <td>4.15</td>
      <td>30</td>
      <td>10.0</td>
      <td>34.65</td>
    </tr>
    <tr>
      <th>35</th>
      <td>Serenity</td>
      <td>1.49</td>
      <td>13</td>
      <td>9.0</td>
      <td>13.41</td>
    </tr>
  </tbody>
</table>
</div>



### Most profitable items


```python
item=item.sort_values('Total_amount_purchased',ascending=False)
Item_summary=item.iloc[0:7,:]
Item_summary
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item_name</th>
      <th>Price</th>
      <th>Item_ID</th>
      <th>purchase_count</th>
      <th>Total_amount_purchased</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>92</td>
      <td>14.0</td>
      <td>38.60</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Final Critic</td>
      <td>4.62</td>
      <td>101</td>
      <td>14.0</td>
      <td>38.60</td>
    </tr>
    <tr>
      <th>50</th>
      <td>Retribution Axe</td>
      <td>4.14</td>
      <td>34</td>
      <td>9.0</td>
      <td>37.26</td>
    </tr>
    <tr>
      <th>81</th>
      <td>Stormcaller</td>
      <td>4.15</td>
      <td>30</td>
      <td>10.0</td>
      <td>34.65</td>
    </tr>
    <tr>
      <th>82</th>
      <td>Stormcaller</td>
      <td>2.78</td>
      <td>180</td>
      <td>10.0</td>
      <td>34.65</td>
    </tr>
    <tr>
      <th>86</th>
      <td>Spectral Diamond Doomblade</td>
      <td>4.25</td>
      <td>115</td>
      <td>7.0</td>
      <td>29.75</td>
    </tr>
    <tr>
      <th>46</th>
      <td>Orenmir</td>
      <td>4.95</td>
      <td>32</td>
      <td>6.0</td>
      <td>29.70</td>
    </tr>
  </tbody>
</table>
</div>


