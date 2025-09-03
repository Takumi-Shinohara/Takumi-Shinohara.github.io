---
layout: page
permalink: /publications/
title: Publications
description: 
years: [2016, 2017, 2018, 2019, 2020, 2021, 2022, 2023, 2024, 2025, 2026, 2027, 2028, 2029, 2030]
categories: ['Preprints', 'Journal Articles', 'Conference Articles']
catprint: ['', 'Preprints', 'Journal Articles', 'Conference Articles']
nav: true
nav_order: 2
toc:
  sidebar: left
---
<!-- _pages/publications.md -->
<div class="publications" markdown="1">

* Sections
{:toc}

{% for cat_ in page.categories  %}
	{% assign ind = forloop.index %}

	{%- capture cat -%}
	{{ page.catprint[ind] }}
	{%- endcapture -%}

 	### {{ cat }}
  	{: #{{ cat | slugify }} }
	
	{% for y in page.years reversed  %}
		{%- capture citecount -%}
		{% bibliography_count -f papers -q @*[kind={{cat_}} && year={{y}}]* %}
		{%- endcapture -%}

		{% if citecount != "0"  %}
  			#### {{ y }} {: .no_toc}
			{% bibliography -f papers -q @*[kind={{cat_}} && year={{y}}]* %}
		{% endif %}
	{% endfor %}
{% endfor %}

</div>
