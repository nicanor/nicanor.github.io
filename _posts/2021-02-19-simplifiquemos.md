---
layout: post
title:  "Simplifiquemos"
category: articles
tags: programming talk español
location: La Plata
visible: true
---

Transcripción de la charla que dí en Agosto de 2022 en el Nerdearla 101.

Originalmente preparé esta charla para programadores de [Snappler](https://www.snappler.com/) el 19 de Febrero de 2021 y la repetí el 31 de enero de 2022.

[Acá pueden descargar las diapositivas]({{ site.url }}/img/charla-snappler/charla-snappler-2021.pdf)


## Cómo escribir bien

Escribir claro es fundamental para comunicarnos de manera efectiva.

Los programadores escribimos emails, tareas, tickets, casos de uso, comentarios, documentación y también escribimos código de software.

Pero expresar una idea con palabras y que la persona que las lee entienda exactamente lo que quiero decir no es tarea fácil

Hace unos años estaba en la búsqueda de cómo escribir y comunicarme mejor.

Los consejos más comunes que encontré para escribir claro fueron:

- Hablá en voz activa.
- Reducí la cantidad de adjetivos y adverbios.
- Usá palabras sencillas:
  - No digas *denominación* si podés decir *nombre*.
  - No digas *sufragio* si podés decir *voto*.
  - No digas *con la finalidad de* si podés decir *para*.
  - No escribas complicado para parecer importante. No digas que *estás anticipando experimentar una precipitación considerable* si podés decir que *puede llover*.
- Pero también usá palabras precisas. No digas que el presidente se fue de la empresa. ¿Renunció, se retiró o lo echaron?

Con el tiempo fui mejorando mi escritura, pero sentía que todavía me faltaba algo.

Lo que me faltaba lo encontré en el libro **On writting well**. El libro habla de cómo escribir bien. Está en Inglés, pero los consejos que dá aplican también al Español. Es un libro que vuelvo a leer todos los años.

Fue escrito por un periodista Estadounidense llamado William Zinsser.

Según él, **el secreto de la buena escritura es reducir cada oración a sus componentes más limpios**, y para lograr eso hay que asegurarse que **cada palabra esté haciendo trabajo útil**.

La facultad de Ciencias Económicas de la Universidad de Córdoba tiene [un buen ejemplo](https://ecptgu.eco.catedras.unc.edu.ar/unidad-1/en-las-instituciones/el-lenguaje-claro/).
Tomaron el borrador de un texto y le aplicaron varias correcciones:

> Ante la evidente necesidad de otorgar a la ciudadanía la atención con la calidad que ésta solicita y con la finalidad de crear un Gobierno de Calidad que brinde trámites y servicios que satisfagan las necesidades y expectativas de la ciudadanía, el Gobierno Federal está enfocando sus esfuerzos en fomentar programas que permitan transparentar e incrementar la calidad en los trámites y servicios de alto impacto ciudadano, a partir de la implantación de acciones de mejoras derivadas de la opinión ciudadana.

Cuando tenemos que leer algo varias veces para entenderlo, es porque está escrito de forma complicada. El sujeto está en la mitad del texto, y la parte más importante está por el final. Hace juicios de valor, es impreciso y usa muchas palabras largas. Todo esto hace que sea difícil de leer.

Estas personas se preguntaron: ¿Qué es lo que estoy queriendo decir? y después de aplicar varias correcciones terminaron con un texto mucho más fácil de procesar:

> El Gobierno Federal realiza acciones de mejora, derivadas de la opinión pública, para incrementar la  calidad de los trámites y servicios más utilizados por los ciudadanos.

Y yo creo que a este texto todavía se le pueden seguir aplicando correcciones. Si yo tuviera que reescribirlo, escribiría algo como esto:

> El Gobierno Federal escuchó a los ciudadanos y mejorará los trámites y servicios que más usan.

Una vez que quitamos la suciedad el texto es mucho más fácil de leer.

Según Zinsser, escribir es trabajo difícil.
Y una sentencia clara no es un accidente.
Muy pocas sentencias salen bien la primera vez, la segunda o incluso la tercera vez.

La mayoría de los borradores pueden ser cortados en un cincuenta porciento sin perder nada de información y sin perder la voz del escritor.

Para escribir una nota periodística, él escribía un título, luego el primer párrafo, el segundo, el tercero. Y recién el tercero le gustaba. Entonces borraba los dos primeros, cambiaba el nombre del titulo y escribía un par de parrafos más.

Se daba cuenta que los párrafos quedaban mejor si les cambiaba de orden. Corregía y lo reducía a la mitad. Separaba algunos parrafos en dos, o unía dos parrafos en uno.

Y se iba a dormir.

Al día siguiente con la cabeza descansada volvía a leerlo. Se preguntaba: "¿Estoy escribiendo lo que quiero decir?". Volvía a repetir el proceso una y otra vez, hasta que terminaba con el texto tal y como lo quería. Escribir una nota le podía tomar varios días

**Según Zinsser, la esencia de escribir es reescribir**.

Pero no hace falta ser un genio de la escritura para escribir bien.
La mayoría de los escritores que admiramos no son genios.
Son personas comunes que lograron dominar su escritura a través de trabajo constante.

Borges era un obsesivo de la corrección.
Tanto que decía que la razón por la que publicaba, era para dejar de corregir.

La buena escritura es el resultado de trabajo iterativo.

La próxima vez que escriban un email, tarea, mensaje, comentario o documentación tomense unos minutos para corregirlo. Sus colegas lo van a agradecer.


## On writting HTML well

Hoy voy a hablarles de cómo escribir HTML bien.

Hay personas que desestiman HTML.
Dicen que escribir HTML es fácil.
Dicen que escribir HTML no es programar.
No le prestan la atención que se merece.

Y eso es un gran error.

Cuando no cuidamos nuestro código, terminamos con HTML críptico, poco expresivo, poco accesible, muy anidado y difícil de entender. Mantener este código se vuelve una tarea tediosa y frustrante.

Una aplicación web mediana tiene cientos de archivos HTML.
Escribir HTML bien es fundamental para lograr un código web mantenible.


Para escribir bien HTML, la regla más importante es separar estructura de estilo.

- El código HTML tiene que describir la estructura de nuestro sitio web.
- El código CSS tiene que describir cómo se ve nuestro sitio web.

Por ejemplo, miremos este código. Tenemos un artículo con texto *"Estás en peligro!"*. Y clases *color-red*. *pull-left* y *text-center*:

``` html
<article class="color-red pull-left text-center">
  Estás en peligro!
</article>
```

Este código rompe la regla. Los nombres de las clases no describen qué es el elemento, sino que describen cómo tiene que verse.

No hay tanta diferencia entre esto y poner los estilos en linea:

``` html
<article style="color: red; float: left; text-align: center;">
  Estás en peligro!
</article>
```

En ambos casos, cuanto leo el código HTML recibo pistas de cómo se ve.
Y eso es lo que queremos evitar.

Si tengo que elegir entre esos dos ejemplos, prefiero los estilos en linea, porque por lo menos es explícito que está modificando los estilos. Y además no necesito definir las clases *color-red*. *pull-left* y *text-center*:

``` css
.pull-left{
  float: left;
}

.color-red {
  color: red;
}

.text-center {
  text-align: center;
}
```

Los nombres de las clases no deberían darnos información sobre cómo un elemento luce, sino que debería describir lo que el elemento representa:

``` html
<article class="alert">
  Estás en peligro!
</article>
```

El código HTML no tiene que darme ni una pista de cómo se ve una alerta.
Esa información está en el archivo CSS:

``` css
.alert {
  float: left;
  color: red;
  text-align: center
}
```

De esta forma, si un día queremos que la alerta se vea diferente, no hace falta modificar el código HTML.
Simplemente debemos cambiar el código CSS.

### No usemos clases de grid

Las clases de grid, como **container**, **row**, **col-** y **offset-**, muy comunes en Frameworks web como Bootstrap, tampoco cumplen la regla, porque describen cómo queremos que se distribuyan las partes de la página:

``` html
<main class="book-page">
  <div class="container">
    <div class="row">
      <div class="col-md-8">
        <article class="book-info">
        ...
        </article>
      </div>
      <div class="col-md-4">
        <div class="author-details">
        ...
        </div>
      </div>
    </div>
  </div>
</main>
```

En este ejemplo tenemos una página de un libro con información del libro y del autor.
El resto de las etiquetas son clases de grid, que nos dicen que la página se distribuye en dos columnas. Una de ancho 8, y otra de ancho 4.

Y no queremos eso. Este documento tiene demasiada información de como se tiene que ver.
Y como dijimos antes, el HTML tiene que abstraernos del estilo.

Tenemos que lograr mover esa responsabilidad al CSS. El HTML debería ser simple:

``` html
<main class="book-page">
  <article class="book-info">
    ...
  </article>

  <aside class="author-details">
    ...
  </aside>
</main>
```

Al igual que en la escritura, tenemos que reducir al HTML a sus componentes más limpios.

Hoy en día es muy sencillo describir cómo distribuir los elementos en columnas usando sólo CSS.
Podemos usar Float:

``` css
.book-page {
  display: block;
}

.book-info {
  width: 66.66%;
  float: left;
}

.author-details {
  width: 33.33%;
  float: left;
}
```

Podemos usar Flexbox:
``` css
.book-page {
  display: flex;
}

.book-info {
  flex: 2;
}

.author-details {
  flex: 1;
}
```

Podemos usar Grid CSS:

``` css
.book-page {
  display: grid;
  grid-template-columns: 2fr 1fr;
  grid-column-gap: 1rem;
}
```

Sea lo que sea que usemos, no hay razón para que toquemos el HTML.

### Usemos tags apropiados.

Una práctica común entre programadores es usar `<div>` para todo.

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
    <div class="post">
      <div>...</div>
      <div>...</div>
    </div>

    <div class="post">
      <div>...</div>
      <div>...</div>
      <div>...</div>
    </div>
  </div>

  <div class="site-footer">
    Creado por ...
  </div>
</body>
```

Es una práctica que quedó del pasado, cuando no había tantos tags para elegir.
Pero hoy en día HTML es muy expresivo, y tiene tags para todos los usos:

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
    <article class="post">
      <header>...</header>
      <section>...</section>
    </article>

    <article class="post">
      <header>...</header>
      <section>...</section>
      <aside>...</aside>
    </article>
  </main>

  <footer class="site-footer">
    Creado por ...
  </footer>
</body>
```

* Si el elemento es un encabezado, usá `<header>`.
* Si es un elemento de navegación usá `<nav>`.
* Si es el contenido principal de la página usá `<main>`
* Si es el pié de página usá `<footer>`.
* Si es un elemento que tiene sentido en si mismo usá `<article>`.
* Si el elemento representa una parte de un todo mayor usá `<section>`.
* Si es información extra o relacionada usá `<aside>`.
* A su vez un articulo o sección pueden también tener sus propios encabezados, pies, subsecciones, etc.

Usar los tags adecuados mejora mucho la legibilidad.
Es mucho más fácil visualizar donde empieza y termina cada elemento.

La única razón para usar `<div>` es para romper las reglas.
O sea, cuando necesiten agregar un elemento sin valor semántico para lograr cierto efecto.
Por ejemplo para usar una librería javascript:

``` html
<!-- This div tag is needed for the typehead-js library to work -->
<div class="typehead-container typehead-js">
  <input type="text" class="typehead-input" />
</div>
```
Cuando hagan cosas fuera de lo común, asegurense de agregar comentarios.


### Un ejemplo

Imaginemos que queremos implementar una barra de navegación con dos links.

![Barra de navegación](/img/charla-snappler/menu.png){:style="width: 100%"}

Lo que hace todo el mundo es ir a la página web de Bootstrap y copiar el código de ejemplo del navbar:

``` html
<nav class="navbar">
  <div class="container-fluid">
    <div class="collapse navbar-collapse">
      <ul class="nav navbar-nav">
        <li class="active">
          <a href="/">Home</a>
        </li>
        <li>
          <a href="/about">About</a>
        </li>
      </ul>
    </div>
  </div>
</nav>
```

Tenemos una barra de navegación que usa el tag **nav**. Hasta ahí todo perfecto.

Después tenemos un `container-fluid`, que como vimos no da ninguna información semántica. Podemos borrarlo.

Después tenemos una lista desordenada `ul` con clase `nav`.
¿Entonces, es un `nav` o es un `ul`?

Si navbar ya significa *barra de navegación*.
¿Por qué tenemos un `navbar-nav` adentro?
¿Qué significa?
¿Navegación dentro de la barra de navegación?
No tiene sentido.
También podemos borrarlo.

A todo esto, es perfectamente válido tener una serie consecutiva de links `a` uno detrás del otro. No necesitamos usar `ul` y `li` para eso.

El proposito original de `ul` y `li` no es listar elementos de HTML, sino crear listas con valor semántico, como listas de supermercado.

Lo único que necesitabamos era una barra de navegación con dos links:

``` html
<nav class="navbar">
  <a class="navbar-item active" href="/">Home</a>
  <a class="nabvar-item" href="/about">About</a>
</nav>
```

Esto es a lo que nos referimos cuando decimos que hay que **asegurarnos de que cada elemento haga trabajo útil**.

Los tags `ul` y `li` no estaban haciendo trabajo útil.

### Amiguémonos con el CSS

Muchos programadores piensan que escribir CSS es muy complicado.
Yo creo que eso es un miedo que nos quedó de hace muchos años atrás.
Antes era muy difícil hacer que un sitio web se viera bien en todos los navegadores.

En ese sentido, Bootstrap era una ayuda gigante.
Nos permitía armar sitios lindos sin preocuparnos tanto de problemas de compatibilidad.

Pero hoy en día la situación cambió.
Los navegadores son mucho mas compatibles entre sí.
Y CSS tiene muchas facilidades que antes no tenía.

Usar Bootstrap parece un atajo pero a la larga perjudica más que lo que ayuda.
Boostrap rompe las reglas constantemente, y nos dificulta escribir HTML semántico, lo que paradojicamente nos lleva a escribir más código CSS. Y es bastante lógico que pase esto: si tenemos más etiquetas, tenemos más clases para definir.

Otra cosa que pasa cuando reducimos el HTML y el CSS es que todo el Javascript que usamos para manipular el DOM también se simplifica. Y es bastante lógico que pase esto. Si hay menos etiquetas, necesitamos menos código para manipularlas.

Y todo esto no sólo se traduce en código más fácil de leer y mantener, sino que también en mayor rendimiento de nuestros sitios web.


## ¿Vale la pena esforzarnos tanto?

Martin Fowler (Un programador bastante conocido) intenta contestar esta pregunta en su conocido artículo titulado [¿Vale la pena hacer software de alta calidad?](https://martinfowler.com/articles/is-quality-worth-cost.html).

Fowler diferencia calidad interna y externa.

- La calidad interna es la que es sólo visible para los programadores. Ejemplos de calidad interna es la limpieza del código, que tan buena es la arquitectura general, si se usan buenos nombres o si se separa correctamente en módulos.
- La calidad externa es lo que puede ver el cliente. Por ejemplo la interfáz de usuario, o si hay defectos en el software.

Fowler hace esta separación porque a simple vista pareciera que los clientes no aprecian la calidad interna. No les importa realmente si un modulo está bien nombrado. Les importa que su software haga lo que tiene que hacer.

Según Fowler, baja calidad interna es resultado de la suciedad: cualquier cosa que sobra, que es redundante y se interpone en nuestro camino.

Según Martin Fowler, incluso los mejores equipos introducen pequeñas suciedades al código todo el tiempo. La suciedad en el código como la mala hierba, crece incontrolablemente y requiere esfuerzo eliminarla.

Según Fowler, si tenemos dos sistemas idénticos, uno con mucha suciedad y otro sin suciedad, agregar funcionalidades nuevas en el primero demora mucho mas tiempo que en el segundo.

La calidad interna hace más fácil mejorar el software.
Los programadores pasamos la mayor parte de nuestro tiempo modificando código.
Alta calidad interna hace que el código sea más fácil de leer, modificar y eliminar.
Lo que se traduce en que agregar funcionalidades sea más rápido y barato.

Y eso **SÍ** es muy importante para los clientes.

A medida que crece el software, nos toma cada vez más y más tiempo agregar nuevas funcionalidades.

Esto pasa con mucha mas fuerza cuando no le prestamos atención a la calidad interna del software.

Cuando le prestamos atención a la calidad del software desde el comienzo, podemos agregar nuevas funcionalidades mucho más rápido:

![Calidad](/img/charla-snappler/quality.png){:style="width: 100%"}

**Hacer mi propio grafico**


Al principio tardamos más. Pero según Martin Fowler, se paga en semanas, no en meses.

Los desarrolladores no hacemos un buen trabajo en explicar esta situación.
Decimos cosas como *"No nos dejan escribir codigo de calidad porque toma mucho tiempo"*, implicando que la calidad viene a un costo.

Pero no es así. El costo de escribir código de calidad es negativo.
Las horas que invierto hoy en simplificar el código, las recupero con creces en pocas semanas.

El código malo es malo para todos.

Hace las vidas de los programadores más difíciles, y a la larga les cuesta más dinero a los clientes.

Finalmente **es más barato hacer software de calidad**.

## Simplifiquemos nuestra arquitectura

Los programadores tenemos una tendencia a la sobre-ingeniería.
Queremos usar las herramientas que usan Google, Facebook y Netflix.

Simple <----------------------------------------> Complejo

Queremos usar **Serverless**, **soluciones distribuídas**, **microservicios**, **Kubernetes**, **React**, **Angular**, **AJAX**, **websockets**, **routing del lado del cliente**, **componentes web**, etc.

Todas arquitecturas y tecnologías que existen para resolver problemas complejos.

Pero la mayoría de los problemas web se pueden resolver con herramientas simples.

Los programadores somos muy buenos para entender el valor de todas nuestras herramientas, pero somos malos para entender su costo.

Todas estas tecnologías tienen un costo de implementación y de mantenimiento, y si no tenemos cuidado pueden hacernos las vidas muy difíciles más adelante.

Mi regla de oro para elegir una arquitectura o herramienta es que *se lo tiene que ganar*.
Estas herramientas no se usan por las dudas.
Se usan a propósito habiendo ponderado los beneficios y los costos.

### Simplificar desde el comienzo

> My point today is that, if we wish to count lines of code, we should not regard them as “lines produced” but as “lines spent”: the current conventional wisdom is so foolish as to book that count on the wrong side of the ledger.
> - Edsger W. Dijkstra

Edsger W. Dijkstra decía que no hay que contar las lineas de código como *lineas producidas*, sino como *lineas gastadas*.

La mejor forma de simplificar el código es no escribiéndolo en primer lugar.

Les voy a dar un ejemplo: Mi pagina web personal es un sitio web estático.
Consiste en HTML y CSS. No tiene ni una linea de javascript.

Podría haberlo resuelto usando Ruby on Rails, Postgres, Heroku, React y Bootstrap.
Pero elegí hacerlo con un sitio web estático.

- Como no tiene base de datos, no tengo que preocuparme por ataques de injeccion SQL, ni por diseñar la arquitectura de las tablas, ni de agregar índices, ni de mantenerla actualizada.
- Como uso git, tengo el historial de todos los cambios en mis publicaciones a mi disposición.
- Como no uso Rails, no necesito preocuparme por mantenimiento de la aplicación, ni de vulnerabilidades en las librerías, ni de bugs.
- Como no uso React ni AJAX ni routing del lado del cliente, ni javascript, no tengo que preocuparme por bugs del lado del cliente.

Este sitio no necesita mantenimiento.
Lo actualizo más o menos una o dos veces al año para agregar alguna publicación.

Si tengo que comparar la solución de Rails con esta solución, considero que esta solución es una solución superior. No a pesar de ser simple, sino como consecuencia de ser simple.

Casi siempre, la solución más simple es también la mejor solución.

Tomarnos el tiempo para simplificar la arquitectura es especialmente beneficioso en etapas tempranas de desarrollo.

Dedicar una o dos semanas a simplificar la arquitectura parece un sacrificio muy grande. Pero si tenemos en cuenta que el software va a tener que ser mantenido durante varios años, una o dos semanas ya no parece tanto tiempo.

Mientras antes empezamos a simplificar, más tiempo nos ahorramos a largo plazo.
Nosotros vamos a ser más felices y nuestros clientes también van a ser más felices.

## Nuestros límites.

Hay personas que estudian los limites teóricos de la computación. Por ejemplo que problemas son computables y cuales no.

Un profesor de físicas del MIT quería calcular [los limites *físicos* de la computación](https://cds.cern.ch/record/396654/files/9908043.pdf). Esto es, hasta donde podemos llegar con los conocimientos que tenemos sobre el universo.

Las computadoras son sistemas físicos: lo que pueden hacer y lo que no, está dictado por las leyes de la física. La velocidad a la que puede procesar información está limitada por su energía.

Este profesor quería decifrar a qué velocidad podía ir la última notebook que construyamos. Calculó cuanta energía podía meterse en una notebook de 1 kg de peso.

Tuvo en cuenta la velocidad de la luz, la gravedad, las leyes de la termodinámica, las leyes cuánticas, y llegó a la conclusión de que el límite físico de "la última notebook" sería de 10^50 operaciones por segundo. Que es un montón y no estamos ni cerca.

Pero no es lo mismo límite físico que límite práctico. Para llegar a esa velocidad es necesario comprimir la computadora a un tamaño minúsculo, formando un agujero negro. Para usar esta computadora tendríamos que estar adentro del agujero negro, donde moriríamos al instante.

Yo no se ustedes, pero yo prefiero seguir vivo aunque mi computadora sea más lenta.

Nosotros los seres humanos también somos sistemas físicos.
Lo que podemos y no podemos hacer también está dictado por las leyes de la física.

Nuestros cerebros también tienen límites.
Hay una cantidad de información máxima que podemos procesar en un momento dado.

Esto es una razón más para simplificar.
Mientras más simple sea un sistema, más fácil va a ser para nuestros cerebros entenderlo, modificarlo y mantenerlo.

Pero el código es solamente el producto final.
La mayor parte del trabajo pasa en nuestras cabezas.

Si no cuidamos a nuestras cabezas por un tiempo prolongado podemos terminar con burn out.
Cuando sufrimos burn out no podemos razonar correctamente.
Nos transformamos en una peor versión de nosotros mismos.
Lo que afecta nuestras vida y las de los que nos rodean.
Lo que nos causa frustración y resentimiento.

Es un circulo vicioso que puede hacer que terminemos muy mal.

No se quemen la cabeza.

Si no pueden resolver un problema, no trabajen 10 horas por día.
Hagan una pausa. Salgan a caminar. Tomense una siesta.
Denle tiempo al cerebro a procesar la información.
Cierren la computadora cuando termina la jornada.
El trabajo va a seguir esperandolos al día siguiente.

Cuiden sus cabezas.

Trabajar adentro de un agujero negro no vale la pena.


### Resolver problemas complejos

¿Les ha pasado que tienen un problema que no pueden resolver, y no hay con que darle.
Y pasan horas y horas intentando. Y se frustan.
Y de repente al día siguiente lo resuelven en 15 minutos?

No significa que perdieron el tiempo el día anterior.
Todo ese tiempo de esfuerzo y frustración fue necesario para resolver el problema.
Su cerebro necesitaba tiempo para procesar toda esa información.

No existe el 10X programador, o el "programador que programa tan eficientemente como 10 programadores".
Es un mito que le hace mucho daño a la profesión.

No tenés que ser un genio para resolver problemas complejos.
**Los problemas complejos los resolvemos las personas comunes presentandonos a trabajar cada día**.

Todas las personas podemos ser programadoras.
Simplemente hay que presentarse a trabajar cada día, enfrentarnos a los problemas, pensar y descanzar bien.

Si hacen eso, les aseguro que no hay problema que no puedan resolver.
