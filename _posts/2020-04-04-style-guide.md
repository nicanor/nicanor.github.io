---
layout: post
title:  "Style Guide"
category: articles
tags: programming html css
location: La Plata, Argentina
visible: false
---

## Use Semantic class names

Class names should not tell us how an element looks:
``` html
<article class="color-red pull-left text-center">
  You are in danger!
</article>
```

Class names should describe what an element represents:
``` html
<article class="alert">
  You are in danger!
</article>
```

We use CSS to tell how the element should look like:
``` css
.alert {
  float: left;
  color: red;
  text-align: center
}
```


## Don't use Grid Classes:

We should avoid using `container`, `row`, `col-*` and others:
``` html
<main class="page">
  <div class="container">
    <div class="row">
      <div class="col-xs-12 col-sm-12 col-md-8">
        Important information
      </div>
      <div class="col-xs-12 col-sm-12 col-md-4">
        Extra information
      </div>
    </div>
  </div>
</main>
```

Instead we should try to use good class names:
``` html
<main class="page">
  <article class="important-information">
    Important information
  </article>

  <aside class="extra-information">
    Extra information
  </aside>
</main>
```

And style with CSS:
``` css
.page {
  display: flex;
  justify-content: space-between;
}
```


## Don't use divs for everything

``` html
<body>
  <div class="site-header">
    <a href="/">Mi sitio web</a>
  </div>

  <div class="site-nav">
    <a class="site-nav-link" href="/">Home</a>
    ...
  </div>

  <div class="site-main">
    <div class="page-title">Title</div>
    <div class="page-body">
      Body
      <div class="other-news">
        Some other news
      </div>
      <div class="page-aside">Aside</div>
    </div>
  </div>

  <div class="site-footer">
    Creado por Nicanor Perera
  </div>
</body>
```

Use HTML5 more semantic tags `main`, `nav`, `header`, `footer`, `section`, `article`:
``` html
<body>
  <header class="site-header">
    <a href="/">Mi sitio web</a>
  </header>

  <nav class="site-nav">
    <a class="site-nav-link" href="/">Home</a>
    ...
  </nav>

  <main class="site-main">
    <h1 class="page-title">Title</h1>
    <section class="page-body">
      Body
      <article class="other-news">
        Some other news
      </article>
      <aside class="page-aside">Aside</aside>
    </section>
  </main>

  <footer class="site-footer">
    Creado por Nicanor Perera
  </footer>
</body>
```

## Avoid unnecesary nesting:

Don't add more tags than needed:
``` html
<nav class="navbar">
  <div class="container-fluid">
    <div class="collapse navbar-collapse">
      <ul class="nav navbar-nav">
        <li class="active">
          <a href="/">Home</a>
        </li>
        <li>
          <a href="/assets">Assets</a>
        </li>
      </ul>
    </div>
  </div>
</nav>
```

Instead, try to reduce the number of elements.

Every element should do useful work.
``` html
<nav class="site-nav">
  <a class="site-nav-item active" href="/">Home</a>
  <a class="site-nav-item" href="/assets">Assets</a>
</nav>
```
