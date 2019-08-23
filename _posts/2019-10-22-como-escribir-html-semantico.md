---
layout: post
title:  "Cómo escribir HTML semántico"
category: articles
tags: programming español html css
location: La Plata, Argentina
visible: true
---

Cuando recién comenzaba a armar sitios web, escribir HTML y CSS era un reto.
No sabía mucho de programación y diseño y podía tardar horas en lograr que mi sitio web se viera como quería.

Usar Bootstrap por primera vez fue un alivio:
sin ayuda y con muy poco esfuerzo podía crear sitios web de buena calidad.
Me acostumbré rápidamente, y lo usé en todos mis proyectos desde entonces.

Pero con el tiempo aprendí que los frameworks vienen con un costo: Sus convenciones te fuerzan a estructurar el código de una manera que no siempre es la más conveniente.

Por ejemplo, abusar de las clases **container**, **row**, **col** y **offset**, hace que tu HTML se vea así:

``` html
<div class="container">
  <div class="row">
    <div class="col-xs-12 col-sm-12 col-md-8 col-me-offset-2 col-lg-8 col-lg-offset-2 well">
      <div class="container-fluid">
        <div class="row">
          <div class="col-xs-12 text-center">
            <h1>Descargar archivos</h1>
            <p class="small">( Rastreando )</p>
            <br />
            <p>Descarga los archivos a continuación.</p>
            <!--If expiry date exists-->
              <p class="green">Tienes 5 días para descargar los archivos.</p>
            <!--end if-->
            <div class="clearfix"></div>
          </div>
        </div>
        <hr class="dotted"/>
        ...
```

Cuando el mismo archivo podría verse así:

``` html
<section class="file-pick-up">
  <h1>Descargar archivos</h1>
  <p class="state">( Rastreando )</p>
  <p>Descarga los archivos a continuación.</p>
  <p class="expire-warning">
    Tienes 5 días para descargar los archivos.
  </p>
</section>
```

En el primer ejemplo, hay hasta ocho niveles de anidamiento. El código es difícil de seguir. No es claro que significa cada parte. Las clases no nos describen qué es lo que estamos mirando, sino cómo tiene que verse.

Ese código es el resultado de haber olvidado una de las primeras lecciones que nos enseñan: **debemos separar la estructura (HTML) del estilo (CSS)**.

A esto se lo llama HTML semántico. El HTML no debe preocuparse por si los elementos van a estar dispuestos en columnas, o cómo tienen que distribuirse en diferentes tamaños de pantalla **¡Eso es el trabajo del CSS!**

Cuando separamos el contenido del estilo, como lo hicimos en el segundo ejemplo, el HTML se vuelve más evidente, más corto, más fácil de leer y más fácil de modificar.

En el proyecto en el que trabajo actualmente hay más de 200 largos archivos HTML escritos como el primer ejemplo, y cuando tengo que hacer alguna modificación, paso un buen rato tratando de limpiar un poco el código. Pero este es tan complejo que se me dificulta entender dónde empieza y termina cada bloque.

Cuando descubrí las ventajas del HTML semántico, comencé a investigar otros frameworks CSS.
Pero no me gustó ninguno. Casi todos ellos ofrecían un **sistema de grids**, o de alguna forma alentaban a escribir HTML de una forma complicada.

Decidí, entonces, no usar un framework para mi siguiente proyecto, y fue una experiencia muy enriquecedora.

Me tomé mi tiempo para escribir el código de forma prolija, empezando por cómo quería que se viera la estructura del sitio web:

``` html
<body>
  <header class="site-header">
    <section class="brand">
      <a href="/">Mi sitio web</a>
    </section>
  </header>

  <nav class="site-nav">
    <a class="site-nav-link" href="/">Inicio</a>
    ...
  </nav>

  <main class="site-main">
    ...
  </main>

  <footer class="site-footer">
    Creado por Nicanor Perera
  </footer>
</body>
```

Quería que se viera así de simple.
Nada de `container` ni `container-fluid`, ni de `rows`, ni de `col-md, col-sm, col-xs`, ni de `clearfix`.

A mi HTML no le importa si la página está dividida en columnas o filas.
Lo que sabe es que hay un encabezado, un menú de navegación, un cuerpo principal y un pié de página; y las nuevas etiquetas de HTML5 me ayudaron a describir el propósito de cada una de estas secciones:
* header
* nav
* main
* footer

El siguiente paso fue describir, usando CSS, cómo quería que **se viera** la página.
Quería que el encabezado se ubique encima, el menú de navegación a la izquierda, el cuerpo de la página a su derecha, y el pié de página debajo.

De haber usado Bootstrap, hubiera hecho casi todo el trabajo en el HTML:

``` html
<body>
<header class="navbar navbar-inverse">
  <div class="container-fluid">
    <div class="navbar-header">
      <button type="button" class="navbar-toggle" data-toggle="collapse" data-target="#myNavbar">
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>                        
      </button>
      <a class="navbar-brand" href="#">My sitio web</a>
    </div>
    <div class="collapse navbar-collapse" id="myNavbar">
      <ul class="nav navbar-nav">
        <li class="active"><a href="/">Inicio</a></li>
        ...
      </ul>
    </div>
  </div>
</header>

<div class="container-fluid text-center">    
  <div class="row content">
    <div class="col-md-3 col-sm-4 sidenav">
      <ul class="nav">
        <li class="nav-item">
          <a class="nav-link active" href="/">Active</a>
        </li>
      </ul>
    </div>
    <div class="col-md-9 col-sm-8 text-left">
      <h1>Bienvenido</h1>
      <p>...</p>
    </div>
  </div>
</div>

<footer class="container-fluid text-center">
  <p>Footer Text</p>
</footer>
</body>
```

Pero ahora que no usaba Boostrap, era claro que tenía que amigarme con el CSS e investigar mis opciones. Venía con muchas ganas de probar `display: grid` y me maravilló lo simple que era lograr la estructura que quería:

```css
.site-header { grid-area: header; }
.site-nav    { grid-area: nav; }
.site-main   { grid-area: main; }
.site-footer { grid-area: footer; }

body {
  display: grid;
  grid-template-areas:
    'header  header'
    'nav    main'
    'footer footer';
  grid-template-rows: 8rem 1fr 8rem;
  grid-template-columns: 24rem 1fr;
}
```

Con esta fórmula, si decido cambiar de estilo, no necesito tocar el HTML.
Por ejemplo, si quisiera que el navegador esté debajo del encabezado, bastaría con modificar un poco el CSS:

```
grid-template-areas:
  'header'
  'nav'
  'main'
  'footer';
```

Me tomé mi tiempo para revisar el código varias veces, y borrar lo que no servía.
Para organizar mis archivos CSS de una forma que tuviera sentido.

Tardé un poco más que lo que hubiera tardado en armar el sitio con Bootstrap, pero aprendí muchísimo en el camino, y tanto el código HTML como el CSS terminaron siendo 3 o 4 veces más cortos que si hubiera usado Bootstrap.

Me gustó tanto el resultado, que tomé todo lo que aprendí y decidí crear mi propio sistema de estilos:
No quería crear un Framework que me obligara a escribir de una cierta forma, sino más bien una guía estilos y forma de de organización que me sirviera para comenzar un proyecto con HTML y CSS semánticos en segundos.

Mi investigación me llevó a buscar una forma de organizar los estilos que fuera simple y elegante y en la cual sea evidente dónde realizar cada cambio.

Me puse a reflexionar sobre las distintas partes que conforman un sitio web, y las razones que hay para modificar un estilo, y separé los estilos en cuatro grupos.

* **Estilos Base:** Son comunes a todo el sitio web. Incluyen los colores, las tipografías, tamaños de los títulos, estilos de los links, y de los párrafos. Describen la esencia del sitio web. Se aplican directamente a tags generales, como `body`, `p`, `h1`, `a`.
* **Estilos del Layout:** Describen la estructura general del sitio web y sus partes. Posición, tamaño y estilos generales del encabezado, navegador, contenido y pié de página.
* **Estilos de Componentes:** Elementos reusables como botones, formularios, imágenes y tablas. A diferencia de los estilos base, estos se aplican a clases, ej: `.btn` o `.table`.
* **Estilos específicos:** Elementos únicos. Por ejemplo `.author-name`, `.download-button`.

Por ejemplo, el directorio de estilos de una de mis aplicaciones tiene esta estructura:
```
 scss
  ├── base
  │   ├── Base.scss
  │   ├── Colors.scss
  │   ├── Images.scss
  │   ├── Normalize.scss
  │   └── Typography.scss
  ├── layout
  │   ├── Layout.scss
  │   ├── SiteHeader.scss
  │   ├── SiteNav.scss
  │   ├── SiteMain.scss
  │   └── SiteFooter.scss
  ├── components
  │   ├── Button.scss
  │   ├── Form.scss
  │   └── Table.scss
  ├── specific
  │   ├── Home.scss
  │   └── SearchForm.scss
  └── App.scss
```

En este caso uso SCSS, porque me gusta poder anidar estilos, y usar variables para los colores.
Todos los colores que uso en el sitio tienen nombre y están definidos en `/base/colors`:

``` scss
$gold: #Ff6800;
$river: #3498db;
$dark-river: #2980b9;
$clouds: #fafafa;
$silver: #bdc3c7;
$coal: #222;
$white: #fff;
$black: #000;

$brand-color: $river;
$emphasized-brand-color: $dark-river;
$text-color: $white;
$base-color: $black;
$pale-color: $clouds;
$line-color: $silver;
```

De esta forma, si necesito hacer un cambio en un color este es el único archivo que tengo que modificar.
En todos los demás archivos uso el nombre de la variable:

``` scss
// Link
a {
  color: $brand-color;
  text-decoration: none;

  &:focus,
  &:hover {
    color: $text-color;
  }
}
```

La mayoría de los archivos tienen menos de 30 lineas de código, y puedo ver todo su contenido sin mover la ruedita del mouse. Por ejemplo, el archivo `base/Images.scss` de esta aplicación de ejemplo tiene sólo 3 líneas de código:

```
img {
  max-width: 100%;
}
```

Después de bastante esfuerzo, puedo decir que he cumplido mi objetivo: Ahora cuento con un sistema HTML + CSS con el que puedo arrancar [un proyecto web](https://github.com/nicanor/acordes/tree/master/assets/css) en pocos segundos y que me permite escribir código simple, semántico y mantenible a niveles que no pensaba que era posible.

Es sin dudas un camino de ida para mí, y espero con ansias comenzar el próximo proyecto sin usar un framework CSS.
