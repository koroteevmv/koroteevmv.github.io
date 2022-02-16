---
title: "Учебник по мобильной разработке"
permalink: /md/textbook
layout: textbook

section: md

---

{% for p in site.text %}
  {% if p.section == page.section %}
<h2 id="{{ p.title }}"><a href="{{ p.url }}">{{ p.title }}</a> </h2>
{{ p.content }} 
  {% endif %}
{% endfor %}

