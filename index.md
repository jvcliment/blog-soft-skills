---
layout: default
title: Inicio
---

<section class="home-wrap">
  <h2 class="home-title">Recent articles</h2>

  <div class="post-list">
    {% for post in site.posts %}
      {% assign words = post.content | markdownify | strip_html | split: ' ' | size %}
      {% assign minutes = words | plus: 199 | divided_by: 200 %}
      {% assign date_str = post.date | date: "%-d %b '%y" | upcase %}

      <article class="post-card">
        {% if post.image %}
          <a class="thumb" href="{{ post.url | relative_url }}">
            <img src="{{ post.image | relative_url }}" alt="{{ post.title }}">
          </a>
        {% endif %}

        <div class="body">
          <div class="meta">
            <span class="date">{{ date_str }}</span>
            <span class="readtime">{{ minutes }} min read</span>
          </div>

          <h2 class="title">
            <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
          </h2>

          <p class="excerpt">
            {{ post.description | default: post.excerpt | strip_html | truncate: 180 }}
          </p>
        </div>
      </article>

      {% unless forloop.last %}<hr class="divider">{% endunless %}
    {% endfor %}
  </div>
</section>
