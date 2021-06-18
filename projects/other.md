---
layout: page
title: Projects
permalink: /projects/other
---

{% include nav_sub.html  %}

{% for post in site.categories.other %}
<div class="project-item">
  <div class="icon">
    {% if post.img %}
      <a href="{{ post.url }}"><img src="{{ post.img }}"></a>
    {% endif %}
  </div>

<div class="text">
      {% if post.alt_url %}
          <p class="title"><a href="{{ post.alt_url }}">{{ post.title }}</a>
      {% else %}
      <p class="title"><a href="{{ post.url }}">{{ post.title }}</a>
      {% endif %}
            {% if post.github %}
            <span style="float: right">
              <a href="{{ post.github }}" target="_blank">
                <i class="fa fa-github fa-1x" aria-hidden="true"></i>
              </a>
            </span>
            {% endif %}
          </p>
          {% if post.author %}
        <span class="author">{{ post.author }}</span>
        {% endif %}
        <div class="desc">
       {{ post.description }}
       </div>
      </div>

</div>

{% endfor %}