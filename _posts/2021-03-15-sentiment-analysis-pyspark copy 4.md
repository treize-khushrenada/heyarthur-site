---
title: this is a fake newsletter post
excerpt_separator: "<!--more-->"
date: 2021-03-15T15:34:30-04:00
categories:
  - newsletter
tags:
  - Spark
  - pyspark
  - Big Data
  - Sentiment Analysis
header:
  image: /assets/images/carambola-1.png
---

### What to expect:
- Understand the competitive advantages of Spark for big data processing
- Utilize Spark Dataframe to explore Yelp review datasets

---

### About Spark

Spark maintains the conventional big data programming model- MapReduce’s linear scalability and fault tolerance, while its engine can execute a more general directed acyclic graph (DAG) of operators. It is well suited for highly iterative algorithms that require multiple passes over a data set, as well as reactive applications that quickly respond to user queries by scanning large in-memory data sets.

Some key terms to note:

RDD: a type of dataset in spark, distributed as partitions in different work node. For example, the program reads from text file, using Parallelize method to create an RDD from an existing collection (For e.g Array) present in the driver.

Lazy evaluation in Spark: e.g. computation would not be executed until "action stage" (i.e. no error when we create RDD with wrong instructions during the transformation stage) , so it is very 'lazy' in computing.

### Spark's data processing hierarchy and workflow:

SparkSession-> SparkContext -> RDD/ Dataframe

Data source: Please refer to [Yelp Data from Kaggle](https://www.kaggle.com/yelp-dataset/yelp-dataset).

Example code of creating a SparkSession and SparkContext

```python

# import required packages
from pyspark.sql import SparkSession
from pyspark.sql.functions import explode, udf
from pyspark.sql.types import *
from pyspark.ml.feature import * 
import re
import string


spark = SparkSession \
    .builder \
    .master("local[*]") \
    .appName('Your_App_Name') \
    .getOrCreate() 

sc = spark.sparkContext


# Creating Spark Dataframes
business = spark.read.json('filepath/yelp_academic_dataset_business.json.gz')
checkin = spark.read.json('filepath/yelp_academic_dataset_checkin.json.gz')
review = spark.read.json('filepath/yelp_academic_dataset_review.json.gz')
tip = spark.read.json('filepath/yelp_academic_dataset_tip.json.gz')
user = spark.read.json('filepath/yelp_academic_dataset_user.json.gz')

```

Explore schema from `user` Dataframe:

```python

# showing the schema from user DataFrame
user.printSchema()

```

```
root
 |-- average_stars: double (nullable = true)
 |-- compliment_cool: long (nullable = true)
 |-- compliment_cute: long (nullable = true)
 |-- compliment_funny: long (nullable = true)
 |-- compliment_hot: long (nullable = true)
 |-- compliment_list: long (nullable = true)
 |-- compliment_more: long (nullable = true)
 |-- compliment_note: long (nullable = true)
 |-- compliment_photos: long (nullable = true)
 |-- compliment_plain: long (nullable = true)
 |-- compliment_profile: long (nullable = true)
 |-- compliment_writer: long (nullable = true)
 |-- cool: long (nullable = true)
 |-- elite: string (nullable = true)
 |-- fans: long (nullable = true)
 |-- friends: string (nullable = true)
 |-- funny: long (nullable = true)
 |-- name: string (nullable = true)
 |-- review_count: long (nullable = true)
 |-- useful: long (nullable = true)
 |-- user_id: string (nullable = true)
 |-- yelping_since: string (nullable = true)

```

Assign condition to extract rows that users received more than 5000 'cool' compliments:

```python

res1 = user.filter(user['compliment_cool'] > 5000).collect()
len(res1)
```
Results:
```
79
```

More practical functionalities to be shared in the next article of this series.