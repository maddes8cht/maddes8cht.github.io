---
title: Posts
layout: page
---
<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
      {{post.excerpt}}
      {{post.content}}
    </li>
  {% endfor %}
</ul>
