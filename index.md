---
layout: default
title: Inicio
---

# Bienvenido a mi blog 👋

Aquí iré publicando mis entradas.  

## Entradas recientes
<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
      <small>({{ post.date | date: "%Y-%m-%d" }})</small>
    </li>
  {% endfor %}
</ul>

