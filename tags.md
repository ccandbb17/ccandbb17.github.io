---
layout: page
title: 标签
permalink: /tags/
---

点击标签查看相关博客文章。

<ul class="tags">
{% for tag in site.tags %}
  {% assign t = tag | first %}
  {% assign posts = tag | last %}
  <li><a href="/tag/#{{t | downcase | replace:" ","-" }}">{{ t | downcase }}</a> {{ posts | size }}篇</li>
{% endfor %}
</ul>

---

{% for tag in site.tags %}
  {% assign t = tag | first %}
  {% assign posts = tag | last %}

<h4><a name="{{t | downcase | replace:" ","-" }}"></a><a class="internal" href="/tag/#{{t | downcase | replace:" ","-" }}">{{ t | downcase }}</a></h4>
<ul>
{% for post in posts %}
  {% if post.tags contains t %}
  <li>
    <a href="{{ post.url }}">{{ post.title }}</a>
    <span class="date">{{ post.date | date: "%Y-%m-%d" }}</span>
  </li>
  {% endif %}
{% endfor %}
</ul>

---

{% endfor %}
