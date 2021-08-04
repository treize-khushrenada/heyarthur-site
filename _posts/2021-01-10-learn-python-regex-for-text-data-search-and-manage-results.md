---
title: "Quickly Search and Filter Your Text Data with Python's Regex Module"
excerpt_separator: "<!--more-->"
date: 2021-01-10T15:34:30-04:00
categories:
  - Blog
tags:
  - Python
  - Data Manipulation
  - Regex
---
### What to expect:

- Understand how to use Python's `re` module to perform searching in text files
- See examples of regex patterns and methods
- Explore how to use matched results for further processing

---

Whether you are a product manager, a user researcher, or any other role in this all-things-digital age, it has become extremely common that you'd have to efficiently process raw data to **generate insights**. Be it a .csv or a .txt file, it could always be a daunting task- we used the built-in search functions, got a dozens (or perhaps hundreds) of matches, manually skimmed through the matched items with our eyeballs, spotted and copy-pasted the useful pieces. 

What's happened next? We had to double-check our work to avoid human errors, or perhaps we just wanted to look up slightly differently- we started over, doing the same task (with potential human errors) all over again.

### The power of regex

It does not have to be that way.  With some simple Python scripts, you can easily extract the desirable pieces and never miss a thing. 

Regular expression, known as regex, is a sequence of characters that specifies a search pattern. Very often, these patterns are used to validate, find and replace input text data.

With just a few lines of Python code, you can create a powerful function that will scan through your documents and help you manage search results at ease. Such a powerful technique!

**NOTE:** If you are new to regex, **don't panic**. These patterns may look like alien languages at the first sight, and it can be counter-intuitive to memorize. The good news is, there are tons of free tools and cheatsheets for us to test and learn quickly. I will share the most practical resources at the end of this article. You can always refer to them to strengthen your memory- just sit back and relax!
{: .notice--primary}

---
### 1. Design a pattern, apply it to a regex method
In Python's regex module `re`, the `findall()` function will return all matched results from the input in a list format.

Here's an example text string:

`"John was initially the group's de facto leader, a role gradually ceded to Paul. from 1968 to 1972, he produced more than a dozen records with Yoko, including a trilogy of avant-garde albums."`

```python
import re

sample_text = "Lennon was initially the group's de facto leader, a role gradually ceded to McCartney. from 1968 to 1972, he produced more than a dozen records with Ono, including a trilogy of avant-garde albums."

pattern = r'[A-Z][a-z]+'
matched_results = re.findall(pattern, sample_text)

print(matched_results)

```
Result:
```python
['John', 'Paul', 'Yoko']
```

--- 
### 2. Connect with other Python methods

Combine with `open()` and `read()` method, you can perform searching in text files:

```python
with open ("filepath/filename.extention", "r") as file:
    txt_obj = file.read()

# below is an example pattern to find all strings that are on the same line and before ": "
# (?=) is called a "Positive Lookahead" pattern

pattern = '(.+)(?=: )' 
matched_results = re.findall(pattern, txt_obj)

```
---
### 3. Turning search results into structural data

Let's see another example of how we can incorporate regex functions to transform text data into a structural, refined dataset, with one simple line of code.

First, let's take a look at Python's list comprehension expression. It makes data transformation from one list to another super simple:

```python
new_list = [item.someMethod() for item in old_list]
```

Using list comprehension along with regex function `finditer()` and `goupdict()`, we can perform searching with multiple targets in mind, and put results in a dictionary format.

Let's say we have a log file of user behavior data, and we have to extract the username and timestamp data for each user.

We can first design a pattern with 2 regex groups using `(?P)`:

```python
pattern = "((?P<user_name>\w*|-)(\s)(\[(?P<timestamp>.+)\])(\s))" 

result = [item.groupdict() for item in re.finditer(pattern, txt_obj)]
```

Note that during handling from `.groupdic()`, `<tag_name>` will become keys in the dictionary, while the matched results (`item`) would be assigned as their corresponding values. It's that simple!

---
### Let's start learning!

Here are the tools and references for you to get started. First and foremost, I wound recommend this regex pattern testing tool with a table of commonly used patterns- you can mix and match the patterns to see how things work:

<http://www.pyregex.com>

If you need more detailed explanations for the patterns, this blog post from Dataquest comes in handy:

<https://www.dataquest.io/blog/regex-cheatsheet/>

To explore all the other methods in the `re` module, here's the official documentation: 

<https://docs.python.org/3/library/re.html>

Going further- Regex is a popular regex testing tool, you can see how regex is used across different languages (e.g. PHP/ Java). You can also find the explanations of different patterns on the reference panels:
 
<https://regex101.com>
