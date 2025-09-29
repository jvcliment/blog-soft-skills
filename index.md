---
layout: default
title: Inicio
---

<style>
  /* ======= Home styles (auto-contenidos) ======= */
  :root{
    --bg:#272b33;        /* fondo principal */
    --card:#2f3440;      /* fondo tarjeta */
    --text:#d7dde8;      /* texto principal */
    --muted:#a5adbb;     /* texto secundario */
    --accent:#76e39a;    /* verde fecha */
    --border:#3a3f4c;    /* separadores */
  }
  .home-wrap{
    max-width: 980px; margin: 2.5rem auto 4rem; padding: 0 1rem;
    color: var(--text); font-weight: 400;
  }
  .home-title{
    text-align:center; font-size: clamp(1.6rem, 2.2vw, 2.1rem);
    font-weight: 700; margin: 0 0 1.8rem;
  }
  .post-list{ display: grid; gap: 1.6rem; }
  .post-card{
    display:grid; grid-template-columns: 280px 1fr; gap: 1.4rem; align-items:start;
    padding: 1.1rem 0;
  }
  .thumb{
    width:100%; aspect-ratio:16/9; border-radius: 8px; overflow:hidden; background:#000;
    box-shadow: 0 0 0 1px rgba(0,0,0,.25);
  }
  .thumb img{ width:100%; height:100%; object-fit:cover; display:block; }
  .meta{
    display:flex; justify-content:space-between; align-items:center; margin-bottom:.35rem;
    font-size:.95rem; letter-spacing:.4px;
  }
  .date{ color: var(--accent); font-weight:700; text-transform: uppercase; }
  .readtime{ color: var(--muted); white-space:nowrap; }
  .title{ font-size: clamp(1.15rem, 2.2vw, 1.75rem); font-weight:700; line-height:1.25; margin:.15rem 0 .35rem; }
  .title a{ color: var(--text); text-decoration:none; }
  .title a:hover{ text-decoration:underline; }
  .excerpt{ color: var(--muted); font-size:1.05rem; line-height:1.5; margin:0; }
  .divider{ border:0; border-top:1px solid var(--border); margin: .6rem 0 0; }
  @media (max-width: 760px){
    .post-card{ grid-template-columns: 1fr; }
    .thumb{ aspect-ratio: 21/9; }
  }
</style>

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
