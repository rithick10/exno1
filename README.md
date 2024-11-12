<h1 align="center">Ex. 1   Data Cleaning and Outlier Detection & Removal</h1>


## AIM
### To read the given data and perform data cleaning and save the cleaned data to a file.

## Explanation
### Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

## Algorithm
### STEP 1
#### Read the given Data

### STEP 2
#### Get the information about the data

### STEP 3 
#### Remove the null values from the data

### STEP 4
#### Save the Clean data to the file

### STEP 5
#### Remove outliers using IQR

### STEP 6
#### Use zscore of to remove outliers

## Coding and Outputs

<h3 align="center">Data Cleaning</h3>

```py
import pandas as pd
import numpy as np
import seaborn as sns
import os 
df=pd.read_csv("SAMPLEIDS.csv")
df
```

![image](https://github.com/KANISHKAR2607/exno1/assets/118886772/124e2d2c-73fa-4f2d-bdab-5abf837a473d)


```py
df.isnull().sum()

```

![image](https://github.com/KANISHKAR2607/exno1/assets/118886772/9f7849e2-6672-4615-9386-c1e13e5c6b6b)




```py
df.isnull().any()
```

![image](https://github.com/KANISHKAR2607/exno1/assets/118886772/bc9fa1bc-059a-4e47-9593-e62368bdbe67)


```py
df.dropna()
```

![image](https://github.com/KANISHKAR2607/exno1/assets/118886772/b7cace7b-bca7-43e4-b641-19056d99d231)


```py
df.fillna(0)
```

![image](https://github.com/KANISHKAR2607/exno1/assets/118886772/de9103ad-bedc-4c78-afc7-ebdf26115615)


```py
df.fillna(method = 'ffill')
```

![image](https://github.com/KANISHKAR2607/exno1/assets/118886772/6f693434-c0a2-4dda-b7f5-d8d30f656a9a)


```py

df.fillna(method = 'bfill')
```

![image](https://github.com/KANISHKAR2607/exno1/assets/118886772/d5547d0d-3131-4398-a668-4c115d238fd4)


```py
df_dropped = df.dropna()
df_dropped
```

![image](https://github.com/KANISHKAR2607/exno1/assets/118886772/94ecc695-7697-4da4-8baf-d0ddee440a4b)


```py
df.fillna({'GENDER':'MALE','NAME':'KANISHKAR','ADDRESS':'POONAMALEE','M1':98,'M2':87,'M3':76,'M4':92,'TOTAL':305,'AVG':89.999999})
```
![WhatsApp Image 2024-02-26 at 10 16 32_b866136c](https://github.com/KANISHKAR2607/exno1/assets/118886772/6a2c7ddf-f022-477f-8420-6cca78668e0d)


<hr><hr>

<h3 align="center">IQR(Inter Quartile Range)</h3>

```py
import pandas as pd
```

```py
ir=pd.read_csv('iris.csv')
ir
```

![image](https://github.com/KANISHKAR2607/exno1/assets/118886772/0862d650-ed81-4159-ba20-e27b8da2eca6)


```py
ir.describe()
```
![image](https://github.com/KANISHKAR2607/exno1/assets/118886772/b82f56ac-7861-4ccf-9e54-22b8ac539338)


```py
import seaborn as sns
```

```py

sns.boxplot(x='sepal_width',data=ir)
```


![image](https://github.com/KANISHKAR2607/exno1/assets/118886772/592199a9-643f-43bf-ab43-5c133e49a9b2)



```py
c1=ir.sepal_width.quantile(0.25)
c3=ir.sepal_width.quantile(0.75)
iq=c3-c1
print(c3)
```
![image](https://github.com/KANISHKAR2607/exno1/assets/118886772/0cc5d8cb-bca5-4721-a0a6-623d674c6835)



```py

rid=ir[((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
rid['sepal_width']
```

![image](https://github.com/KANISHKAR2607/exno1/assets/118886772/bd068741-ba70-4828-869e-a730414566b1)


```py
delid=ir[~((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
delid
```
![image](https://github.com/KANISHKAR2607/exno1/assets/118886772/84fea1fb-ca53-4956-80e4-1b0f6135baf8)


```py
sns.boxplot(x='sepal_width',data=delid)
```
![image](https://github.com/KANISHKAR2607/exno1/assets/118886772/9e4626be-7571-40e5-bbb5-099a1dc16ddf)


<hr><hr>

<h3 align="center">Z-Score</h3>

```py
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import scipy.stats as stats
```
```py
dataset=pd.read_csv("heights.csv")
dataset
```

![image](https://github.com/KANISHKAR2607/exno1/assets/118886772/0b72c3ed-8ce8-4b12-b0ec-ae0a08ead387)


```py
df = pd.read_csv("heights.csv")
q1 = df['height'].quantile(0.25)
q2 = df['height'].quantile(0.5)
q3 = df['height'].quantile(0.75)
```

```py
iqr = q3-q1
iqr
```

![image](https://github.com/KANISHKAR2607/exno1/assets/118886772/b754842d-7171-4a4d-bc08-2102a3c36ca4)



```py
low = q1 - 1.5*iqr
low
```

![image](https://github.com/KANISHKAR2607/exno1/assets/118886772/942a1ac6-3fb2-4bf0-bb3b-39f24d2061dd)


```py
high = q3 + 1.5*iqr
high
```

![image](https://github.com/KANISHKAR2607/exno1/assets/118886772/e67a2411-eb70-4a6e-84b6-1a1a26b88ccf)



```py
df1 = df[((df['height'] >=low)& (df['height'] <=high))]
df1
```
![image](https://github.com/KANISHKAR2607/exno1/assets/118886772/d95eeeb3-5c17-440c-9741-8f0841edb075)



```py
z = np.abs(stats.zscore(df['height']))
z
```
![image](https://github.com/KANISHKAR2607/exno1/assets/118886772/04c0d01f-64fd-4d85-ba85-780061035bf6)


```py
df1 = df[z<3]
df1
```

![image](https://github.com/KANISHKAR2607/exno1/assets/118886772/2966ba3a-74b6-4d69-8cc0-e0dcf6012e50)


<hr>

## Result
<br>

### Hence the data was cleaned , outliers were detected and removed.
