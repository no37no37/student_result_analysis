# student_result_analysis

## Introduction

The "Student Result Analysis" project aims to provide insights into student performance based on various factors. The analysis utilizes Python programming language along with popular data manipulation and visualization libraries such as NumPy, Pandas, Matplotlib, and Seaborn.

## Dataset Overview

The project begins by loading a dataset located at `C:\Users\acer\Downloads\Expanded_data_with_more_features.csv\student_scores.csv`. This dataset contains information about students, including demographic details, test scores, and other relevant factors.

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load the dataset
file_path = r"C:\Users\acer\Downloads\Expanded_data_with_more_features.csv\student_scores.csv"
df = pd.read_csv(file_path)

# Display basic information about the dataset
print(df.head())
print(df.describe())
print(df.info())
print(df.isnull().sum())
```

## Data Cleaning

The initial exploration includes a summary of the dataset, highlighting the count of non-null values, data types, and a brief statistical overview. Missing values are identified and addressed by dropping the "Unnamed: 0" column.

```python
# Drop unnecessary column
df = df.drop("Unnamed: 0", axis=1)
```

## Data Transformation

The project involves transforming the data, specifically in the "WklyStudyHours" column. The code snippet below replaces a specific string, enhancing the clarity of the data.

```python
# Change weekly study hours column
df["WklyStudyHours"] = df["WklyStudyHours"].str.replace("05-Oct", "5-10")
print(df.head())
```

## Exploratory Data Analysis

### Gender Distribution

The project explores the gender distribution within the dataset using a count plot, revealing that the number of females is slightly higher than males.

```python
# Gender Distribution
plt.figure(figsize=(5, 5))
ax = sns.countplot(data=df, x="Gender")
ax.bar_label(ax.containers[0])
plt.show()
```

### Parent's Education and Student's Score Relationship

The analysis continues by examining the relationship between parent education levels and student scores. A grouped bar plot with a heatmap provides a visual representation of this relationship.

```python
# Group by Parent's Education and calculate mean scores
gb = df.groupby("ParentEduc").agg({"MathScore": "mean", "ReadingScore": "mean", "WritingScore": "mean"})

# Display a heatmap
plt.figure(figsize=(5, 5))
sns.heatmap(gb, annot=True)
plt.title("Relationship between Parent's Education and Student's Score")
plt.show()
```

### Parent Marital Status and Student's Score Relationship

Similarly, the project investigates the impact of parent marital status on student scores, presenting the findings through a heatmap.

```python
# Group by Parent's Marital Status and calculate mean scores
gb1 = df.groupby("ParentMaritalStatus").agg({"MathScore": "mean", "ReadingScore": "mean", "WritingScore": "mean"})

# Display a heatmap
plt.figure(figsize=(5, 5))
sns.heatmap(gb1, annot=True)
plt.title("Relationship between Parent's Marital Status and Student's Score")
plt.show()
```

### Boxplots for Scores

The distribution of scores is visualized using boxplots, providing insights into the spread and central tendency of Math, Writing, and Reading scores.

```python
# Boxplots for Math, Writing, and Reading Scores
sns.boxplot(data=df, x="MathScore")
plt.show()

sns.boxplot(data=df, x="WritingScore")
plt.show()

sns.boxplot(data=df, x="ReadingScore")
plt.show()
```

### Distribution of Ethnic Groups

The analysis concludes by exploring the distribution of ethnic groups within the dataset. A pie chart and a count plot are used to present the findings.

```python
# Distribution of Ethnic Groups
ethnic_counts = df["EthnicGroup"].value_counts()

# Pie chart
plt.pie(ethnic_counts, labels=ethnic_counts.index, autopct="%1.2f%%")
plt.title("Distribution of Ethnic Groups")
plt.show()

# Count plot
ax = sns.countplot(data=df, x="EthnicGroup")
ax.bar_label(ax.containers[0])
plt.show()
```

In summary, the "Student Result Analysis" project provides a comprehensive exploration of student data, uncovering insights into various factors influencing academic performance. The use of Python and powerful libraries facilitates effective data manipulation and visualization for a meaningful analysis.
