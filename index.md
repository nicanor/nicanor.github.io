---
layout: default
description: "Opiniones y experiencias de Nicanor Perera - Programador"
id: home
---

<div class="hero">
  <div class="hero-inner">
    <img class="hero-logo" src="/img/code.png" alt="">
    <h1>{{ site.title }}</h1>
    <p>{{ site.description }}</p>
  </div>
</div>

<div class="articles">
  <div class="articles-inner">
    <h2>Artículos</h2>
    <ul>
      {% for article in site.categories.articles %}
        {% if article.visible == true %}
          <li>
            <a href="{{ article.url }}"> {{ article.title }}</a>
          </li>
        {% endif %}
      {% endfor %}
    </ul>
  </div>
</div>
