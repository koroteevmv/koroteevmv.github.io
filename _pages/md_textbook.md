---
title: "Учебник по мобильной разработке"
permalink: /md/textbook
layout: textbook
toc: false
read_time: true
share: true
comments: true
related: true
word_count: true
excerpt: ""

section: md

---

{% for p in site.text %}
  {% if p.section == page.section %}
<h2 id="{{ p.title }}"><a href="{{ p.url }}">{{ p.title }}</a> </h2>
{{ p.content }} 
  {% endif %}
{% endfor %}

