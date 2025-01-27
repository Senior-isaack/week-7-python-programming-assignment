# week-7-python-programming-assignment
basic data analysis
Task 1: Load and Explore the Dataset
We'll start by loading the dataset, inspecting its structure, and cleaning any missing values.


import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

# Load the Iris dataset from seaborn
df = sns.load_dataset('iris')

# Display the first few rows to inspect the data
print(df.head())

# Check the data types of each column and check for missing values
print(df.info())

# Check for any missing values
print(df.isnull().sum())

# If there are missing values, we can fill them or drop them. Since Iris dataset has no missing values,
# we won't need to fill/drop anything, but let's include this for future datasets.
df_cleaned = df.dropna()  # Dropping missing values if any
Explanation:
df.head(): Displays the first few rows of the dataset.
df.info(): Provides information about the data types and number of non-null values.
df.isnull().sum(): Checks for missing values in the dataset.
df.dropna(): Removes any rows with missing data, though the Iris dataset does not have any missing values.
Task 2: Basic Data Analysis
Now, let's calculate some basic statistics, group the data by species, and compute the mean of numerical columns for each group.


# Basic statistics for the numerical columns
print(df.describe())

# Grouping by species and calculating the mean of numerical columns
grouped_data = df.groupby('species').mean()

print(grouped_data)
Explanation:
df.describe(): Computes the mean, median, standard deviation, etc., for each numerical column.
df.groupby('species').mean(): Groups the dataset by the species column and computes the mean for each numerical column within each species.
Task 3: Data Visualization



# 1. Line chart showing trends over time (Assuming we had a time column; here we'll simulate a trend with 'sepal_length')
df['sepal_length_trend'] = df['sepal_length'].cumsum()  # Simulating a cumulative trend

plt.figure(figsize=(10, 6))
plt.plot(df['sepal_length_trend'], marker='o', color='b', label='Cumulative Sepal Length')
plt.title('Cumulative Sepal Length Trend')
plt.xlabel('Index')
plt.ylabel('Cumulative Sepal Length')
plt.legend()
plt.show()

# 2. Bar chart showing average petal length per species
plt.figure(figsize=(10, 6))
sns.barplot(x='species', y='petal_length', data=df, ci=None)
plt.title('Average Petal Length per Species')
plt.xlabel('Species')
plt.ylabel('Average Petal Length')
plt.show()

# 3. Histogram of sepal width distribution
plt.figure(figsize=(10, 6))
sns.histplot(df['sepal_width'], kde=True, bins=20, color='g')
plt.title('Distribution of Sepal Width')
plt.xlabel('Sepal Width')
plt.ylabel('Frequency')
plt.show()

# 4. Scatter plot of petal length vs. petal width
plt.figure(figsize=(10, 6))
sns.scatterplot(x='petal_length', y='petal_width', hue='species', data=df, palette='Set1')
plt.title('Petal Length vs. Petal Width')
plt.xlabel('Petal Length')
plt.ylabel('Petal Width')
plt.legend(title='Species')
plt.show()
Explanation of Visualizations:
Line Chart: We simulate a cumulative trend of sepal length. This chart shows how the cumulative sum of sepal length changes as we move through the dataset.

df['sepal_length'].cumsum() calculates the cumulative sum of the sepal_length column.
Bar Chart: This shows the average petal length for each species of Iris.

sns.barplot() is used to create a bar plot, with the x-axis being the species and the y-axis being the average petal length.
Histogram: The distribution of sepal width is plotted to see its frequency and distribution.

sns.histplot() creates the histogram, and we also include a Kernel Density Estimate (KDE) to visualize the smooth distribution.
Scatter Plot: This shows the relationship between petal length and petal width, with points colored by species to see if there are distinct patterns.

sns.scatterplot() helps visualize how petal length and petal width relate, with different colors representing different species.
Error Handling
Let include some error handling to deal with potential issues, such as missing files or invalid columns.



    # Try loading the dataset
    df = pd.read_csv('iris.csv')  # If you use your own file path here
except FileNotFoundError:
    print("Error: File not found. Please check the file path.")
except pd.errors.EmptyDataError:
    print("Error: The file is empty. Please check the content of the file.")
except Exception as e:
    print(f"An error occurred: {e}")








