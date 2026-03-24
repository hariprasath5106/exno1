# Exno:1 - Data Cleaning Process

## AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

## Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

## Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

## Coding and Output
### Step 1: Import required libraries and read the data
```
import pandas as pd
import numpy as np
from scipy import stats
import seaborn as sns
# Step 1: Read the Data
data = pd.read_csv('/content/Data_set.csv')
data
```
<img width="1415" height="452" alt="image" src="https://github.com/user-attachments/assets/7f91d3ee-1515-4eb1-a862-4787a63d2da5" />

### Step 2: Get basic information about the data
```
data = pd.read_csv('/content/Data_set.csv')
data.info()
data.describe()
```
<img width="856" height="668" alt="image" src="https://github.com/user-attachments/assets/d62f31cf-1e6e-46b4-a884-6caae6ce5f2d" />

###  Step 3: Remove null values and display the sum of null values in each row
```
df_null=df.isnull()
df_null
df_null_sum=df.isnull().sum()
df_null_sum
df_nafill_0=df.fillna(0)
df_nafill_0
df_ffill=df.ffill()
df_ffill
# Fill Null Values with bfill Method
df_bfill=df.bfill()
df_bfill
# Calculate the mean value of a column and fill it with null values.
df_mean1=df['num_episodes'].fillna(df['num_episodes'].mean())
df_mean1
# Drop Null Values
df_dropna=df.isnull().dropna()
df_dropna
```
<img width="1175" height="461" alt="image" src="https://github.com/user-attachments/assets/0930b339-a19b-426c-aa2e-6375137920a8" />

### Step 4: Save the clean data to a new file
```
clean_data = data.dropna()
clean_data.to_csv('clean_data.csv', index=False)
```
### Step 5: Remove Outliers using IQR Method
```
ir=pd.read_csv('/content/iris.csv')
ir
# Use Boxplot function to detect outlier
sns.boxplot(ir)
# Use Scatterplot function to detect outlier
sns.scatterplot(ir)
q1=ir.sepal_width.quantile(0.25)
q3=ir.sepal_width.quantile(0.75)
iqr=q3-q1
print(iqr)
rid=ir[((ir.sepal_width<(q1-1.5*iqr))|(ir.sepal_width>(q3+1.5*iqr)))]
rid['sepal_width']
delid=ir[~((ir.sepal_width<(q1-1.5*iqr))|(ir.sepal_width>(q3+1.5*iqr)))]
delid
```
<img width="730" height="552" alt="image" src="https://github.com/user-attachments/assets/0e675cae-2e31-4f11-80e6-97bb52cd3e4a" />
<img width="536" height="413" alt="image" src="https://github.com/user-attachments/assets/5c567d19-451f-4205-a430-41d6c8a4cbec" />
<img width="534" height="413" alt="image" src="https://github.com/user-attachments/assets/6a68ff83-ae77-4680-92ca-744e0b4d0a0a" />

### Step 6: Remove Outliers using Z-score Method
```
data=[1,12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60]
df=pd.DataFrame(data)
mean=np.mean(data)
mean
std=np.std(data)
std
z=np.abs(stats.zscore(df))
z
threshold=3
outliers = df[abs(df) > 3]
print("Outliers:")
print(outliers)
# Remove outliers
df_cleaned = df[(z <= threshold)]
df_cleaned
```
```
Outliers:
       0
0    NaN
1   12.0
2   15.0
3   18.0
4   21.0
5   24.0
6   27.0
7   30.0
8   33.0
9   36.0
10  39.0
11  42.0
12  45.0
13  48.0
14  51.0
15  54.0
16  57.0
17  60.0
```
## Result
Thus the data cleaning process and outlier detection and removal on the given dataset is executed successfully.
