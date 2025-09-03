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
(function () {
  function markYearsToSkip() {
    document.querySelectorAll('h2.bibliography').forEach(h => {
      const t = (h.textContent || '').trim();
      if (/^\d{4}$/.test(t)) h.setAttribute('data-toc-skip','');
    });
  }
  markYearsToSkip();
  window.addEventListener('DOMContentLoaded', markYearsToSkip);
  window.addEventListener('load', markYearsToSkip);
})();
</script>
