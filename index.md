---
layout: none
title: Inicio
---

<section class="home">
  <h2>Recent Articles</h2>

  <div class="post-list">
    {% for post in site.posts %}
      {% assign words = post.content | markdownify | strip_html | split: ' ' | size %}
      {% assign minutes = words | plus:199 | divided_by:200 %} {% comment %} ~200 wpm, redondeo hacia arriba {% endcomment %}


      <article class="post-card">
        {% if post.image %}
          <a class="post-thumb" href="{{ post.url | relative_url }}">
            <img src="{{ post.image | relative_url }}" alt="{{ post.title }}">
          </a>
        {% endif %}

        <div class="post-body">
          <h3 class="post-title">
            <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
          </h3>

          <div class="post-meta">
            <span>{{ post.date | date: "%Y-%m-%d" }}</span>
            <span>•</span>
            <span>{{ minutes }} min read</span>
          </div>

          <p class="post-excerpt">
            {{ post.description | default: post.excerpt | strip_html | truncate: 160 }}
          </p>
        </div>
      </article>
    {% endfor %}
  </div>
</section>
