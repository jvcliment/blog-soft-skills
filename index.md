---
layout: default
title: Inicio
---

<style>
  .site-header { border-top: 0 !important; }

  .site-footer { display: none !important; }

  .page-content { padding: 0; }

  .home-wrap {
    max-width: 980px; 
    margin: 2.5rem auto 4rem; 
    padding: 0 1rem;
  }

  .home-title {
    text-align: center; 
    font-size: clamp(1.6rem, 2.2vw, 2.1rem); 
    font-weight: 700; 
    margin: 0 0 1.8rem;
  }

  .post-list {
    display: grid; 
    gap: 1.6rem;
  }

  .post-card {
    display: grid; 
    grid-template-columns: 280px 1fr;
    gap: 1.4rem;
    align-items: start;
    padding: 1.1rem 0;
  }

  .thumb {
    width: 100%; 
    aspect-ratio: 16/9; 
    border-radius: 8px; 
    overflow: hidden; 
    background: #000;
  }

  .thumb img {
    width: 100%; 
    height: 100%; 
    object-fit: cover; 
    display: block;
  }

  .meta {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: .35rem;
    font-size: .95rem;
    letter-spacing: .4px; 
  }

  .date {
    color: #0a7d37;
    font-weight: 700;
    text-transform: uppercase;
  }

  .readtime {
    color: #6b7280;
    white-space: nowrap;
  }

  .title {
    font-size: clamp(1.15rem, 2.2vw, 1.75rem);
    font-weight: 700;
    line-height: 1.25;
    margin: .15rem 0 .35rem;
  }

  .title a {
    color: inherit;
    text-decoration: none;
  }

  .title a:hover { text-decoration: underline; }

  .excerpt {
    color: #4b5563;
    font-size: 1.05rem;
    line-height: 1.5;
    margin: 0;
  }

  .divider {
    border: 0;
    border-top: 1px solid #e5e7eb;
    margin:.6rem 0 0;
  }

  @media (max-width: 760px) { 
    .post-card {
      grid-template-columns: 1fr; 
    } 
    
    .thumb { 
      aspect-ratio: 21/9; 
    } 
  }

  .title a, .site-title, .page-link {
    transition: color 0.2s ease;
  }
   
  .title a:hover, .site-title, .page-link {
    text-decoration: none !important;
    color: #282828;
  }


</style>

<section class="home-wrap">
  <h1 class="home-title">Entradas recientes</h1>

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
            <span class="readtime">{{ minutes }} min de lectura</span>
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
