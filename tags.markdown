---
layout: default
title:  "Tags"
---

<ul>
  {% for tag in site.tags %}
    <li>
    {{ tag[0] }}
    </li>
  {% endfor %}
</ul>

<ul>
  {% for tag in site.tags %}
    <li>
    {{ tag }}
    </li>
  {% endfor %}
</ul>
