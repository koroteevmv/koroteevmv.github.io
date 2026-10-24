---
title: "Учебник по машинному обучению"
permalink: /ml/textbook
layout: textbook
section: ml
---

{% for p in site.pres %}
  {% if p.section == page.section and p.title != page.title%}
<h2 id="{{ p.title }}"><a href="{{ p.url }}">{{ p.title }}</a> </h2>
<div>
{{ p.content | markdownify }} 
</div>
  {% endif %}
{% endfor %}

