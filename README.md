# Exno:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output
## Data Cleaning:
```
import pandas as pd
df=pd.read_csv('/content/SAMPLEIDS.csv')
print(df)
```
![1](https://github.com/user-attachments/assets/f16d37b6-6b99-4b53-ad90-f47aca7a7622)


```
df.head(10)
```
![2](https://github.com/user-attachments/assets/8d568f75-7bd3-48ad-88d2-0951ee8c8f64)


```
df.describe()
```

![3](https://github.com/user-attachments/assets/f9f20254-bfea-4114-989f-74e61c10df38)


```
df.isnull().sum()
```

![4](https://github.com/user-attachments/assets/c7983ff6-fb65-4868-aa2e-3c8268885a1b)


```
df.isnull().any()
```

![5](https://github.com/user-attachments/assets/898d3418-2efe-44fa-9d5d-61e15d0f5850)


```
df.dropna()
```

![6](https://github.com/user-attachments/assets/53a690ab-8a40-464d-b9d2-3915fa6be35b)

```
print(df.shape)
```

![7](https://github.com/user-attachments/assets/3724cb97-0628-49e3-a3d4-c82f3611d138)

```
df.fillna(0)
```

![8](https://github.com/user-attachments/assets/4f311545-054d-4b1c-a9e0-dd09b33f3f7a)


```
df.fillna(method='ffill')
```

![9](https://github.com/user-attachments/assets/911ec18b-61b6-48fe-a94e-1e54364df2e1)

```
df.fillna(method='bfill')
```

![10](https://github.com/user-attachments/assets/06ee4bd5-a19b-4595-8a45-b94448a1feb2)

```
df_dropped=df.dropna()
df_dropped
```

![11](https://github.com/user-attachments/assets/378a94d7-9b4d-4310-8013-422fb35f1c35)

```
df.fillna({'GENDER':'MALE','NAME':'SRI','ADDRESS':'POONAMALEE','M1':98,'M2':87,'M3':76,'M4':92,'TOTAL':305,'AVG':89.999999})
```

![12](https://github.com/user-attachments/assets/64ccc0c8-bda9-4ebd-8b64-7dc07440063c)



## IQR(Inter Quartile Range)

```
import pandas as pd
import seaborn as sns
import numpy as np

ir=pd.read_csv('/content/iris.csv')
ir
```

![13](https://github.com/user-attachments/assets/e78bcdda-8435-4f9a-af01-8544f208aed7)

```
ir.describe()
```

![14](https://github.com/user-attachments/assets/ebc8b7ce-b5ae-4430-995f-f54e0b967c23)

```
sns.boxplot(x='sepal_width',data=ir)
```

![15](https://github.com/user-attachments/assets/11c59411-0935-408c-a194-037ec58616be)

```
c1=ir.sepal_width.quantile(0.25)
c3=ir.sepal_width.quantile(0.75)
iq=c3-c1
print(c1)
print(c3)
print(iq)
```

![16](https://github.com/user-attachments/assets/6b5319dc-341a-4d52-ac7e-1b48704a642e)

```
rid=ir[((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
rid['sepal_width']
```

![17](https://github.com/user-attachments/assets/b6d29221-2250-4e5f-8551-264959c5af48)


```
delid=ir[~((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
delid
```

![18](https://github.com/user-attachments/assets/53c21bde-90f9-4d44-ae69-832f51417fd0)


```
sns.boxplot(x='sepal_width',data=delid)
```

![19](https://github.com/user-attachments/assets/5e5dfb87-c5b9-4831-8821-4b8b2a219007)


## Z-Score

```
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
import scipy.stats as stats
dataset=pd.read_csv('/content/heights.csv')
dataset
```

![20](https://github.com/user-attachments/assets/f966114d-4b4b-48ab-b547-c5361ac77c85)


```
df=pd.read_csv("heights.csv")
q1=df['height'].quantile(0.25)
q2=df['height'].quantile(0.5)
q3=df['height'].quantile(0.75)

iqr=q3-q1
iqr
```

![21](https://github.com/user-attachments/assets/ce3b8c46-7abd-4ccc-ae3e-63e5247168e0)


```
low= q1-1.5*iqr
low
```

![22](https://github.com/user-attachments/assets/7379cbc4-8f1a-466c-a8e7-f33eda99e1e0)


```
high=q3+1.5*iqr
high
```

![23](https://github.com/user-attachments/assets/21df706a-f1cc-42a3-8c1a-c163460ab702)


```
df1=df[((df['height'] >= low) & (df['height'] <= high))]
df1
```

![24](https://github.com/user-attachments/assets/96cf6c6e-5a95-4c03-a8b6-e1cf341a91bd)


```
z=np.abs(stats.zscore(df['height']))
z
```

![25](https://github.com/user-attachments/assets/24f0d489-b47b-421b-b0a0-da5a297f3676)


```
df1 = df[z<3]
df1
```

![26](https://github.com/user-attachments/assets/f84527f0-c689-4cf8-9033-8b74439cdbc4)


# Resut:
Thus we have cleaned the data and removed the outliers by detection using IQR and Z-score method
