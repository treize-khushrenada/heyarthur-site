---
title: Spark for Sentiment Analysis on Review Platforms- Dealing with Big Data- Part 1
excerpt_separator: "<!--more-->"
date: 2021-03-15T15:34:30-04:00
categories:
  - Blog
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
Similar to pandas, we can sort top reviews by their attributes in the pyspark dataframe; apply `limit()` for slicing top items:

```python

review_desc=review.orderBy('useful', ascending=False)
res2=review_desc.select('review_id','text','useful').limit(10)
res2.show()
```

```
+--------------------+--------------------+------+|review_id|text|useful|+--------------------+--------------------+------+|4ZN5ZWVoGd8er9giA...|Dinner for 1.- ...|  1241||A8mLBytNM2zmjHgSp...|In retrospect, I ...|  1122||ZmEtySx0W_RSv07aY...|This restaurant i...|   970||EYbuFrEnVkVdavuRm...|This is the secon...|   846||O1YX1g7Wbf0rmcoud...|I actually suspec...|   808||aTLCBP_6lrCs2Qo3k...|"scary that peopl...|   781||EluaWiwRr0VhTwJe9...|I really wanted t...|   694||oo7W2IgyMMiraml-s...|A few years ago a...|   668||QovoEUcs34yvCCm5u...|I'd put zero star...|   650||69suGHxR3PVxicAgm...|We were very disa...|   578|+--------------------+--------------------+------+
```

More practical functionalities to be shared in the next article of this series.