# week-8-python
# Task 1: Load and Explore the Dataset


# Import required libraries
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load the dataset from the local path
file_path = 'winequality-red.csv'  # Ensure this path is correct and points to your file location

try:
    # Attempt to load the dataset from the local file path
    df = pd.read_csv(file_path, sep=";")
    print("✅ Dataset loaded successfully!\n")
except Exception as e:
    print("❌ Error loading dataset:", e)
    df = None  # Assign None to df if loading fails

# Proceed only if the dataset is loaded successfully
if df is not None:
    # Display first few rows
    print("🔹 First 5 rows of the dataset:")
    print(df.head())

    # Data structure and missing values
    print("\n🔹 Dataset Info:")
    print(df.info())

    print("\n🔹 Missing Values in Each Column:")
    print(df.isnull().sum())

    # Basic statistics
    print("\n🔹 Summary Statistics:")
    print(df.describe())

    # Group by 'quality' and calculate mean alcohol
    print("\n🔹 Average Alcohol Content by Wine Quality:")
    print(df.groupby('quality')['alcohol'].mean())

    # --------- VISUALIZATIONS ---------

    # Set seaborn style
    sns.set(style="whitegrid")

    # Line Chart: Alcohol vs. Wine Quality
    plt.figure(figsize=(8,5))
    df.groupby("quality")["alcohol"].mean().plot(kind="line", marker="o", color="blue")
    plt.title("Average Alcohol by Wine Quality")
    plt.xlabel("Wine Quality")
    plt.ylabel("Average Alcohol (%)")
    plt.grid(True)
    plt.show()

    # Bar Chart: Average Sulphates by Quality
    plt.figure(figsize=(8,5))
    df.groupby("quality")["sulphates"].mean().plot(kind="bar", color="lightgreen")
    plt.title("Average Sulphates by Wine Quality")
    plt.xlabel("Wine Quality")
    plt.ylabel("Average Sulphates")
    plt.show()

    # Histogram: Alcohol Content
    plt.figure(figsize=(8,5))
    plt.hist(df["alcohol"], bins=10, color="coral", edgecolor="black")
    plt.title("Alcohol Content Distribution")
    plt.xlabel("Alcohol (%)")
    plt.ylabel("Frequency")
    plt.show()

    # Scatter Plot: Alcohol vs. Density
    plt.figure(figsize=(8,5))
    plt.scatter(df["alcohol"], df["density"], alpha=0.6, color="purple")
    plt.title("Alcohol vs. Density")
    plt.xlabel("Alcohol")
    plt.ylabel("Density")
    plt.show()
else:
    print("❌ Dataset could not be loaded. Please check the file path.")
