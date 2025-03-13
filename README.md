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
##  Data Cleaning

```
import pandas as pd
df=pd.read_csv("/content/Data_set (1).csv")
df
```
![image](https://github.com/user-attachments/assets/ecd5c1e0-d8ac-4f35-99df-d5ec717442bd)
```
df.isnull()
```
![Screenshot 2025-03-13 140637](https://github.com/user-attachments/assets/42b02054-121c-494c-8637-ff5e0eb288f3)
```
df.notnull()
```
![Screenshot 2025-03-13 140857](https://github.com/user-attachments/assets/ebac5e43-6cdc-4866-a8fc-6f3ba9864969)
```
df.isnull().sum()
```
![Screenshot 2025-03-13 141038](https://github.com/user-attachments/assets/7c39490f-d5f5-468a-81b0-05cbf6fdaff6)
```
df.dropna(axis=1)
```
![Screenshot 2025-03-13 141141](https://github.com/user-attachments/assets/8c3ee20d-b573-4af0-9295-48c714825879)
```
df.dropna(axis=0)
```
![Screenshot 2025-03-13 141300](https://github.com/user-attachments/assets/5cf5f291-6363-47fa-bf63-97694b477f06)
```
df.fillna(0)
```
![Screenshot 2025-03-13 141356](https://github.com/user-attachments/assets/223c8978-dced-457e-86d0-8bf3f1c861ce)
```
df.fillna(method='ffill')
```
![image](https://github.com/user-attachments/assets/c47e8fc6-9929-448c-bee4-2b6639175a05)
```
df.fillna(method='bfill')
```
![Screenshot 2025-03-13 141748](https://github.com/user-attachments/assets/de4647d8-e971-47b8-803d-7a1c47df022c)
```
df['watchers'].fillna(value=df['watchers'].mean())
```
![Screenshot 2025-03-13 142321](https://github.com/user-attachments/assets/63cb37c4-825e-405f-818f-23468c0a4fc5)
```
df
```
![Screenshot 2025-03-13 142520](https://github.com/user-attachments/assets/8236f8a5-8ed5-46a3-9228-4a1c2274b2fa)
```
df.dropna(axis=1)
```
![Screenshot 2025-03-13 143008](https://github.com/user-attachments/assets/dc7da54d-9c63-4d7a-aefb-f29d4cee9291)
```
df.dropna(axis=0)
```
![Screenshot 2025-03-13 143105](https://github.com/user-attachments/assets/939e59d7-a6d2-49fc-9705-871a5f8b2635)

### IQR(Inter Quartile Range)
```
import pandas as pd
import seaborn as sns
sns.boxplot(x='watchers',data=df)
```
![Screenshot 2025-03-13 143430](https://github.com/user-attachments/assets/c1588ddc-695b-4fb5-ac9d-294cbd522de5)
```
q1=df.watchers.quantile(0.25)
q3=df.watchers.quantile(0.75)
iqr=q3-q1
print(iqr)
```
![Screenshot 2025-03-13 143524](https://github.com/user-attachments/assets/f4c93b26-8eee-4e66-91d7-c82a92d866f4)
```
lower_bound=q1-1.5*iqr
upper_bound=q3+1.5*iqr
print(lower_bound)
print(upper_bound)
```
![image](https://github.com/user-attachments/assets/41be9a5a-521b-4d4f-bbf6-d814f0ea5717)
```
df=df[(df.watchers<lower_bound)|(df.watchers>upper_bound)]
df['watchers']
```
![image](https://github.com/user-attachments/assets/2c6dd4de-5f53-415e-a9ae-294d4dd8958d)
```
sns.boxplot(x='watchers',data=df)
```
![Screenshot 2025-03-13 143828](https://github.com/user-attachments/assets/d17138d4-6400-41ae-bd3e-66c1c40732a9)
### Z-SCORE
```
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from scipy.stats import zscore
'''
'''
af=pd.read_csv("/content/heights.csv")
```
```
af
```
![Screenshot 2025-03-13 144109](https://github.com/user-attachments/assets/24b9d9b5-8280-444c-afe1-a164cf6b554a)
```
sns.boxplot(y='height',data=af)
```
![Screenshot 2025-03-13 144206](https://github.com/user-attachments/assets/5d3ac063-b750-4ba2-a786-687b843ec55d)
```
af["z_score"] = zscore(af["height"])
threshold = 3
outliers = af[abs(af["z_score"]) > threshold]
print(outliers)
```
![image](https://github.com/user-attachments/assets/5b932c8f-8a6e-4896-8db8-a4131bbd43cb)
```
af_cleaned = af[abs(af["z_score"]) <= threshold].drop(columns=["z_score"])
sns.boxplot(y=af_cleaned["height"])
```
![Screenshot 2025-03-13 144407](https://github.com/user-attachments/assets/ad7aa97d-e6a2-4187-8483-101fd13b4bd1)
































# Result
Thus we have cleaned the data and removed the outliers by detection using IQR and Z-score method.
