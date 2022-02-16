---
title: "Учебник по сетевым системам и приложениям"
permalink: /os/textbook
layout: textbook

section: os

---


{% for p in site.text %}
  {% if p.section == page.section %}
<h2 id="{{ p.title }}"><a href="{{ p.url }}">{{ p.title }}</a> </h2>

<div>
{{ p.content }} 
</div>

  {% endif %}
{% endfor %}
