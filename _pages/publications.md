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
  // 年の <h2 class="bibliography">xxxx</h2> を TOC から除外
  function markYearsToSkip(root=document) {
    root.querySelectorAll('h2.bibliography').forEach(h => {
      const text = (h.textContent || '').trim();
      if (/^\d{4}$/.test(text)) {
        h.setAttribute('data-toc-skip', ''); // bootstrap-toc が無視する
      }
    });
  }

  // すぐ実行（deferスクリプトより先に走る）
  markYearsToSkip();

  // DOM 完了後も一応もう一度（安全策）
  document.addEventListener('DOMContentLoaded', markYearsToSkip);

  // もしテーマが後から本文/TOCを書き換える場合に備えて監視
  new MutationObserver(muts => {
    muts.forEach(m => m.addedNodes.forEach(n => {
      if (n.nodeType === 1) markYearsToSkip(n);
    }));
  }).observe(document.body, { childList: true, subtree: true });
})();
</script>
