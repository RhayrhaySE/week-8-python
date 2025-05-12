# week-8-python
# Task 1: Load and Explore the Dataset

import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
from sklearn.datasets import load_iris

# Error handling
try:
    iris = load_iris()
    data = pd.DataFrame(data=iris.data, columns=iris.feature_names)
    data['species'] = iris.target
    data['species'] = data['species'].map({i: name for i, name in enumerate(iris.target_names)})

    print("✅ Dataset loaded successfully!\n")
    print(data.head())  # Display first 5 rows

except Exception as e:
    print("❌ Error loading dataset:", e)

# Explore data structure
print("\n🔍 Data Info:")
print(data.info())

# Check for missing values
print("\n🧼 Missing Values:")
print(data.isnull().sum())

# No missing values, so no cleaning needed

# Task 2: Basic Data Analysis

print("\n📊 Descriptive Statistics:")
print(data.describe())

# Group by species and get the mean
grouped = data.groupby('species').mean()
print("\n📈 Mean values per species:")
print(grouped)

# Task 3: Data Visualization

# Set seaborn theme
sns.set(style='whitegrid')

# Line Chart: Average petal length per species (simulated over index as "time")
plt.figure(figsize=(8,5))
for species in data['species'].unique():
    subset = data[data['species'] == species]
    plt.plot(subset.index, subset['petal length (cm)'], label=species)
plt.title("Petal Length Trend (Simulated Over Index)")
plt.xlabel("Index")
plt.ylabel("Petal Length (cm)")
plt.legend()
plt.show()

# Bar Chart: Average Sepal Width per Species
plt.figure(figsize=(6,4))
sns.barplot(x=grouped.index, y=grouped['sepal width (cm)'], palette="viridis")
plt.title("Average Sepal Width by Species")
plt.xlabel("Species")
plt.ylabel("Sepal Width (cm)")
plt.show()

# Histogram: Distribution of Petal Length
plt.figure(figsize=(6,4))
sns.histplot(data['petal length (cm)'], kde=True, bins=20, color='orange')
plt.title("Distribution of Petal Length")
plt.xlabel("Petal Length (cm)")
plt.show()

# Scatter Plot: Sepal Length vs Petal Length
plt.figure(figsize=(6,5))
sns.scatterplot(data=data, x='sepal length (cm)', y='petal length (cm)', hue='species')
plt.title("Sepal Length vs Petal Length by Species")
plt.xlabel("Sepal Length (cm)")
plt.ylabel("Petal Length (cm)")
plt.legend()
plt.show()
