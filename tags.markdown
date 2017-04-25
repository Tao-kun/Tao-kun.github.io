---
layout: default
title:  "Tags"
---

<ul>
  {% for tag in site.tags %}
    <li>
    {{tag[0]}}
    <br />
    {{ tag[1].title }}
    </li>
  {% endfor %}
</ul>
