#This dataset includes various features related to car sales. It contains information such as customer names, gender, annual income, dealer details, car specifications, and more.
#Let's start!

# Basic Library Import :
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
%matplotlib inline
import seaborn as sns

# Ignoring the warnings :
import warnings
warnings.filterwarnings("ignore")
# Update the data path 
data_path = '/github/Janema-tech/car-sales-report/Car Sales.xlsx - car_data.csv' 
data = pd.read_csv(data_path)
data.head(5)
data.tail(5)
data.shape
# data cleaning
data.isna().sum()
data.duplicated().sum()

data.info()
data.nunique()   
# there must be some people who purched more cars as they have same number : Since, Unique Car_id != Unique Phone

data.describe()  
# The Maximum Price of car is = 858000$; The Minimum Price of car is = 1200$; Types of Engines = 2, Color = 3 and Body Styles = 5

# Checking the categories of the categorical features:
print("The categories in the variable 'Gender': ",end=" ")
print(data['Gender'].unique())

print("The categories in the variable 'Company': ",end=" ")
print(data['Company'].unique())

print("The categories in the variable 'Engine': ",end=" ")
print(data['Engine'].unique())

print("The categories in the variable 'Transmission': ",end=" ")
print(data['Transmission'].unique())

print("The categories in the variable 'Color': ",end=" ")
print(data['Color'].unique())

print("The categories in the variable 'Body Style': ",end=" ")
print(data['Body Style'].unique())

print("The categories in the variable 'Dealer_Region': ",end=" ")
print(data['Dealer_Region'].unique())

# This specific type of Engine name is 'DoubleÂ\xa0Overhead Camshaft' -> 'Double Overhead Camshaft'
print(data['Engine'].value_counts()['DoubleÂ\xa0Overhead Camshaft'])

# Replace occurrences
data['Engine'] = data['Engine'].replace('DoubleÂ\xa0Overhead Camshaft', 'Double Overhead Camshaft')

# Confirming the replacement
print(data['Engine'].unique())

# Now, defining Numerical and Categorical Features :
num_feature = [feature for feature in data.columns if data[feature].dtype != 'O']

cat_feature = [feature for feature in data.columns if data[feature].dtype == 'O']

# Names of Numeric and Categorical Features :
print('We have {} numerical features : {}'.format(len(num_feature), num_feature))
print('We have {} categorical features : {}'.format(len(cat_feature), cat_feature))

# there are some features that are not very useful that we can remove :Phone, Car_id, Customer Name, Dealer Name, Dealer_No
drop_col = ['Phone','Car_id','Customer Name','Dealer_Name','Dealer_No ']
df = data.drop(drop_col,axis=1)
df.head()

# Data Visualization and Interpretation 
fig, axs = plt.subplots(1, 2, figsize=(15, 7))
plt.subplot(121)
sns.histplot(data=df,x='Annual Income',bins=12,kde=True,color='g')
plt.subplot(122)
sns.histplot(data=df,x='Annual Income',bins=12,kde=True,hue='Gender')
plt.show()

min_salary = df['Annual Income'].min()
max_salary = df['Annual Income'].max()
print("The minimum salary (Annual) of a person that bought the car = {}".format(min_salary))
print("The maximum salary (Annual) of a person that bought the car = {}".format(max_salary))

# The minimum salary (Annual) of a person that bought the car = 10080
# The maximum salary (Annual) of a person that bought the car = 11200000

sns.countplot(data=df,x='Gender',color='skyblue')
fig, axs = plt.subplots(1, 1, figsize=(10, 5))
plt.subplot(111)
sns.histplot(data=df,x='Price ($)',bins=12,kde=True,color='teal')
plt.grid()
plt.show()

plt.figure(figsize=(8, 6))
sns.countplot(data=df,y='Company',palette = 'pastel')

plt.figure(figsize=(10, 24))
sns.countplot(data=df,y='Model',palette = 'pastel')

plt.figure(figsize=(5, 4))
sns.countplot(data=df,x='Engine',palette='husl')

plt.figure(figsize=(5, 5))
sns.countplot(data=df,x='Transmission',palette = 'Blues')

plt.figure(figsize=(5, 5))
sns.countplot(data=df,x='Color',palette = 'flare')

fig, axs = plt.subplots(1, 2, figsize=(12, 6))
plt.subplot(121)
sns.histplot(data=df,x='Body Style',color='skyblue')
plt.subplot(122)
sns.histplot(data=df,x='Body Style',hue='Gender')
plt.show()

plt.figure(figsize=(7, 5))
sns.countplot(data=df,x='Dealer_Region',palette = 'Blues')

sns.scatterplot(data=df,x='Price ($)',y='Transmission',hue='Transmission')

plt.figure(figsize=(10, 10))
sns.pairplot(data=df,hue='Gender',kind='scatter',diag_kind='hist')

plt.figure(figsize=(5, 5))
sns.jointplot(data=df,x='Annual Income',y='Price ($)',hue='Transmission')

plt.figure(figsize=(5, 5))
sns.jointplot(data=df,x='Price ($)',y='Annual Income',hue='Color',marker='^')

sns.boxplot(data=df, x="Price ($)", y="Body Style",hue='Body Style',palette = 'crest')

sns.boxplot(data=df, x="Price ($)", y="Engine",hue='Engine',palette = 'viridis')

# conclusion: 
# Top 5 Companies - Chevrolet, Dodge, Ford, Volkswagen
# Mitsubishi, Prefered Engine - Double Overhead Camshaft
# Prefered Transmission - Auto
# Most Liked Color of Cars - Pale White
# Most Cars sold in Price range - 15,000 USD to 40,000 USD
# Highest Sales Regions - Austin, Janesville, Scottsdale
# People's Favourite Body Style - SUV and HatchBack









































