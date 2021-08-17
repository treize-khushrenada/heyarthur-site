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
  Apply AI and data science technologies to make a difference.<br />
intro: 
  - excerpt: 'Nullam suscipit et nam, tellus velit pellentesque at malesuada, enim eaque. Quis nulla, netus tempor in diam gravida tincidunt, *proin faucibus* voluptate felis id sollicitudin. Centered with `type="center"`'
feature_row:
  - image_path: /assets/images/lihkg-lipig.gif
    alt: "AI Product Experience"
    title: "AI Product Experience"
    excerpt: "Selected works ranging from conversational AI/ NLP solutions, model training operations to big data analysis projects."
    url: "/docs/configuration/"

  - image_path: /assets/images/lihkg-lipig.gif
    alt: "The White Box "
    title: "The White Box"
    excerpt: "Self-conducted research project aimed to demystify AI and data science. No more black box."
    url: "/docs/layouts/"

  - image_path: /assets/images/lihkg-lipig.gif
    alt: "Showcase: Macross"
    title: "Showcase: Macross"
    excerpt: "Should be a streamlit app or collab notebook"
    url: "/docs/license/"

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


{% include feature_row id="intro" type="center" %}


- PM Who can actually make things
- data transparency
- model/ problem matching advice (upstream/ downstream/shift)
- product analytics techniques
- working with data pipelines

Apply AI and data science technologies to make a difference.


{% include feature_row %}

<h3 class="archive__subtitle">{{ site.data.ui-text[site.locale].recent_posts | default: "Weekly News in AI" }}</h3>



{% assign entries_layout = page.entries_layout | default: 'list' %}
<div class="entries-{{ entries_layout }}">
  {%- for post in site.categories.newsletter -%}
    {% include archive-single.html type=entries_layout %}
  {% endfor %}
</div>