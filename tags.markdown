---
layout: default
title:  "Tags"
---

<ul>
  {% for tag in site.tags %}
    <li>
    {{ tag[0] }}
  {% endfor %}
</ul>

<ul>
  {% for tag in site.tags %}
    <li>
    {{ tag[1].excerpt }}
  {% endfor %}
</ul>
