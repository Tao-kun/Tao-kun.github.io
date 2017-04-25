---
layout: default
title:  "Tags"
---

{% for tag in site.tags %}
    {{ tag[0] }}
    {{ tag[1] }}
{% endfor %}