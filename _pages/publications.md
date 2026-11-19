---
layout: page
permalink: /publications/
title: Publications
nav: true
nav_order: 2
categories: ["Preprints", "Journal Articles", "Conference Articles"]
toc:
  sidebar: left
  min_level: 2
  max_level: 2
scholar:
  sort_by: year
  order: descending
  group_by: none
  bibliography_template: bib_compact
  bibliography_list_tag: ul
  bibliography_item_attributes:
    class: mb-2
---

{% for category in page.categories %}
  {% capture count %}{% bibliography_count -f papers -q @*[kind={{ category }}]* %}{% endcapture %}
  {% assign count = count | strip | plus: 0 %}
  {% if count > 0 %}
<h2 id="{{ category | slugify }}">{{ category }}</h2>
{% bibliography -f papers -q @*[kind={{ category }}]* %}
  {% endif %}
{% endfor %}
