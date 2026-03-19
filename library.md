---
layout: default
title: Library
---

# Englsih series

<div style="display: flex; flex-wrap: wrap;">
{% for book in site.data.books %}
  <div style="border: 1px solid #ccc; margin: 10px; width: 200px; padding: 10px;">
    <img src="{{ book.cover }}" width="100%">
    <h3>{{ book.title }}</h3>
    <p>publisher：{{ book.publisher }}</p>
    <p>{{ book.desc }}</p>
  </div>
{% endfor %}
</div>
