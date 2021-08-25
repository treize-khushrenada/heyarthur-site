---
title: Spark for Sentiment Analysis on Review Platforms- Dealing with Big Data
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

### 1. Data Retrieval and basic exploration

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

### 2. Analysis with conditionals

How many top users contribute cool reviews to the community? We can assign condition to extract rows that users received more than 5000 'cool' compliments:

```python

users_cool_reviews = user.filter(user['compliment_cool'] > 5000).collect()
len(users_cool_reviews)
```
Results:
```
79
```

Similar to pandas, we can sort top reviews by their attributes in the pyspark dataframe; apply `limit()` for slicing top items:

```python

review_desc=review.orderBy('useful', ascending=False)
top_useful_reviews =review_desc.select('review_id','text','useful').limit(10)
top_useful_reviews.show()
```

```
+--------------------+--------------------+------+
|           review_id|                text|useful|
+--------------------+--------------------+------+
|4ZN5ZWVoGd8er9giA...|Dinner for 1.

- ...|  1241|
|A8mLBytNM2zmjHgSp...|In retrospect, I ...|  1122|
|ZmEtySx0W_RSv07aY...|This restaurant i...|   970|
|EYbuFrEnVkVdavuRm...|This is the secon...|   846|
|O1YX1g7Wbf0rmcoud...|I actually suspec...|   808|
|aTLCBP_6lrCs2Qo3k...|"scary that peopl...|   781|
|EluaWiwRr0VhTwJe9...|I really wanted t...|   694|
|oo7W2IgyMMiraml-s...|A few years ago a...|   668|
|QovoEUcs34yvCCm5u...|I'd put zero star...|   650|
|69suGHxR3PVxicAgm...|We were very disa...|   578|
+--------------------+--------------------+------+
```

### 3. User Defined Function for Further Filtering

Each element of a list-like object can be exploded as rows:

<img src="{{ site.url }}{{ site.baseurl }}/assets/images/concept-explode.png" alt="" class="full">

That is helpful for further processing with the elements in the list-like objects, such as hourly check-in records.

Create a User Defined Function (UDF) for date splitting and retrieving hour data through list comprehension, and convert data type, then inspect rush hour intervals throughout 24 hours:

```python
datesplit = udf(lambda x: x.split(','), ArrayType(StringType()))
get_hour = udf(lambda x: re.findall(r'\s(\d\d):', x)[0], StringType())

checkin_exploded = checkin.select(datesplit('date').alias('date_list')).withColumn('checkin_record', explode('date_list'))

checkin_hourly = checkin_exploded.select(get_hour('checkin_record').alias('hours'))
checkin_hourly.groupBy('hours').count().collect()

```

```

[Row(hours='07', count=231417),
 Row(hours='15', count=617830),
 Row(hours='11', count=111769),
 Row(hours='01', count=1561788),
 Row(hours='22', count=1257437),
 Row(hours='16', count=852076),
 Row(hours='18', count=1272108),
 Row(hours='00', count=1491176),
 Row(hours='17', count=1006102),
 Row(hours='09', count=100568),
 Row(hours='05', count=485129),
 Row(hours='19', count=1502271),
 Row(hours='23', count=1344117),
 Row(hours='08', count=151065),
 Row(hours='03', count=1078939),
 Row(hours='02', count=1411255),
 Row(hours='06', count=321764),
 Row(hours='20', count=1350195),
 Row(hours='10', count=88486),
 Row(hours='12', count=178910),
 Row(hours='04', count=747453),
 Row(hours='13', count=270145),
 Row(hours='21', count=1238808),
 Row(hours='14', count=418340)]

```
### 4. Dealing with Text Data

Stopwords can be removed using pyspark's `ml.feature` package, which can be applied along with regex UDF (to remove punctuations or any unwanted text patterns) for text data cleaning.

Counting top 50 frequently used words- which can be achieved with chaining methods with `\` and new line: 

```python 
stopwords_remove = StopWordsRemover(inputCol="words", outputCol="filtered" )
textsplit = udf(lambda x: re.sub(r'[^\w\s]', '', x).lower().split(), ArrayType(StringType()))

review_text = review.select(textsplit('text').alias('words'))
review_text = Remover_res4.transform(review_text)


review_text_frequency = review_text.select('filtered').withColumn('word', explode('filtered'))\
.groupBy('word')\
.count()\
.sort('count', ascending=False)\
.take(50)

```

By filtering reviews with attributes such as ratings and locations, popular words related to specific scenarios can be retrieved. For example, 4/5 star reviews contain top words such as:

```
['great', 'place', 'good', 'food', 'service']

```
