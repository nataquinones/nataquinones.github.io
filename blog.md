---
layout: page
title: Blog
permalink: /blog
---

<ul>
{% for post in site.categories.blog %}
  {% capture y %}{{post.date | date:"%Y"}}{% endcapture %}
  {% if year != y %}
    {% assign year = y %}
    <li class="blog-list-subtitle">{{ y }}</li>
  {% endif %}
  <li >
    <time class="blog-list-item" datetime="{{ post.date | date:"%Y-%m-%d" }}">
    {{ post.date | date:"%Y-%m-%d" }}
    </time>
    <a href="{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a>
  </li>
{% endfor %}
</ul>