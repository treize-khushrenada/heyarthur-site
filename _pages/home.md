---
layout: splash
permalink: /
hidden: true
header:
  overlay_color: "#18191c"
  # overlay_image: /assets/images/bg-overlay.gif
  # actions:
    # - label: "<i class='fas fa-download'></i> Install now"
      # url: "/docs/quick-start-guide/"
excerpt: >
  AI Enthusiast \| Master in Data Science <br>
  Product Manager \| PMI Agile Practitioner
intro: 
  - excerpt: "A learner and problem solver, obsessed with solving real-world problems.<br> <br>[About Me](/bio){: .btn .btn--primary}"

feature_row:
  - image_path: /assets/images/empty_icon.png
    alt: "AI Product Experience"
    title: AI Product Experience <br> 2017-2020
    excerpt: "Selected works ranging from conversational AI/ NLP solutions, model training operations to big data analysis projects."
    url: "/ai"

  - image_path: /assets/images/empty_icon.png
    alt: "The White Box "
    title: The White Box <br> 2021- now
    excerpt: "Self-conducted research project aimed to demystify AI and data science- No more black box."
    url: "/the-white-box"

  - image_path: /assets/images/empty_icon.png
    alt: "Project Macross"
    title: Project Macross <br> 2021- now
    excerpt: "An app that analyzes your music taste with deep learning and NLP technologies."
    url: "/showcase-macross"

  - image_path: /assets/images/empty_icon.png
    alt: "Project Macross"
    title: Project Macross <br> 2021- now
    excerpt: "An app that analyzes your music taste with deep learning and NLP technologies."
    url: "/showcase-macross"

  - image_path: /assets/images/empty_icon.png
    alt: "Agile and PM Skills"
    title: Agile and PM Skills
    excerpt: "Link to a page about the Agile certification, explain what it means; list out the product management skills I process, and project examples; list out the PM tools/ tools that I used"
    url: "/pm-gen"

  - image_path: /assets/images/empty_icon.png
    alt: "My Professional Journey"
    title: "My Professional Journey"
    excerpt: "Startups and Big Tech."
    url: "/gen"

---
<h1 class="archive__item-title">{% include feature_row id="intro" type="center" %}</h1>
**Updated Sep 2021:** Deep Learning research at University of Michigan + Independent AI project. Open for new challenges and collaborations!
{: .notice}

<h1 class="archive__item-title">Portfolio</h1><br>

{% include feature_row %}


<h1 class="archive__item-title">{{ site.data.ui-text[site.locale].recent_posts | default: "Insights" }}</h1>

{% assign entries_layout = page.entries_layout | default: 'list' |  sort_by: date %}
<div class="entries-{{ entries_layout }}">
  {%- for post in site.categories.Blog -%}
    {% include archive-single.html type=entries_layout %}
  {% endfor %}
</div>