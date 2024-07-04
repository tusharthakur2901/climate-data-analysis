# climate-data-analysis
Tools and scripts for analyzing climate data trends
# Climate_Data_Analysis.ipynb

import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load the data
data = pd.read_csv('../data/climate_data.csv')

# Display basic information about the dataset
data.info()

# Display descriptive statistics
data.describe()

# Data Cleaning: Handle missing values if any
data = data.dropna()

# Data Visualization
plt.figure(figsize=(10, 6))
sns.lineplot(x='Year', y='Temperature', data=data)
plt.title('Yearly Average Temperature')
plt.xlabel('Year')
plt.ylabel('Temperature')
plt.grid(True)
plt.show()

# Analysis: Calculate trends
data['Temperature_MA'] = data['Temperature'].rolling(window=10).mean()

plt.figure(figsize=(10, 6))
sns.lineplot(x='Year', y='Temperature', data=data, label='Yearly Temperature')
sns.lineplot(x='Year', y='Temperature_MA', data=data, label='10-Year Moving Average')
plt.title('Yearly Average Temperature with 10-Year Moving Average')
plt.xlabel('Year')
plt.ylabel('Temperature')
plt.legend()
plt.grid(True)
plt.show()
