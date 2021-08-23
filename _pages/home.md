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
  - image_path: /assets/images/research-data-science-icon.png
    alt: "AI/ Data Science Reseprearch"
    title: "AI/ Data Science Research"
    excerpt: "Self-conducted studies and research in data science"
    url: "/data-science-studies"

  - image_path: /assets/images/applied-ai-icon.png
    alt: "Applied AI"
    title: "Applied AI"
    excerpt: "Selected works of applied AI solutions"
    url: "/applied-ai"

  - image_path: /assets/images/pm-general-icon.png
    alt: "Product Management"
    title: Product Management
    excerpt: "Products delivered in the past, PM artifacts and activities highlights"
    url: "/pm-general"

feature_row_in_progress:
  - image_path: 
    alt: "Project Macross (In Progress)"
    title: "Project Macross <br> (In Progress)"
    excerpt: "Analyze your music taste with deep learning and NLP."
    url: "/showcase-macross"

  - image_path: /assets/images/empty_icon.png
    alt: "Project Macross"
    title: Project Macross <br> 2021- now
    excerpt: "An app that analyzes your music taste with deep learning and NLP technologies."
    url: "/showcase-macross"

---
<h1>{% include feature_row id="intro" type="center" %}</h1>
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