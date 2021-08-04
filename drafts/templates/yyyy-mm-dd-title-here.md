---
title: "Title"
excerpt_separator: "<!--more-->"
date: yyyy-mm-ddT15:34:30-04:00
categories:
  - Blog
tags:
  - Tag1
  - tag2
# link: https://github.com
# header:
  # image: /assets/images/cats.png
---
### What to expect/ What is it about/ Objectives/ Highlights:

- point
- point
- point

---

intro paragraph

### sub-topic

paragraph

**NOTE:** note
{: .notice--primary}

---
### 1. Another topic sentence


```python
import re

sample_text = "Lennon was initially the group's de facto leader, a role gradually ceded to McCartney. from 1968 to 1972, he produced more than a dozen records with Ono, including a trilogy of avant-garde albums."

pattern = r'[A-Z][a-z]+'
matched_results = re.findall(pattern, sample_text)

print(matched_results)

```

<http://www.pyregex.com>

If you need more detailed explanations for the patterns, this blog post from Dataquest comes in handy:

<https://www.dataquest.io/blog/regex-cheatsheet/>

To explore all the other methods in the `re` module, here's the official documentation: 

<https://docs.python.org/3/library/re.html>

Going further- Regex is a popular regex testing tool, you can see how regex is used across different languages (e.g. PHP/ Java). You can also find the explanations of different patterns on the reference panels:
 
<https://regex101.com>


A notice displays information that explains nearby content. Often used to call attention to a particular detail.

When using Kramdown `{: .notice}` can be added after a sentence to assign the `.notice` to the `<p></p>` element. 

**Changes in Service:** We just updated our [privacy policy](#) here to better service our customers. We recommend reviewing the changes.
{: .notice}

**Primary Notice:** Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer nec odio. [Praesent libero](#). Sed cursus ante dapibus diam. Sed nisi. Nulla quis sem at nibh elementum imperdiet.
{: .notice--primary}

**Info Notice:** Lorem ipsum dolor sit amet, [consectetur adipiscing elit](#). Integer nec odio. Praesent libero. Sed cursus ante dapibus diam. Sed nisi. Nulla quis sem at nibh elementum imperdiet.
{: .notice--info}

**Warning Notice:** Lorem ipsum dolor sit amet, consectetur adipiscing elit. [Integer nec odio](#). Praesent libero. Sed cursus ante dapibus diam. Sed nisi. Nulla quis sem at nibh elementum imperdiet.
{: .notice--warning}

**Danger Notice:** Lorem ipsum dolor sit amet, [consectetur adipiscing](#) elit. Integer nec odio. Praesent libero. Sed cursus ante dapibus diam. Sed nisi. Nulla quis sem at nibh elementum imperdiet.
{: .notice--danger}

**Success Notice:** Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer nec odio. Praesent libero. Sed cursus ante dapibus diam. Sed nisi. Nulla quis sem at [nibh elementum](#) imperdiet.
{: .notice--success}

Want to wrap several paragraphs or other elements in a notice? Using Liquid to capture the content and then filter it with `markdownify` is a good way to go.

```html
{% raw %}{% capture notice-2 %}
#### New Site Features

* You can now have cover images on blog pages
* Drafts will now auto-save while writing
{% endcapture %}{% endraw %}

<div class="notice">{% raw %}{{ notice-2 | markdownify }}{% endraw %}</div>
```

{% capture notice-2 %}
#### New Site Features

* You can now have cover images on blog pages
* Drafts will now auto-save while writing
{% endcapture %}

<div class="notice">
  {{ notice-2 | markdownify }}
</div>

Or you could skip the capture and stick with straight HTML.

```html
<div class="notice">
  <h4>Message</h4>
  <p>A basic message.</p>
</div>
```

<div class="notice">
  <h4>Message</h4>
  <p>A basic message.</p>
</div>

> Only one thing is impossible for God: To find any sense in any copyright law on the planet.
  
> <cite><a href="http://www.brainyquote.com/quotes/quotes/m/marktwain163473.html">Mark Twain</a></cite>