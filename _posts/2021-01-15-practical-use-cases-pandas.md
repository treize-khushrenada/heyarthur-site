---
title: Inspect CSV Files and Generate Analytics On the Fly- Basic Use Cases of pandas and scipy.stats
excerpt_separator: "<!--more-->"
date: 2021-01-15T15:34:30-04:00
categories:
  - Blog
tags:
  - Python
  - Data Manipulation
  - pandas
  - scipy
header:
  image: /assets/images/panda.png
---
### Highlights:
- Query large .csv dataset and compute mathematic operations without any spreadsheet tools
- Create data objects and manipulate their properties
--

Basic spreadsheet tools (e.g. Microsoft Excel/ Numbers/ Google Sheets) provide an easy way for us to manipulate tabular data, process the entries and visualize them. But when it comes to large dataset, such tools start having performance issues. It is also not ideal when we have to manually extract insights without clear "work scripts".

The `pandas` package is widely-used in the data science community. We can create efficient work scripts to retrieve data, clean data, and generate insights.

**NOTE:** This article focuses on practical use cases with the `pandas` module. `numpy`, is a dependency of `pandas` package. Check out [this article](https://www.javatpoint.com/pandas-vs-numpy) to learn more.
{: .notice--primary}

### Getting Started

Import packages for your python environment:

```python
import numpy as np
import pandas as pd
import scipy as sp
import scipy.stats as stats
```

Check the versions of packages:

```python
print ("pandas version: "+pd.__version__)
print ("numpy version: "+np.__version__)
print ("scipy version: "+sp.__version__)
```

#### Scenario 1: Gather all data from one column and generate a dictionary with proportional value for each variable (group by):

Confirm the column to look at- create a list called field.

```python
field = ['col_name']
```

Use `pd.read_csv` to read the csv file, and look at a specific column by appointing `usecols=field`.

```python
df = pd.read_csv("filename.csv", usecols=field)
```

The `df` item returned can be treated as a data object of the single column `col_name`

**NOTE:** When in doubt, use `df.head()` to inspect the data object and `df.dtypes` to check data type.
Note that the dtype is shown as object, not string and it's correct behavior. 
More technically speaking: instead of saving the bytes of `strings` in the `ndarray` directly, Pandas use object `ndarray`, which save pointers to objects.
{: .notice--primary}

Some datasets have their own naming conventions. For example, they may use a special set of numerical value (001/002/003) to represent variations ('apple'/ 'orange'/ 'banana') for each cell. We can replace these codes with more general terms. 

```python
# note: we can convert the column data type to string to ensure no errors during value replacement 
df = df.astype(str)
df = df.replace({"num_code_1" : "variation_1", "num_code_2" : "variation_2", "num_code_3" : "variation_3", "num_code_4" : "variation_4"})
```

Apply .value_counts() to object to count the column data object, with `(normalize=True)` so that the count results are in proportional values:

```python
df = df.value_counts(normalize=True)
```

**NOTE:** The `value_counts()` function will result in a `Series` object, which is specifically used for column data. It does not affect further processing.
{: .notice--primary}

Convert the data object to a dictionary using `.to_dict` method():

```python
dic = df.to_dict()
```

Return the dictionary object:

```python
{'variation_1': 0.47974705779026877,
 'variation_2': 0.24588090637625154,
 'variation_3': 0.172352011241876,
 'variation_4': 0.10202002459160373}
```

#### Scenario 2: Analyze data with conditionals and extra filtering:

Some data entries should be omitted during analytics stage. If we are to analyze the product funnel, some user_ids related to testers should be filtered out. Furthermore, some records might be incomplete in our database, and we have to get rid of those entries with `N/A` data fields. We can use `.drop()` and `.dropna()` for the job. 

Here is a simple illustration of how we can chain the two methods together:

```python
cleaned_df = df.dropna().drop(df[some_conditional_expressions].index)
# some_conditional_expressions: df.col_name = / != / >/ < values
```

Perform filtering and counting with multiple conditionals:

```python
field = ['col_1', 'col_2', 'col_3']
df = pd.read_csv("filename.csv", usecols=field)
counted = len(df.query('col_1 == 1 & col_2 == 0').index)
```

#### Scenario 3: Compare correlations between selections

`scipy`'s `stats` module contains useful statistics methods. Here we can use Pearson correlation coefficient and p-value for testing non-correlation. It supports taking `pandas` data objects as inputs.

```python
corr, p_value = stats.pearsonr(df["col_1"],df["col_2"])
```
### Learning Resources:

pandas official documentation:
<https://pandas.pydata.org/docs/>
scipy reference guide:
<https://docs.scipy.org/doc/scipy/reference/>