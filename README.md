# EXNO2DS
# AIM:
      To perform Exploratory Data Analysis on the given data set.
      
# EXPLANATION:
  The primary aim with exploratory analysis is to examine the data for distribution, outliers and anomalies to direct specific testing of your hypothesis.
  
# ALGORITHM:
STEP 1: Import the required packages to perform Data Cleansing,Removing Outliers and Exploratory Data Analysis.

STEP 2: Replace the null value using any one of the method from mode,median and mean based on the dataset available.

STEP 3: Use boxplot method to analyze the outliers of the given dataset.

STEP 4: Remove the outliers using Inter Quantile Range method.

STEP 5: Use Countplot method to analyze in a graphical method for categorical data.

STEP 6: Use displot method to represent the univariate distribution of data.

STEP 7: Use cross tabulation method to quantitatively analyze the relationship between multiple variables.

STEP 8: Use heatmap method of representation to show relationships between two variables, one plotted on each axis.

## CODING AND OUTPUT
```
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt

data = pd.read_csv("C:/Users/acer/Downloads/titanic_dataset.csv")

print("\nDataset Loaded Successfully\n")
print(data.head())
print("\nDataset Info:\n")
print(data.info())
print(data.describe())

for column in data.columns:
    if data[column].dtype == 'object':
        data[column] = data[column].fillna(data[column].mode()[0])   # Mode for categorical
    else:
        data[column] = pd.to_numeric(data[column], errors='coerce')
        data[column] = data[column].fillna(data[column].median())   # Median for numerical

plt.figure(figsize=(6,4))
sns.boxplot(x=data["Age"])
plt.title("Boxplot - Age")
plt.show()

plt.figure(figsize=(6,4))
sns.boxplot(x=data["Fare"])
plt.title("Boxplot - Fare")
plt.show()

def remove_outliers_iqr(df, column):
    Q1 = df[column].quantile(0.25)
    Q3 = df[column].quantile(0.75)
    IQR = Q3 - Q1
    lower = Q1 - 1.5 * IQR
    upper = Q3 + 1.5 * IQR
    return df[(df[column] >= lower) & (df[column] <= upper)]

print("Outliers for Age:", remove_outliers_iqr(data, "Age").shape)
print("Outliers for Fare:", remove_outliers_iqr(data, "Fare").shape)
print("Outliers removed using IQR method.\n")

plt.figure(figsize=(6,4))
sns.countplot(x="Survived", data=data)
plt.title("Countplot - Survival Distribution")
plt.show()
plt.figure(figsize=(6,4))
sns.countplot(x="SibSp", data=data)
plt.title("Countplot - Sibling/Spouse Distribution")
plt.show()
plt.figure(figsize=(6,4))
sns.countplot(x="Pclass", data=data)
plt.title("Countplot - Passenger Class Distribution")
plt.show()

sns.displot(data["Age"], kde=True, height=4, aspect=1.5)
plt.title("Displot - Age Distribution")
plt.show()
sns.displot(data["Fare"], kde=True, height=4, aspect=1.5)
plt.title("Displot - Fare Distribution")
plt.show()

print("\nCross Tabulation: SibSp vs Survived\n")
print(pd.crosstab(data["SibSp"], data["Survived"]))
print("\nCross Tabulation: Pclass vs Survived\n")
print(pd.crosstab(data["Pclass"], data["Survived"]))

plt.figure(figsize=(8,6))
correlation_matrix = data.select_dtypes(include=np.number).corr()
sns.heatmap(correlation_matrix, annot=True, cmap="coolwarm")
plt.title("Correlation Heatmap - Titanic Dataset")
plt.show()
```
<img width="1246" height="506" alt="image" src="https://github.com/user-attachments/assets/eafe057d-a4d1-4a35-8c9f-cd7562ce6bc2" />
<img width="1236" height="516" alt="image" src="https://github.com/user-attachments/assets/d663f9cd-ceb4-4449-bbb9-be6218d54feb" />
<img width="1239" height="408" alt="image" src="https://github.com/user-attachments/assets/5b9bc178-d19e-4228-9301-6007bb79d0a1" />
<img width="1244" height="512" alt="image" src="https://github.com/user-attachments/assets/e2302365-0ada-49b3-98f9-bbe34005104e" />
<img width="1210" height="503" alt="image" src="https://github.com/user-attachments/assets/4effd754-d426-441a-8cae-dd5752851b80" />
<img width="1238" height="616" alt="image" src="https://github.com/user-attachments/assets/630313cc-64f0-4d8e-9246-c87468795fd9" />
<img width="1239" height="509" alt="image" src="https://github.com/user-attachments/assets/d73ca88f-c26a-4980-b5f4-a2547ef2a9e0" />
<img width="1245" height="504" alt="image" src="https://github.com/user-attachments/assets/dfdb2e10-6e4c-4ac8-b050-50005474b0a0" />
<img width="1245" height="531" alt="image" src="https://github.com/user-attachments/assets/9f6031c8-0435-4301-b09e-b927645484f9" />
<img width="1239" height="521" alt="image" src="https://github.com/user-attachments/assets/a6327d48-9a14-48b6-986e-639617a76021" />
<img width="1231" height="434" alt="image" src="https://github.com/user-attachments/assets/67fa519f-a78a-43f1-a61f-8a72ec909f04" />
<img width="1363" height="768" alt="image" src="https://github.com/user-attachments/assets/f148b2f4-da6c-4d1a-ac44-025fd31f39c6" />

# RESULT
The Program and The Output has been sucessfully Verified along with the Visualization .
