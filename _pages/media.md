---
title: Работа со СМИ
layout: archive
classes: wide
permalink: /media/
entries_layout: grid
toc: true
---

{% assign entries_layout = 'grid' %}
{% for category in site.categories %}
  {% if category[0] == "tv" %}
<section id="{{ category[0] | slugify | downcase }}" class="taxonomy__section">
<h2 class="archive__subtitle">Выступления на телевидении</h2>
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
  {% if category[0] == "comment" %}
<section id="{{ category[0] | slugify | downcase }}" class="taxonomy__section">
<h2 class="archive__subtitle">Комментарии</h2>
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
<h2 class="archive__subtitle">Участие в подкастах</h2>
<div class="entries-{{ entries_layout }}">
  {% for post in category.last %}
    {% include archive-single.html type=entries_layout %}
  {% endfor %}
</div>
<a href="#page-title" class="back-to-top">{{ site.data.ui-text[site.locale].back_to_top | default: 'Back to Top' }} &uarr;</a>
</section>
  {% endif %}
{% endfor %}
