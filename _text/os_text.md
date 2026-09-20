---
section: os
title: "Учебник по операционным системам"
permalink: /os/textbook
layout: textbook
---

{% for p in site.text %}
  {% if p.section == page.section and p != page %}
<h2 id="{{ p.title }}"><a href="{{ p.url }}">{{ p.title }}</a> </h2>
<div>
{{ p.content }} 
</div>
  {% endif %}
{% endfor %}
