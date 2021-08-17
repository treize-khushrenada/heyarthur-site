---
layout: splash
permalink: /
hidden: true
header:
  overlay_color: "#18191c"
  # overlay_image: /assets/images/mm-home-page-feature.jpg
  # actions:
    # - label: "<i class='fas fa-download'></i> Install now"
      # url: "/docs/quick-start-guide/"
excerpt: >
  proAI in diversity<br />
  Misinformation<br />
  Democratizing Education<br />
  Self Expression with the help of content tools<br />
  Social agenda manipulation through content engineering<br />
  looking ahead in content streaming services<br />
  The real performance of an algorithm/ ai products (how they work)<br />
  content technologies in process automation<br />
  'AI-empowered' companies product strategies and comparison<br />

intro: 
  - excerpt: self conducted research in and expirementations on applying ai / data science technologies to real world problems. the bottleneck, the cost, how to effectively discover problems and apply solutions. so now i am spending a whole year to build things that solves bigger problems. extract the goodies from this active research area, and build great things

feature_row:
  - image_path: /assets/images/lihkg-lipig.gif
    alt: "AI Product Experience"
    title: "AI Product Experience"
    excerpt: "Selected works ranging from conversational AI/ NLP solutions, model training operations to big data analysis projects."
    url: "/ai-experience-highlights"

  - image_path: /assets/images/lihkg-lipig.gif
    alt: "The White Box "
    title: "The White Box"
    excerpt: "Self-conducted research project aimed to demystify AI and data science- No more black box."
    url: "/the-white-box"

  - image_path: /assets/images/lihkg-lipig.gif
    alt: "Project Macross"
    title: "Project Macross"
    excerpt: "An app that analyzes your music taste with deep learning and NLP technologies."
    url: "/showcase-macross"

  - image_path: /assets/images/lihkg-lipig.gif
    alt: "Project Macross"
    title: "Project Macross"
    excerpt: "An app that analyzes your music taste with deep learning and NLP technologies."
    url: "/showcase-macross"

  - image_path: /assets/images/lihkg-lipig.gif
    alt: "Agile and PM Skills"
    title: "Agile and PM Skills"
    excerpt: "Link to a page about the Agile certification, explain what it means; list out the product management skills I process, and project examples; list out the PM tools/ tools that I used"
    url: "/docs/license/"

  - image_path: /assets/images/lihkg-lipig.gif
    alt: "My Professional Journey"
    title: "My Professional Journey"
    excerpt: "Startups and Big Tech."
    url: "/docs/license/"

---

self conducted research in and expirementations on applying ai / data science technologies to real world problems. the bottleneck, the cost, how to effectively discover problems and apply solutions. so now i am spending a whole year to build things that solves bigger problems. extract the goodies from this active research area, and build great things

- PM Who can actually make things
- data transparency
- model/ problem matching advice (upstream/ downstream/shift)
- product analytics techniques
- working with data pipelines

Apply AI and data science technologies to make a difference.

Portfolio

{% include feature_row %}

<h3 class="archive__subtitle">{{ site.data.ui-text[site.locale].recent_posts | default: "Latest Insights" }}</h3>

{% assign entries_layout = page.entries_layout | default: 'list' %}
<div class="entries-{{ entries_layout }}">
  {%- for post in site.categories.insights-curations -%}
    {% include archive-single.html type=entries_layout %}
  {% endfor %}
</div>