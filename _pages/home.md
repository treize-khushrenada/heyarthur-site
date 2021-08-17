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
feature_row:
  - image_path: /assets/images/panda.png
    alt: "Experience Spotlight: AI and Machine Learning Products"
    title: "Experience Spotlight: AI and Machine Learning Products"
    excerpt: "Link to a page where I explain what I did that is related to AI and Machine Learning Products"
    url: "/docs/configuration/"
    btn_class: "btn--primary"
    btn_label: "Learn more"
  - image_path: /assets/images/panda.png
    alt: "fully responsive"
    title: "Responsive layouts"
    excerpt: "Built with HTML5 + CSS3. All layouts are fully responsive with helpers to augment your content."
    url: "/docs/layouts/"
    btn_class: "btn--primary"
    btn_label: "Learn more"
  - image_path: /assets/images/panda.png
    alt: "Project: The White Box"
    title: "Project: The White Box"
    excerpt: "Link to a page where people can see how AI concepts is demistified and democratised"
    url: "/docs/license/"
    btn_class: "btn--primary"
    btn_label: "Learn more"
  - image_path: /assets/images/panda.png
    alt: "Agile and PM Skills"
    title: "Agile and PM Skills"
    excerpt: "Link to a page about the Agile certification, explain what it means; list out the product management skills I process, and project examples; list out the PM tools/ tools that I used"
    url: "/docs/license/"
    btn_class: "btn--primary"
    btn_label: "Learn more" 
  - image_path: /assets/images/panda.png
    alt: "My Professional Journey"
    title: "My Professional Journey"
    excerpt: "Startups and Big Tech."
    url: "/docs/license/"
    btn_class: "btn--primary"
    btn_label: "Learn more" 

---

- PM Who can actually make things
- data transparency
- model/ problem matching advice (upstream/ downstream/shift)
- product analytics techniques
- working with data pipelines

My lens are:

AI in diversity
Misinformation
Democratizing Education
Self Expression with the help of content tools
Social agenda manipulation through content engineering
looking ahead in content streaming services
The real performance of an algorithm/ ai products (how they work)
content technologies in process automation
'AI-empowered' companies product strategies and comparison


What are some of the latest measure to previent racisms with imbalanced data
Can data scientist make an scalable app business?
in the world of reinforcement learning, how can we celebrate diversity?
Is there a relationship between audio files representations and popularity/ billboard data to find "the x factor"?

narration:

one catchy line. big names and condensed achievements

so now i am spending a whole year to build things that solves bigger problems
extract the goodies from this active research area, and build great things

sharing the kb for people who are interested in tech products management
to try to fix the bottleneck in applied ai product domain, and promote data science dna for organizations.

- self products/ data products- latest, knowledge and insights showcase, proven skills
-> macross (aim product hunt)
-> ersa (aim product hunt)

- old news- pass selectd work
-> ai/ big data solutions
-> product funnel analysis
-> scrum and agile
-> content technologies

- ai/ ds knowledge for business/ whitebox agenda
-> ai/ds "ankis"
-> practical ds/ ai skills sharing
-> research paper decompose
-> futuristic thinking based on some observations and facts

my philosophy:
pm- things to look at:
value perspective
-> create value for users, depth and breadth
-> map value with a creative process
-> investment depth and breadth
user perspective
-> problems and pain points
-> satisfaction and retention
-> control and behavioral shifts
technicality perspective
-> feasibility (research) **tech readiness in doubt, hidden germs not uncovered 
-> stability
-> efficiency
production perspective
-> operation roi **team readiness in ai in doubt
-> focus and lean
-> prioritization
-> foster environment for team growth
-> scalability (sourcing in labelling)

Strategy: finding the fits between the "->"s in the right order

on written communication strategy:
When talking about a product: people to perceive that starting from the product, how is that connected to high level vision/ epic (which is bridged to business/ strategy), and going downstream, how are the artifacts doing the job in correct interpretation. and moving forward, what processes to get to the pbis and prioritization, and based on the vision, what can be explored (combined with business/ tech/ personal knowledge and insight)

curate examples to explain ideas


{% include feature_row %}


<h3 class="archive__subtitle">{{ site.data.ui-text[site.locale].recent_posts | default: "Weekly News in AI" }}</h3>

{% if paginator %}
  {% assign posts = paginator.posts %}
{% else %}
  {% assign posts = site.posts %}
{% endif %}

{% assign entries_layout = page.entries_layout | default: 'list' %}
<div class="entries-{{ entries_layout }}">
  {% for post in posts %}
    {% include archive-single.html type=entries_layout %}
  {% endfor %}
</div>