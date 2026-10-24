---
title: "Математические основы машинного обучения"
permalink: /math/textbook
layout: textbook

section: math

---

{% for p in site.text %}
  {% if p.section == page.section and p.title != page.title%}
<h2 id="{{ p.title }}"><a href="{{ p.url }}">{{ p.title }}</a> </h2>
<div>
{{  p.content  }} 
</div>
  {% endif %}
{% endfor %}

