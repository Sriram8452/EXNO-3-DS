## EXNO-3-DS

# AIM:
To read the given data and perform Feature Encoding and Transformation process and save the data to a file.

# ALGORITHM:
STEP 1:Read the given Data.
STEP 2:Clean the Data Set using Data Cleaning Process.
STEP 3:Apply Feature Encoding for the feature in the data set.
STEP 4:Apply Feature Transformation for the feature in the data set.
STEP 5:Save the data to the file.

# FEATURE ENCODING:
1. Ordinal Encoding
An ordinal encoding involves mapping each unique label to an integer value. This type of encoding is really only appropriate if there is a known relationship between the categories. This relationship does exist for some of the variables in our dataset, and ideally, this should be harnessed when preparing the data.
2. Label Encoding
Label encoding is a simple and straight forward approach. This converts each value in a categorical column into a numerical value. Each value in a categorical column is called Label.
3. Binary Encoding
Binary encoding converts a category into binary digits. Each binary digit creates one feature column. If there are n unique categories, then binary encoding results in the only log(base 2)ⁿ features.
4. One Hot Encoding
We use this categorical data encoding technique when the features are nominal(do not have any order). In one hot encoding, for each level of a categorical feature, we create a new variable. Each category is mapped with a binary variable containing either 0 or 1. Here, 0 represents the absence, and 1 represents the presence of that category.

# Methods Used for Data Transformation:
  # 1. FUNCTION TRANSFORMATION
• Log Transformation
• Reciprocal Transformation
• Square Root Transformation
• Square Transformation
  # 2. POWER TRANSFORMATION
• Boxcox method
• Yeojohnson method

# CODING AND OUTPUT:

# 1.FEATURE ENCODING:
 
 ```
import pandas as pd
df=pd.read_csv("Encoding Data.csv")
df
```
![image](https://github.com/Sriram8452/EXNO-3-DS/assets/118708032/63330983-1267-49f8-8f98-a6f5b127692b)

# 2.ORDINAL ENCODER:

```
from sklearn.preprocessing import LabelEncoder,OrdinalEncoder
pm=["Hot","Warm",'Cold']
e1=OrdinalEncoder(categories=[pm])
e1.fit_transform(df[["ord_2"]])
```
![image](https://github.com/Sriram8452/EXNO-3-DS/assets/118708032/9b2a4b19-7c34-430c-9b6a-d273cbaf8ce0)

```
df['bo2']=e1.fit_transform(df[["ord_2"]])
df
```
![image](https://github.com/Sriram8452/EXNO-3-DS/assets/118708032/fd718ecf-e21d-4319-b5e7-fc289086604a)

# 3.LABEL ENCODER:

```
le=LabelEncoder()
dfc=df.copy()
dfc['ord_2']=le.fit_transform(dfc['ord_2'])
dfc
```
![image](https://github.com/Sriram8452/EXNO-3-DS/assets/118708032/0d728fda-59e5-4e43-9bda-fea94a022d03)

# 4.ONEHOT ENCODER:

```
from sklearn.preprocessing import OneHotEncoder
ohe=OneHotEncoder(sparse=False)
df2=df.copy()
enc=pd.DataFrame(ohe.fit_transform(df2[['nom_0']]))
df2=pd.concat([df2,enc],axis=1)
pd.get_dummies(df2,columns=["nom_0"])
```
![image](https://github.com/Sriram8452/EXNO-3-DS/assets/118708032/c549e6c7-0c59-42b6-a4be-f634e23971e7)

# 5.BINARY ENCODER:

```
pip install category_encoders
```
![image](https://github.com/Sriram8452/EXNO-3-DS/assets/118708032/ba99936c-a0cf-4612-ac2d-4d34cc307f18)

```
from category_encoders import BinaryEncoder
df=pd.read_csv("data.csv")
be=BinaryEncoder()
nd=be.fit_transform(df['Ord_2'])
dfb=pd.concat([df,nd],axis=1)
dfb
```
![image](https://github.com/Sriram8452/EXNO-3-DS/assets/118708032/92e9fe0f-f066-4fca-bf37-73d822068357)

# 6.TARGET ENCODER:

```
from category_encoders import TargetEncoder
te=TargetEncoder()
cc=df.copy()
from category_encoders import TargetEncoder
te=TargetEncoder()
cc=df.copy()
new=te.fit_transform(X=cc["City"],y=cc["Target"])
cc=pd.concat([cc,new],axis=1)
cc
```
![image](https://github.com/Sriram8452/EXNO-3-DS/assets/118708032/5110c400-69f7-49e8-9e1e-ab9f3c98218c)

# 7.DATA TRANSFORMATION:

```
import pandas as pd
from scipy import stats
import numpy as np
df=pd.read_csv("Data_to_Transform.csv")
df
```
![image](https://github.com/Sriram8452/EXNO-3-DS/assets/118708032/0c16886d-47db-41aa-bf07-39fcbe7deddb)

```
df.skew()
```
![image](https://github.com/Sriram8452/EXNO-3-DS/assets/118708032/0bab19c6-b011-48f0-acde-f4d8397f83e0)

```
np.log(df["Highly Positive Skew"])
```
![image](https://github.com/Sriram8452/EXNO-3-DS/assets/118708032/a1b09b3f-7c36-43e4-9d96-384cb9d43f2f)

```
np.reciprocal(df["Moderate Positive Skew"])
```
![image](https://github.com/Sriram8452/EXNO-3-DS/assets/118708032/c7756850-3bbe-48df-b7e7-a32dd03c047b)

```
np.sqrt(df["Highly Positive Skew"])
```
![image](https://github.com/Sriram8452/EXNO-3-DS/assets/118708032/2672f5e0-c4f1-4e2c-a823-cf537c35fdeb)

```
np.square(df["Highly Positive Skew"])
```
![image](https://github.com/Sriram8452/EXNO-3-DS/assets/118708032/1f76af93-f42d-4368-8197-9a1f5a9a9cfd)

```
df["Highly Positive Skew_boxcox"],parameters=stats.boxcox(df["Highly Positive Skew"])
df
```
![image](https://github.com/Sriram8452/EXNO-3-DS/assets/118708032/b8b2b111-b9ac-4216-8e7e-c6d2b4a0ddbc)

```
df["Moderate Negative Skew_yeojohnson"],parameters=stats.yeojohnson(df["Moderate Negative Skew"])
df.skew()
```
![image](https://github.com/Sriram8452/EXNO-3-DS/assets/118708032/f3c7a9fa-369c-420c-b65a-ffc9e74f2175)

```
df["Highly Negative Skew_yeojohnson"],parameters=stats.yeojohnson(df["Highly Negative Skew"])
df.skew()
```
![image](https://github.com/Sriram8452/EXNO-3-DS/assets/118708032/185a64c7-cfc9-40ef-9e00-e910519458a9)

# 8.Graphical Visualization:
```
import matplotlib.pyplot as plt
import seaborn as sns
import statsmodels.api as sm
import scipy.stats as stats
sm.qqplot(df["Moderate Negative Skew"],line='45')
plt.show()
```
![image](https://github.com/Sriram8452/EXNO-3-DS/assets/118708032/0dff9075-c794-4fed-b270-49f30ba20341)

```
sm.qqplot(np.reciprocal(df["Moderate Negative Skew"]),line='45')
```
![image](https://github.com/Sriram8452/EXNO-3-DS/assets/118708032/ec3a9a35-4e06-4ebc-9169-43590015fe02)

```
from sklearn.preprocessing import QuantileTransformer
qt=QuantileTransformer(output_distribution='normal',n_quantiles=891)
df["Moderate Negative Skew"]=qt.fit_transform(df[["Moderate Negative Skew"]])
sm.qqplot(df["Moderate Negative Skew"],line='45')
plt.show()
```
![image](https://github.com/Sriram8452/EXNO-3-DS/assets/118708032/ad8ef943-9088-4035-9f66-4eb6a8b1d145)

# RESULT:
Thus the given data is read and  Feature Encoding and Transformation process is performed and save the data to a file.


       
