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

{% for tag in site.tags %}
  <a href="/show_by_tag.html?tag={{ tag[0] }}"> {{ tag[0] }}</a>
{% endfor %}