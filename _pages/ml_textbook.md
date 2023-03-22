---
title: "Учебник по машинному обучению"
permalink: /ml/textbook
layout: textbook

section: ml

---

{% for p in site.text %}
  {% if p.section == page.section %}
<h2 id="{{ p.title }}"><a href="{{ p.url }}">{{ p.title }}</a> </h2>

<div>
{{ p.content }} 
</div>

  {% endif %}
{% endfor %}

