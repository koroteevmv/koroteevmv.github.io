---
section: os_guide
title: "Учебное пособие по операционным системам"
# permalink: /wd/textbook
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