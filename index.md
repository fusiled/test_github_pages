---
layout: default
title: ROOT
---

{% assign root = "/" %}
{% assign folders = "" | split: "" %}

{% for file in site.static_files %}
  {% if file.path contains root %}
    {% assign rest = file.path | remove_first: root %}
    {% assign parts = rest | split: "/" %}

    {% if parts.size > 1 %}
      {% assign folder = parts[0] %}
      {% unless folders contains folder %}
        {% assign folders = folders | push: folder %}
      {% endunless %}
    {% endif %}
  {% endif %}
{% endfor %}

<ul>
{% for folder in folders %}
  <li>
    <a href="{{ root | append: folder | append: '/' | relative_url }}">
      {{ folder }}/
    </a>
  </li>
{% endfor %}
</ul>
