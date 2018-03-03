
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


