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
- [Export Data](#export-data)

---

## Load Data

```python
import pandas as pd

df = pd.read_csv('data.csv')
df = pd.read_excel('data.xlsx')
df = pd.read_json('data.json')
```

## Inspect Data

```python
df.head()
df.tail()
df.info()
df.describe()
df.columns
df.dtypes
```

## Select & Filter

```python
df['column']
df[['col1', 'col2']]
df.loc[0]
df.iloc[0]
df[df['age'] > 30]
df[(df['age'] > 30) & (df['gender'] == 'M')]
```

## Sort Data

```python
df.sort_values('age')
df.sort_values('age', ascending=False)
```

## Group & Aggregate

```python
df.groupby('department').size()
df.groupby('department')['salary'].mean()
df.groupby(['dept', 'gender']).agg({'salary': ['mean', 'max']})
```

## Join & Merge

```python
pd.merge(df1, df2, on='id', how='inner')  # options: left, right, outer
df1.join(df2, lsuffix='_left', rsuffix='_right')
```

## Column Operations

```python
df['new_col'] = df['salary'] * 1.1
df.rename(columns={'old': 'new'}, inplace=True)
df.drop('unwanted', axis=1, inplace=True)
```

## Missing Data

```python
df.isnull().sum()
df.dropna()
df.fillna(0)
```

## Export Data

```python
df.to_csv('output.csv', index=False)
df.to_excel('output.xlsx')
```
