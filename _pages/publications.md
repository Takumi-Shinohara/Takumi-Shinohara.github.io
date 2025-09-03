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
  min_level: 2
  max_level: 2
---

<!-- _pages/publications.md -->
<div class="publications">

{% for cat_ in page.categories  %}
	{% assign ind = forloop.index %}

	{%- capture cat -%}
	{{ page.catprint[ind] }}
	{%- endcapture -%}

	<h2 id="{{ cat | slugify }}">{{ cat }}</h2>
	{% for y in page.years reversed  %}
		{%- capture citecount -%}
		{% bibliography_count -f papers -q @*[kind={{cat_}} && year={{y}}]* %}
		{%- endcapture -%}

		{% if citecount != "0"  %}
			{% bibliography -f papers -q @*[kind={{cat_}} && year={{y}}]* %}
		{% endif %}
	{% endfor %}
{% endfor %}

</div>
<script>
document.addEventListener('DOMContentLoaded', function () {
  const allow = new Set(['#preprints', '#journal-articles', '#conference-articles']);

  document.querySelectorAll('.sidebar .toc a, nav.toc a, .toc a').forEach(a => {
    const href = (a.getAttribute('href') || '').toLowerCase();
    if (!allow.has(href)) {
      const li = a.closest('li') || a.parentElement;
      if (li) li.remove();
    }
  });

  document.querySelectorAll('.sidebar .toc ul, nav.toc ul, .toc ul').forEach(ul => {
    if (!ul.querySelector('li')) ul.remove();
  });
});
</script>

