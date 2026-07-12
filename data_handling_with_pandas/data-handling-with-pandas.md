# Data Handling with Pandas

A practical, structured guide to data manipulation and analysis using the Pandas library — covering loading, exploring, cleaning, transforming, and visualizing real-world datasets, applied through a hands-on Spotify data analysis project.

---

## Table of Contents

1. [Overview](#1-overview)
2. [Learning Objectives](#2-learning-objectives)
3. [Setup](#3-setup)
4. [Pandas Data Structures](#4-pandas-data-structures)
5. [Loading Data](#5-loading-data)
6. [Exploring a Dataset](#6-exploring-a-dataset)
7. [Data Cleaning](#7-data-cleaning)
8. [Selecting and Filtering Data](#8-selecting-and-filtering-data)
9. [Sorting Data](#9-sorting-data)
10. [Grouping and Aggregation](#10-grouping-and-aggregation)
11. [Correlation Analysis](#11-correlation-analysis)
12. [Data Visualization](#12-data-visualization)
13. [Exploratory Data Analysis (EDA) Workflow](#13-exploratory-data-analysis-eda-workflow)
14. [Best Practices](#14-best-practices)
15. [Common Pandas Functions, Quick Reference](#15-common-pandas-functions--quick-reference)
16. [Mini Project: Spotify Songs Data Analysis](#16-mini-project-spotify-songs-data-analysis)
17. [Key Takeaways](#17-key-takeaways)
18. [Project Link](#18-project-link)

---

## 1. Overview

Pandas is one of the most widely used Python libraries for data manipulation and analysis. It provides powerful data structures and functions for loading, cleaning, transforming, analyzing, and exporting datasets.

Data handling is the first step in every data science and machine learning project, since real-world data is often incomplete, inconsistent, or unorganized.

---

## 2. Learning Objectives

By the end of this topic, the goal is to be able to:

- Load datasets from different sources
- Understand the structure of a dataset
- Inspect and summarize data
- Clean missing and duplicate values
- Filter and sort records
- Group data for aggregation
- Perform exploratory data analysis (EDA)
- Draw meaningful insights from data

---

## 3. Setup

### Installation
```bash
pip install pandas
```

### Import
```python
import pandas as pd
```

---

## 4. Pandas Data Structures

### Series
A one-dimensional labeled array.

```python
import pandas as pd

series = pd.Series([10, 20, 30])
print(series)
```

### DataFrame
A two-dimensional table consisting of rows and columns.

```python
data = {
    "Name": ["Ali", "Sara"],
    "Age": [21, 22]
}

df = pd.DataFrame(data)
```

---

## 5. Loading Data

### From a CSV file
```python
df = pd.read_csv("data.csv")
```

### From an Excel file
```python
df = pd.read_excel("data.xlsx")
```

### From a Hugging Face dataset
```python
from datasets import load_dataset

dataset = load_dataset("Zuru7/Spotify_Songs_with_SoundCloud_links")
df = dataset["train"].to_pandas()
```

---

## 6. Exploring a Dataset

| Method | Purpose |
|---|---|
| `df.head()` | View the first five rows, quickly inspect the dataset and verify it loaded correctly |
| `df.tail()` | View the last five rows |
| `df.shape` | Returns `(rows, columns)` |
| `df.columns` | Returns column names |
| `df.info()` | Returns row count, column names, missing values, data types, and memory usage |
| `df.describe()` | Statistical summary of numerical columns mean, median (50%), standard deviation, min, max, and quartiles |

---

## 7. Data Cleaning

### Missing Values

```python
# Check missing values
df.isnull().sum()

# Remove rows with missing values
df.dropna()

# Fill missing values
df.fillna(0)
```

### Duplicate Values

```python
# Check duplicates
df.duplicated().sum()

# View duplicates
df[df.duplicated()]

# Remove duplicates
df.drop_duplicates(inplace=True)
```

### Removing Unnecessary Columns

```python
df.drop(columns=["links", "lyrics"])
```

**Purpose:** reduce memory usage and retain only relevant information.

---

## 8. Selecting and Filtering Data

### Selecting Columns

```python
# Single column
df["track_name"]

# Multiple columns
df[["track_name", "track_popularity"]]
```

### Filtering Rows

```python
# Single condition
df[df["track_popularity"] > 80]

# Multiple conditions
df[
    (df["track_popularity"] > 80) &
    (df["playlist_genre"] == "pop")
]
```

---

## 9. Sorting Data

```python
# Ascending
df.sort_values("track_popularity")

# Descending
df.sort_values("track_popularity", ascending=False)
```

---

## 10. Grouping and Aggregation

```python
# Average popularity by genre
df.groupby("playlist_genre")["track_popularity"].mean()

# Multiple features by group
df.groupby("playlist_genre")[
    ["danceability", "energy", "tempo"]
].mean()
```

### Counting Values

```python
df["playlist_genre"].value_counts()
```

**Useful for:** genres, languages, artists, and other categorical breakdowns.

---

## 11. Correlation Analysis

Used to identify relationships between numerical variables.

```python
# Full correlation matrix
df.corr(numeric_only=True)

# Correlation with a specific column
df.corr(numeric_only=True)["track_popularity"]
```

---

## 12. Data Visualization

```python
import matplotlib.pyplot as plt
import seaborn as sns
```

| Chart | Code |
|---|---|
| Bar chart | `df["playlist_genre"].value_counts().plot(kind="bar")` |
| Histogram | `df["track_popularity"].hist()` |
| Scatter plot | `plt.scatter(df["energy"], df["track_popularity"])` |
| Heatmap | `sns.heatmap(df.corr(numeric_only=True))` |

---

## 13. Exploratory Data Analysis (EDA) Workflow

EDA is the process of understanding a dataset before applying machine learning.

**Typical workflow:**

1. Load dataset
2. Explore data
3. Clean data
4. Handle missing values
5. Remove duplicates
6. Remove irrelevant columns
7. Analyze distributions
8. Filter records
9. Sort records
10. Group data
11. Create visualizations
12. Identify correlations
13. Draw conclusions

---

## 14. Best Practices

- Always inspect data before analysis.
- Never ignore missing values.
- Remove duplicate records.
- Use meaningful variable names.
- Visualize data whenever possible.
- Document important findings.

---

## 15. Common Pandas Functions, Quick Reference

| Function | Purpose |
|---|---|
| `head()` | First rows |
| `tail()` | Last rows |
| `info()` | Dataset information |
| `describe()` | Statistical summary |
| `shape` | Number of rows and columns |
| `columns` | Column names |
| `isnull()` | Missing values |
| `duplicated()` | Duplicate records |
| `drop()` | Remove rows or columns |
| `fillna()` | Fill missing values |
| `groupby()` | Group data |
| `value_counts()` | Count categories |
| `sort_values()` | Sort records |
| `corr()` | Correlation |
| `plot()` | Create visualizations |

---

## 16. Mini Project: Spotify Songs Data Analysis

### Objective
Analyze a real-world Spotify dataset to understand music trends, song popularity, genres, artists, and audio characteristics using Pandas and exploratory data analysis.

### Dataset
- **Source:** Hugging Face
- **Dataset:** [Spotify Songs with SoundCloud Links](https://huggingface.co/datasets/Zuru7/Spotify_Songs_with_SoundCloud_links)

### Tasks Performed
- Loaded dataset from Hugging Face
- Converted dataset into a Pandas DataFrame
- Explored dataset structure
- Checked missing values
- Removed duplicate records
- Removed unnecessary columns
- Analyzed song popularity
- Identified top artists and genres
- Compared popular vs. non-popular songs
- Examined audio features such as danceability, energy, loudness, acousticness, and valence
- Performed correlation analysis
- Created visualizations using Matplotlib and Seaborn
- Summarized key insights

### Skills Demonstrated
- Data Loading
- Data Cleaning
- Data Manipulation
- Exploratory Data Analysis
- Feature Comparison
- Correlation Analysis
- Data Visualization
- Insight Generation

---

## 17. Key Takeaways

Through this project, the following skills were developed:

- Working with Pandas DataFrames
- Importing datasets from multiple sources
- Exploring and cleaning real-world data
- Filtering, sorting, and grouping records
- Performing exploratory data analysis
- Creating visualizations to communicate findings
- Identifying relationships between variables
- Generating meaningful, data-driven insights

---

## 18. Project Link

 **Project Repository:** https://github.com/Shaila-Yasin/spotify-music-analysis

---

*Notes compiled while learning and applying Pandas fundamentals to a real-world data analysis project.*
