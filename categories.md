---
layout: page
title: 分组
permalink: /categories/
---

请点击各分组查看相关博客文章。

<ul class="categories">
{% for category in site.categories %}
  {% assign c = category | first %}
  {% assign posts = category | last %}
  <li><a href="/categories/#{{c | downcase | replace:" ","-" }}">{{ c | downcase }}</a> {{ posts | size }}篇</li>
{% endfor %}
</ul>

---

{% for category in site.categories %}
  {% assign c = category | first %}
  {% assign posts = category | last %}

<h4><a name="{{c | downcase | replace:" ","-" }}"></a><a class="internal" href="/categories/#{{c | downcase | replace:" ","-" }}">{{ c | downcase }}</a></h4>
<ul>
{% for post in posts %}
  {% if post.categories contains c %}
  <li>
    <a href="{{ post.url }}">{{ post.title }}</a>
    <span class="date">{{ post.date | date: "%Y-%m-%d" }}</span>
  </li>
  {% endif %}
{% endfor %}
</ul>

---

{% endfor %}
