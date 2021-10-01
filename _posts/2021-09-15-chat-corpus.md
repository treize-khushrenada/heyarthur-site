---
title: "understanding network/ graph analysis"
excerpt_separator: "<!--more-->"
date: 2021-08-31T15:34:30-04:00
categories:
  - Draft
tags:
  - 
header:
  image: /assets/images/carambola-1.png
---

### What to expect:
- 
- 

---

1. The NPS Chat Corpus

NLTK is a “platform for building Python programs to work with human language data.”  It includes both the whole NPS Chat Corpus, as well as a number of modules for working with the data.

The nps_chat API doesn't provide a simple way to see POS tags and post metadata at the same time, but it's a matter of a one-liner to navigate the XML elements returned by xml_posts() and get this information. 

```python

# showing the schema from user DataFrame
user.printSchema()

```