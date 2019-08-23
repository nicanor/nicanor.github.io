---
layout: post
title:  "Programación y simplicidad"
category: articles
tags: programming español elixir
location: La Plata, Argentina
visible: false
---
Estaba cursando mi cuarto año de la carrera de Licenciatura en Informática, y debía elegir una materia optativa.
Mis opciones eran Programación *Lógica*, *Distribuída* y *Funcional*. No sabía muy bien que significaba cada una, y lamenté no poder anotarme a las tres.

Un compañero me mencionó que Funcional le había hecho *explotar el cerebro*, y no pude resistirme a la tentación. Dicho y hecho, mi cerebro casi estalla en la primera clase, cuando me entero que era el único anotado a la materia.

Era la primera vez que contaba con un profesor y un <abbr title="Jefe de Trabajos Prácticos">JTP</abbr> para mí sólo, lo que me preocupaba, porque iba a comenzar la primer clase, y tenía miedo de quedarme dormido frente al profesor. ¿Por qué tuve que salir la noche anterior? Poco me imaginaba que la materia sería tan interesante que me olvidaría del sueño que tenía.

Fidel, el profesor, comenzó la clase con una pregunta: ¿Son equivalentes la expresión `f(3) + f(3)` y la expresión `2*f(3)`? - Sí, contesté rápidamente. - ¿Siempre? - retrucó. En matemática son equivalentes, y eso significa que podemos reemplazar una expresión por la otra. ¿Pero y en los lenguajes de programación? Tomemos este ejemplo en Javascript:

``` javascript
let x = 0;

function f(y) {
  x = x + 1;
  return x + y;
}

console.log(f(3) + f(3));
```

Era evidente que no lo eran.

La materia iba a ser en Haskell. Pero Fidel aclaró: El lenguaje es mi medio de enseñanza, no el fin de la materia.  No quiero enseñarte un lenguaje de programación. Quiero enseñarte TODOS los lenguajes de programación. Ninguno. Todos. Lo que nos importa son los elementos conceptuales. Conceptos transversales. Generalizables.

Esencia de las ideas.

Valorar el pensamiento abstracto por sobre el concreto.

Aspecto operacional
Aspecto denotacional

La mayoria de los cursos te enseñan lo concreto, y asumen que a la larga vas a aprender lo abstracto.

Los programas sos descripciones ejecutables de soluciones a problemas computacionales
Un programa es texto que cuenta una idea.


1. Explicar cómo eran las clases con Fidel y qué conceptos hablaba.
2. Mencionar alguna que otra idea de forma muy general
3. Lamentar que esta materia no sea parte de la curricula general
4. Contar sobre mi experiencia, y dónde estoy ahora.


<!-- Parte 2 -->

1) Valores, y propiedades. Comparar con objetos. Ver como seguir luego.


Me presentó la programación funcional como una forma de más alto nivel aún que la programación orientada a objetos. Programación funcional parecía muy diferente a todo lo que había programado antes.

Los valores son entidades (matemáticas) abstractas con ciertas
propiedades, por ejemplo `1.5`, `true`, `'C'`, `false`, `42`.


> “El valor de una expresión depende sólo de los elementos que la constituyen.”.



 *el principio de identidad*: todo valor es idéntico a sí mismo.
Si tengo una lista `A = [1,2,3]` y una lista `B = [1,2,3]`, podemos decir que `A` y `B` son **la misma** lista.

Este principio que parece obvio de entrada, no se cumplía en los lenguajes a los que estaba acostumbrado.
En *Ruby* por ejemplo, cada objeto tiene su propio `object_id`.
Incluso si una lista tiene los mismos elementos que otra, no podemos decir que sean la misma lista.

``` ruby
[1,2,3].equal?([1,2,3])
#=> false
```

Es necesario inspeccionarlo para encontrar todos sus atributos ocultos.
Sus métodos, que pueden estar definidos muy arriba en el árbol de herencias.
En programación funcional, en cambio, los datos son evidentes: un 1 es un 1 es un 1.
Y nada más. No hay métodos. Simples. Identificables. Se definen a sí mismos.

Los valores son inmutables y son evidentes: Podemos entender su significado con sólo mirarlos.

Los valores pueden ser compartidos. Los valores dan resultados predecibles. Si llamamos una función varias veces con los mismos valores como parámetros, tenemos los mismos resultados. Los resultados reproducibles son importantes: nos permiten escribir tests. Son fáciles de fabricar.

Son independientes del lenguaje. Son genéricos. Las nociones de estos valores son genéricas.
Los valores aggregate to values.
Una lista de valores inmutables es también un valor inmutable.
Las colecciones son inmutables.

``` ruby
a.object_id
#=> 70354765187380
a = [1,2,3]
#=> [1, 2, 3]
a.object_id
#=> 70354761000580
a.pop
#=> 3
a
#[1, 2]
a.object_id
#=> 70354761000580
```

``` ruby
a = b = [1,2,3]
#=> [1, 2, 3]
a.pop
#=> 3
b
#=> [1, 2]
```

Son fáciles de transmitir. Cuando te mando un valor se exactamente lo que te estoy mandando.
Cuando te mando una referencia a un objeto, no puedo estar seguro que lo que leas sea el mismo objeto que pretendía enviar.

Un dato puede ser un entero, un flotante, un caracter, un booleano. Y también puede ser una estructura de datos, que contenga
Los datos son ...

El siguiente concepto interesante que aprendí fue **función**.
Una función matemática es una relación que se establece entre dos conjuntos, a través de la cual a cada elemento del primer conjunto se le asigna un único elemento del segundo conjunto o ninguno. Al conjunto inicial o conjunto de partida también se lo llama dominio; al conjunto final o conjunto de llegada, en tanto, se lo puede denominar codominio.

Lo segundo que aprendí fue sobre inmutabilidad. No hay variables en el concepto clásico.
Hay constantes.
La funcion X no modifica la lista original, sino que retorna una nueva lista.

Una funcion es simplement un mapeo entre un conjunto de valores y otro conjunto de valores. Un hash-diccionario-mapa puede verse como la forma más simple de declarar una función. En clojure por ejemplo, se puede llamar las claves de un hash como si fueran parametros de una funcion.

Transformaciones
Datos simples
Estado
Comportamiento y Datos van separados.
Recursion y High ordered functions.
