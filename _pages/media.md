---
title: Работа со СМИ
layout: single
classes: wide
permalink: /media/
---

{% assign entries_layout = 'grid' %}
{% for category in site.categories %}
  {% if category[0] == "tv" %}
<section id="{{ category[0] | slugify | downcase }}" class="taxonomy__section">
<h1 class="archive__subtitle">Выступления на телевидении</h1>
<div class="entries-{{ entries_layout }}">
  {% for post in category.last %}
    {% include archive-single.html type=entries_layout %}
  {% endfor %}
</div>
<a href="#page-title" class="back-to-top">{{ site.data.ui-text[site.locale].back_to_top | default: 'Back to Top' }} &uarr;</a>
</section>
  {% endif %}
{% endfor %}

{% assign entries_layout = 'list' %}
{% for category in site.categories %}
  {% if category[0] == "media" %}
<section id="{{ category[0] | slugify | downcase }}" class="taxonomy__section">
<h1 class="archive__subtitle">Комментарии в прессе</h1>
<div class="entries-{{ entries_layout }}">
  {% for post in category.last %}
    {% include archive-single.html type=entries_layout %}
  {% endfor %}
</div>
<a href="#page-title" class="back-to-top">{{ site.data.ui-text[site.locale].back_to_top | default: 'Back to Top' }} &uarr;</a>
</section>
  {% endif %}
{% endfor %}


{% assign entries_layout = 'grid' %}
{% for category in site.categories %}
  {% if category[0] == "podcast" %}
<section id="{{ category[0] | slugify | downcase }}" class="taxonomy__section">
<h1 class="archive__subtitle">Участие в подкастах</h1>
<div class="entries-{{ entries_layout }}">
  {% for post in category.last %}
    {% include archive-single.html type=entries_layout %}
  {% endfor %}
</div>
<a href="#page-title" class="back-to-top">{{ site.data.ui-text[site.locale].back_to_top | default: 'Back to Top' }} &uarr;</a>
</section>
  {% endif %}
{% endfor %}
