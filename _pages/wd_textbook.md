---
title: "Конспект лекций по веб-разработке"
permalink: /wd/textbook
layout: textbook

section: wd

---


{% for p in site.text %}
  {% if p.section == page.section %}
<h2 id="{{ p.title }}"><a href="{{ p.url }}">{{ p.title }}</a> </h2>

<div>
{{ p.content }} 
</div>

  {% endif %}
{% endfor %}
