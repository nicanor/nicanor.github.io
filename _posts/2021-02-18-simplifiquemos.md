---
layout: post
title:  "Simplifiquemos"
category: articles
tags: programming talk español
location: La Plata
visible: true
---

<style>
@media print {

}
</style>

El Viernes 19 de Febrero de 2021 dí una charla virtual para el **Summer Training** de Snappler.
Link a las diapositivas [...]

A continuación la transcripción de la charla.

---------------------

## Introducción

Hola a todos.
Mi nombre es Nicanor Perera.
Soy programador Web.

Trabajé en Snappler durante 3 años.
Que fue una experiencia muy linda de mi vida.

Hoy en día trabajo en Brandkit.io, una empresa de Manejo digital de Assets.

Estoy acá porque Damián me pidió que de una charla para el **Summer Training**.

Le pregunté de qué. Me dijo "De lo que quieras".
Le pregunté cuanto tenía que durar. Me dijo "Lo que quieras".
Le pregunté un par de cositas más, arreglamos para hoy, y acá estoy.

Así que bueno, les voy a hablar de lo que yo quiera.

La charla va a durar 30 minutos, y después de la charla pueden hacerme preguntas y podemos charlar de lo que ustedes quieran.

## Como escribir bien

El primer libro en el que pienso cuando me piden una recomendación es **On writting well**, de William Zinsser.

William Zinsser fue un periodista y escritor Estadounidense, que se dedicó mucho al tema de la escritura.

Ese libro, **On writing well** es un libro que leo todos los años. Está en Inglés, pero los consejos que dá aplican también al Español.

Uno de los consejos más importantes es usar palabras simples:

- No digas *denominación* si podés decir *nombre*.
- No digas *sufragio* si podés decir *voto*.
- No digas *con la finalidad de* si podés decir *para*.
- No digas que *estás anticipando experimentar una precipitación considerable* cuando podés decir que *puede llover*.
- No escribas complicado para parecer importante.

Pero también usá palabras precisas:
No digas que el presidente se fue de la empresa. Renunció? Se retiro? Lo echaron?

Hablá en vos activa. Reducí la cantidad de adjetivos y adverbios. Eliminá la suciedad en tus oraciones. Escribí claro.

El decía que escribir es trabajo dificil.
Que una sentencia clara no es un accidente.
Muy pocas sentencias salen bien la primera vez, la segunda o incluso la tercera vez.

Según él, **el secreto de la buena escritura es reducir cada oración a sus componentes más limpios**, y para lograr eso hay que asegurarse que **cada palabra que esribís esté haciendo trabajo útil**.

En el libro él da como ejemplo un texto que ya había reescrito 4 o 5 veces.
Y todavía tenía más correcciones para hacerle.

![Correcciones de Zinsser](/img/charla-snappler/zinsser.png){:style="width: 100%"}

Según Zinsser, la mayoría de los borradores pueden ser cortados en un 50 porciento sin perder nada de información y sin perder la voz del escritor.

Para escribir una nota periodística, él escribía un título, luego el primer párrafo, el segundo, el tercero. Y recién el tercero le gustaba. Entonces borraba los dos primeros, cambiaba el nombre del titulo y escribía un par de parrafos más. Se daba cuenta que quedaban mejor si les cambiaba de orden. Corregía y lo reducía a la mitad. Separaba algunos parrafos en dos, o unía dos parrafos en uno. Se iba a dormir.

Al día siguiente con la cabeza descansada volvía a leerlo. Se preguntaba: "Estoy escribiendo lo que quiero decir?". Volvía a repetir el proceso una y otra vez, hasta que terminaba con el texto tal y como lo quería. Escribir una nota le podía tomar varios días

**Según Zinsser, la esencia de escribir es reescribir**.

La facultad de Ciencias Económicas de la Universidad de Córdoba tiene un buen ejemplo de reescritura. Tomaron el primero borrador de un texto y le aplicaron varias correcciones:

![Correcciones de FCE - UNC](/img/charla-snappler/correcciones.png){:style="width: 100%"}

El primer texto tiene muchas construcciones complicadas. El sujeto lo encuentran recién a la mitad del texto, y la parte más importante está por el final. Es difícil de leer.

Cuando tienen que leer algo varias veces para entenderlo, es porque está escrito de forma complicada. Estas personas se preguntaron: ¿Qué es lo que estoy queriendo decir? y terminaron con un texto mucho más fácil de procesar.

Y yo creo que a este texto todavía se le pueden seguir aplicando correcciones.

El secreto de la buena escritura es reducir cada oración a sus componentes más limpios

Borges era un obsesivo de la corrección.
Tanto que decía que la razón por la que publicaba, era para dejar de corregir.

La mayoría de las personas que consideramos genios de la literatura no son genios.
Son personas comunes que lograron dominar su escritura a través de trabajo duro.

La buena escritura es el resultado de trabajo iterativo.

Y por qué les hablo de esto?

Porque parte de nuestro trabajo es escribir. Escribimos emails. Escribimos tareas. Escribimos documentación.

Porque considero que muchas de estas reglas aplican perfectamente al software. Y eso es de lo que trata mi charla de hoy.

Voy a hablarles de como escribir HTML bien.

## On writting HTML well

Por qué? porque noto que mucha gente no le presta atención.
Hay personas que lo desestiman diciendo que escribir HTML no es programar.
Es una lástima porque si le prestaran más atención serían más felices.

La regla más importante para escribir bien HTML es separar estructura de estilo.

* El código HTML tiene que describir la estructura de nuestro sitio web.
* El código CSS tiene que describir cómo se ve nuestro sitio web.


Por ejemplo, miremos este código:
``` html
<article class="color-red pull-left text-center">
  Estás en peligro!
</article>
```

Tenemos un artículo con texto *"Estás en peligro!"*. Y clases *color-red*. *pull-left* y *text-center*.
Este código rompe la regla. Los nombres de las clases no describen qué es el elemento.
Describen cómo tiene que verse.

No hay tanta diferencia entre eso y poner los estilos en linea:

``` html
<article style="color: red; float: left; text-align: center;">
  Estás en peligro!
</article>
```

En ambos casos, cuanto leo el código HTML recibo pistas de cómo tiene que verse.
Y eso es lo que queremos evitar.

Si tengo que elegir entre esos dos prefiero los estilos en linea, porque por lo menos es explícito que está modificando los estilos.

Y además no necesito definir las clases *color-red*. *pull-left* y *text-center*:

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

Los nombres de las clases no deberían darnos información sobre cómo un elemento luce.

Lo que deberíamos hacer es intentar que el nombre de la clase describa lo que el elemento representa:

``` html
<article class="alert">
  Estás en peligro!
</article>
```

El código HTML no tiene que darme ni una pista de cómo se vé el elemento.

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

Las clases de grid, como `container`, `row`, `col-*`, `offset-*` tampoco cumplen la regla.

Estas clases describen cómo queremos que se distribuyan las partes de la página:

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

Y no queremos eso. Este documento tiene demasiada información de estilo.
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

Y el CSS debería ocuparse de describir cómo distribuiremos las distintas partes en la página.

Hoy en día es muy sencillo describir cómo distribuir los elementos en columnas usando sólo CSS. Podemos usar float, flexbox, o Grid CSS.


``` css
/* Solución con float */
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

``` css
/* Solución con Flexbox */
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

``` css
/* Solución con Grid CSS */
.book-page {
  display: grid;
  grid-template-columns: 2fr 1fr;
  grid-column-gap: 1rem;
}
```

Sea lo que sea que usemos, no hay razón para que toquemos el HTML.


### Usemos tags apropiados.

Una práctica común entre programadores es usar `div` para todo.

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

Pero hoy en día HTML es muy expresivo, y tiene tags para todos los usos.

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

Si el elemento es un encabezado, usá `header`.
Si es un elemento de navegación usá `nav`.
Si es el contenido principal de la página usá `main`
Si es el pié de página usá `footer`.
Si es un elemento que tiene sentido en si mismo usá `article`.
Si el elemento representa una parte de un todo mayor usá `section`.
Si es información extra o relacionada usá `aside`.
A su vez un articulo o sección pueden también tener sus propios encabezados, pies, subsecciones, etc.

Usar los tags adecuados mejora mucho la legibilidad.
Es mucho más fácil visualizar donde empieza y termina cada elemento.

La única razón para usar `div` es para romper las reglas.
O sea, cuando necesiten agregar un elemento sin valor semántico para lograr cierto efecto.
Por ejemplo para usar una librería javascript.
Cuando hagan cosas fuera de lo común, asegurense de agregar comentarios.

``` html
<!-- This div tag is needed for the typehead-js library to work -->
<div class="typehead-container typehead-js">
  <input type="text" class="typehead-input" />
</div>
```

### Simplifiquemos al máximo

Tenemos que reducir el código HTML a sus componentes más limpios.

Por ejemplo, imaginemos que queremos implementar una barra de navegación con dos links.

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

Son demasiados tags para algo tan simple.

Como ya vimos `container-fluid` no da ninguna información semántica. Podemos eliminarlo

Tenemos una lista desordenada (`ul`) con clase `nav`. Entonces, es un `nav` o es un `ul`?

Si navbar ya significa *barra de navegación*. Por qué tenemos un `navbar-nav` adentro?
Qué significa? Navegación dentro de la barra de navegación?
No tiene sentido.

A todo esto, es perfectamente válido tener una serie consecutiva de links `a` uno detrás del otro.

No necesitamos usar `ul` y `li` para eso.

El proposito original de `ul` y `li` no es listar elementos de HTML.

Es crear listas con valor semántico, como listas de supermercado.

A lo mejor lo único que necesitabamos era una barra de navegación con dos links:

``` html
<nav class="navbar">
  <a class="navbar-item active" href="/">Home</a>
  <a class="nabvar-item" href="/about">About</a>
</nav>
```

Tenemos que **asegurarnos de que cada elemento haga trabajo útil**.

Los tags `ul` y `li` no estaban haciendo trabajo útil.

### Amiguémonos con el CSS

Muchos programadores piensan que escribir CSS es muy complicado.
Yo creo que eso es un miedo que nos quedó de hace muchos años atrás.
Antes era muy difícil hacer que un sitio web se viera bien en todos los navegadores.

En ese sentido, Bootstrap era una ayuda gigante.
Nos permitía armar sitios lindos preocupandonos menos de problemas de compatibilidad.

Pero hoy en día la situación cambió mucho.
Los navegadores son mucho mas compatibles entre sí que antes.
Y CSS tiene muchas facilidades que antes no tenía.

Usar Bootstrap parece un atajo. Pero mi experiencia me ha demostrado que a la larga perjudica mucho más que lo que ayuda.
Boostrap rompe las reglas constantemente, y nos dificulta escribir HTML semántico, lo que nos lleva a escribir más código.

Si escribimos HTML semántico, el código CSS que necesitamos también se reduce un montón.
Y es bastante lógico que pase esto: si tenemos menos etiquetas, tenemos menos clases para definir.

Un libro que recomiendo mucho por si quieren profundizar sobre este tema es **Maintainable CSS** de Adam Silver.
Lo pueden encontrar online y se lee en 20 minutos.

Otra cosa que pasa cuando reducimos el HTML y el CSS es que todo el Javascript que usamos para manipular el DOM también se simplifica.
Y es bastante lógico que pase esto. Si hay menos tags, necesitamos menos código para manipularlo.

Y todo esto se traduce en mayor rendimiento. Tenemos menos HTML, menos CSS y menos Javascript.
Terminamos con código mucho más fácil de leer. Y mucho más fácil de mantener.

## ¿Vale la pena esforzarnos tanto?

Arranco con una pregunta de Martin Fowler (Un programador bastante conocido)
**¿Vale la pena hacer software de alta calidad?**

https://martinfowler.com/articles/is-quality-worth-cost.html


Fowler diferencia calidad interna y externa.

* La calidad externa es lo que puede ver el cliente. Por ejemplo la interfáz de usuario, o si hay defectos en el software.

* La calidad interna es la que es sólo visible para los programadores. Ejemplos de calidad interna es la limpieza del código, que tan buena es la arquitectura general, si se usan buenos nombres o si se separa correctamente en módulos.

A simple vista pareciera que los clientes no aprecian la calidad interna.

"Cruft" o suciedad es un término que se usa en el mundo del software para referirnos a cualquier cosa que sobra, que es redundante y se interpone en nuestro camino.

Según Martin Fowler, incluso los mejores equipos introducen pequeñas suciedades al código todo el tiempo.

La suciedad en el código como la mala hierba, crece mucho y requiere esfuerzo eliminarla.

[Imagen de cruft]

Si tenemos dos sistemas identicos, uno con mucha suciedad y otro sin suciedad, agregar funcionalidades nuevas en el primero demora mucho mas tiempo que en el segundo.

La calidad interna hace más fácil mejorar el software.
Los programadores pasamos la mayor parte de nuestro tiempo modificando código.
Alta calidad interna hace que el código sea más fácil de leer, modificar y eliminar.

Lo que se traduce en que agregar funcionales sea más rápido y barato.
Y eso es muy importante para los clientes.

Si graficamos en el eje vertical las nuevas funcionalidades y en el eje horizontal el tiempo, tenemos:

![Funcionalidades - Tiempo](/img/charla-snappler/features.png){:style="width: 100%"}

A medida que crece el software, nos toma cada vez más y más tiempo agregar nuevas funcionalidades.

Esto pasa con mucha mas fuerza cuando no le prestamos atención a la calidad interna del software.

Cuando le prestamos atención a la calidad del software desde el comienzo, podemos agregar nuevas funcionalidades mucho más rápido:

![Calidad](/img/charla-snappler/quality.png){:style="width: 100%"}

Al principio tardamos más. Pero según Martin Fowler, se paga en semanas, no en meses:

Los desarrolladores no hacemos un buen trabajo en explicar esta situación.
Decimos cosas como *"No nos dejan escribir codigo de calidad porque toma mucho tiempo"*, implicando que la calidad viene a un costo.

Pero no es así. El costo de escribir código de calidad es negativo.
Las horas que invierto hoy en simplificar el código, las recupero con creces en pocas semanas.

El código malo es malo para todos.

Hace las vidas de los programadores más difíciles, y a la larga les cuesta más dinero a los clientes.

Finalmente **es más barato hacer software de calidad**.

## Simplifiquemos

> My point today is that, if we wish to count lines of code, we should not regard them as “lines produced” but as “lines spent”: the current conventional wisdom is so foolish as to book that count on the wrong side of the ledger.
> - Edsger W. Dijkstra:

Edsger W. Dijkstra decía que no hay que contar las lineas de código como *lineas producidas*, sino como *lineas gastadas*.

Y yo no podría estar más de acuerdo. Tenemos que hacer el esfuerzo de simplificar el código.

Y quizás más importante: simplificar la arquitectura.

Simple <------------------------------------------------------------------------> Complejo

Los programadores tenemos una tendencia a la sobre-ingeniería.

Queremos usar las cosas que usan Google, Facebook y Netflix.
Queremos usar `Serverless`, `soluciones distribuídas`, `microservicios`, `React`, `Angular`, `AJAX`, `websockets`, `routing del lado del cliente`, `componentes web`, etc.
Todas arquitecturas y tecnologías que existen para resolver problemas complejos.

Pero la mayoría de los problemas web se pueden resolver con herramientas simples.

Los programadores somos muy buenos para entender el valor de todas nuestras herramientas, pero somos malos para entender su costo.

Todas estas tecnologías tienen un costo de implementación y de mantenimiento, y si no tenemos cuidado pueden hacernos las vidas muy difíciles más adelante.

Mi regla de oro para elegir una arquitectura o herramienta es que *se lo tiene que ganar*.
Estas herramientas no se usan por las dudas. Se usan a propósito habiendo ponderado los beneficios y los costos.

Mi pagina web personal es un sitio web estático.
Consiste en HTML, CSS y quizás una linea o dos de javascript.

Podría haberlo resuelto usando Ruby on Rails, Postgres, Heroku, React y Bootstrap.

Pero considero que mi solución es una solución superior.

No tiene base de datos, así que no tengo que preocuparme por ataques de injeccion SQL, ni por diseñar la arquitectura de las tablas, ni de agregar índices, ni de actualizarla.

No uso Rails, así que no necesito preocuparme por mantenimiento de la aplicación, ni de vulnerabilidades en las librerías, ni de bugs.

No uso React ni AJAX ni routing del lado del cliente, ni javascript. Así que no tengo que preocuparme por bugs del lado del cliente.

La actualizo mas o menos 1 o 2 veces al año.

Lo subo a `github-pages` usando `git`.
Lo que encima me da la ventaja que tengo el historial de todos los cambios a mi disposición.

Mi consejo es que se tomen su tiempo para simplificar la arquitectura.

Esto es especialmente beneficioso en etapas tempranas de desarrollo.

Mientras antes empiecen a simplificar, más tiempo se van a ahorrar a largo plazo.

Ustedes van a ser mas felices y sus clientes también van a ser más felices.


## Nuestros límites.

Hay personas que estudian los limites teóricos de la computación. Por ejemplo que problemas son computables y cuales no.

Un profesor de físicas del MIT quería calcular los limites *físicos* de la computación.

Las computadoras son sistemas físicos: lo que pueden hacer y lo que no, está dictado por las leyes de la física. La velocidad a la que puede procesar información está limitada por su energía.

Este profesor calculó cuanta energía podía meterse en una notebook de 1 kg de peso. Tuvo en cuenta la velocidad de la luz, la gravedad, las leyes de la termodinámica, las leyes cuánticas, y llegó a la conclusión de que el límite físico de "la ultima notebook" sería de 10^50 operaciones por segundo. Que es un montón y no estamos ni cerca.

Como anécdota, los mejores resultados los obtuvo comprimiendo la computadora a 10^-27 metros, formando un agujero negro. La mala noticia es que para usarla seguramente tengamos que estar adentro del agujero negro, donde moririamos espaguetificados en un instante.

Nosotros los seres humanos también somos sistemas físicos.
Lo que podemos y no podemos hacer también está dictado por las leyes de la física.

Nuestros cerebros son limitados.
Cuanto antes lo aceptemos, mejor nos va a ir.

El hecho de que nuestros cerebros son limitados es una razón más para simplificar.
Mientras más simple sea un sistema, más fácil va a ser para nuestros cerebros entenderlo, modificarlo y mantenerlo.

Nuestros cerebros tienen una cantidad de información máxima que pueden procesar en un momento dado.

No se quemen la cabeza.

Si se sienten cansados o agobiados hagan una pausa. Salgan a caminar. Tomense una siesta.
Denle tiempo al cerebro a procesar la información.

No trabajen 10 horas por día. Cuando termina la jornada cierren la computadora.

El trabajo va a seguir esperandolos al día siguiente.

Cuiden su cerebro, que es su herramienta de trabajo.

El código es solamente el producto final.
Pero el 90% del trabajo pasa en la cabeza.
Y una mente que no está descansada no puede razonar bien.

Una mente no descansada tiende mucho más a la procrastinación.
Cuando uno procrastina siente que no trabajó suficiente.

Y eso hace que nos dé ansiedad.

Nuestra carrera está inundada de personas que sufren síndrome del impostor.

Que piensan que no logran hacer suficiente.
Que sienten que no saben, o que no pueden.

Si no cuidan su cabeza durante un tiempo prolongado pueden terminar con BurnOut (*"Con el bocho quemado"*).

Creanme que no está bueno. Cuando uno sufre Burn Out no puede razonar correctamente.
Y se transforma en una peor versión de sí mismo.
Lo que afecta a la vida de uno y también a la vida de las personas que queremos.
Y nos hace trabajar peor, y nos causa frustración.
Y se retroalimenta.

Cuiden sus cabezas.

¿Les ha pasado que tienen un problema que no pueden resolver, y no hay con que darle.
Y pasan horas y horas intentando. Y se frustan.
Y de repente al día siguiente lo resuelven en 15 minutos?

No significa que perdieron el tiempo el día anterior.
Todo ese tiempo de esfuerzo y frustración fue necesario para resolver el problema.
Su cerebro necesitaba procesar toda esa información.

No existe el 10X programador, o el "programador que programa tan eficientemente como 10 programadores". Es un mito que le hace mucho daño a la profesión.

No tenés que ser un genio para resolver problemas complejos.

**Los problemas complejos lo resolvemos las personas comunes presentandonos a trabajar cada día**.

Les aseguro que todas las personas pueden ser programadoras.

Simplemente hay que presentarse a trabajar cada día, enfrentarnos a los problemas y pensar.

Si van a trabajar cada día, les aseguro que no hay problema que no puedan resolver.
