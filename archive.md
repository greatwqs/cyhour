---
layout: page
title: 归档
permalink: /archive/
date: 2011-11-01
---

{% for post in site.posts  %}
  {% capture this_year %}{{ post.date | date: "%Y" }}{% endcapture %}
  {% capture next_year %}{{ post.previous.date | date: "%Y" }}{% endcapture %}

  {% if forloop.first %}
  <h2 id="{{ this_year }}-ref">{{this_year}}</h2>
  <ul>
  {% endif %}

  <li>
    <small class="date">{{ post.date | date: "%Y-%m-%d" }}</small>
    <a href="{{ post.url }}">{{ post.title }}</a>
  </li>

  {% if forloop.last %}
  </ul>
  {% else %}
  {% if this_year != next_year %}
  </ul>
  <h2 id="{{ next_year }}-ref">{{next_year}}</h2>
  <ul>
  {% endif %}
  {% endif %}
{% endfor %}
