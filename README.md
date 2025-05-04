# 🐼 Pandas Syntax Reference Sheet

A quick reference for performing common data operations in **Pandas**.

---

## 📌 Table of Contents

- [Load Data](#load-data)
- [Inspect Data](#inspect-data)
- [Select & Filter](#select--filter)
- [Sort Data](#sort-data)
- [Group & Aggregate](#group--aggregate)
- [Join & Merge](#join--merge)
- [Column Operations](#column-operations)
- [Missing Data](#missing-data)
- [Duplicates](#duplicates)
- [Pivot & Melt](#pivot--melt)
- [Export Data](#export-data)

---

## Load Data

```python
import pandas as pd

# Load from CSV
df = pd.read_csv('data.csv')

# Load from Excel with detailed options
df = pd.read_excel('data.xlsx', sheet_name='Sheet1', header=0, index_col=None, dtype={'col1': str}, engine='openpyxl')

# Load from JSON
df = pd.read_json('data.json')
```

## Inspect Data

```python
df.head()          # First 5 rows
df.tail()          # Last 5 rows
df.info()          # DataFrame info (non-null count, types)
df.describe()      # Summary statistics
df.columns         # Column names
df.dtypes          # Data types of columns
```

## Select & Filter

```python
df['column']                   # Select a single column
df[['col1', 'col2']]            # Select multiple columns

df.loc[0]                       # Select the row with label '0' (index-based label)
df.loc[0:2]                     # Select rows with labels from 0 to 2 (inclusive)
df.loc[df['age'] > 30]          # Select rows where 'age' column value is greater than 30
df.loc[df['age'] > 30, ['name', 'age']]  # Select specific columns for rows where 'age' > 30

df.iloc[0]                      # Select the first row (by position)
df.iloc[0:2]                    # Select the first two rows (positions 0 and 1)
df.iloc[:, 1:3]                 # Select columns from position 1 to 2 (exclusive) for all rows
df.iloc[0, 1]                   # Select the element at row 0 and column 1 (position-based)

df[df['age'] > 30]              # Filter rows where 'age' column value is greater than 30

df[(df['age'] > 30) & (df['gender'] == 'M')]  # Multiple conditions using 'and' (&)
df[(df['age'] > 30) | (df['gender'] == 'M')]  # Multiple conditions using 'or' (|)
```

## Sort Data

```python
df.sort_values('age')                  # Sort by 'age' column
df.sort_values('age', ascending=False)  # Sort by 'age' in descending order
```

## Group & Aggregate

```python
df.groupby('department').size()                        # Count rows by group
df.groupby('department')['salary'].mean()               # Mean salary by department
df.groupby(['dept', 'gender']).agg({'salary': ['mean', 'max']})  # Aggregate with multiple functions

# Using as_index=False to keep grouped columns as regular columns
df.groupby('department', as_index=False)['salary'].mean()
```

## Join & Merge

```python
pd.merge(df1, df2, on='id', how='inner')  # Merge DataFrames on 'id' with inner join
df1.join(df2, lsuffix='_left', rsuffix='_right')  # Join two DataFrames on the index
```

## Column Operations

```python
df['new_col'] = df['salary'] * 1.1               # Create a new column based on existing ones
df.rename(columns={'old': 'new'}, inplace=True)   # Rename columns
df.drop('unwanted', axis=1, inplace=True)         # Drop a column
```

## Missing Data

```python
df.isnull().sum()     # Count missing values in each column
df.dropna()           # Drop rows with missing values
df.fillna(0)          # Replace missing values with 0
```

## Duplicates

```python
df.duplicated()       # Check for duplicate rows (True for duplicates)
df.drop_duplicates()  # Drop duplicate rows

# Drop duplicates based on a specific column, keeping the first occurrence
df.drop_duplicates(subset=['column'], keep='first')

# Drop duplicates based on a specific column, keeping the last occurrence
df.drop_duplicates(subset=['column'], keep='last')

# Drop all duplicates, keeping no occurrences (removes all duplicates)
df.drop_duplicates(subset=['column'], keep=False)
```

## Pivot & Melt

```python
# Pivot DataFrame (reshape)
df.pivot(index='id', columns='year', values='sales')

# Melt DataFrame (unpivot)
df.melt(id_vars=['id'], value_vars=['sales', 'profit'], var_name='metric', value_name='value')
```

## Export Data

```python
df.to_csv('output.csv', index=False)
df.to_excel('output.xlsx')
```
