---
layout: archive
title: "Presentations"
permalink: /projects/
author_profile: true
---

{% if author.googlescholar %}
  You can also find my articles on <u><a href="https://scholar.google.com/citations?user=lK25ZjcAAAAJ&hl=en">my Google Scholar profile</a>.</u>
{% endif %}

======
{% include base_path %}

{% for post in site.presentations reversed %}
  {% include archive-single.html %}
{% endfor %}

Projects
======
{% include base_path %}

{% for post in site.projects reversed %}
  {% include archive-single.html %}
{% endfor %}
