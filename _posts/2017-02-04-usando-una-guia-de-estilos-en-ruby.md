---
layout: post
title:  "Usando una guía de estilos en Ruby"
category: articles
tags: programming talk español
location: La Plata, Argentina
visible: true
---

> El código limpio siempre se ve como si hubiera sido escrito por alguien al que le importaba

Como programadores, debemos entender al código como una forma de comunicación con otros desarrolladores. El código está destinado a ser mantenido por otra persona, no sólo por compañeros de desarrollo en el presente sino también por miembros del equipo en el futuro.

El código suele ser más fácil de escribir que de leer. Incluso el código escrito por uno mismo suele ser más dificil de leer luego de que no se lo mira por un tiempo, y muchas veces es más difícil reusar software de otra persona que escribirlo uno mismo, por el hecho de no entender cómo funciona.

Escribir código en los lenguajes de programación tradicionales consiste en decirle a la computadora qué hacer. Pero los modernos y expresivos lenguajes de programación nos permiten escribir código dirigido a personas, es decir, código que exprese a otros seres humanos cómo queremos que la computadora se comporte.

> Hoy en día es importante que el código comunique su propósito, ya que desarrollar está más relacionado con trabajar en equipo que lo que solemos considerar.

A la hora de trabajar en un equipo de desarrollo, es importante seguir una **guía de estilos**. Una guía de estilos es acerca de **consistencia**, y ser consistentes nos impulsa a escribir código prolijo y fácil de mantener y compartir, al mismo tiempo que mejora la comunicación con nuestros compañeros y nos permite enfocarnos en lo importante.


### Una guía de estilos define entre otras cosas:

* Cómo y dónde usar comentarios
* Cómo identar el código
* Uso apropiado de espacios en blanco
* Nombramiento apropiado de variables y funciones
* Cómo agrupar y organizar el código
* Buenos patrones e idiomas para usar
* Patrones a evitar


Una guía de estilos popular entre desarrolladores de Ruby es la [guía de estilos de Ruby de bbatsov](https://github.com/bbatsov/ruby-style-guide).

### Algunos consejos que nos da esta guía son:

* Identar con 2 espacios  
* Limitar lineas a 80 caractéres
* Evitar métodos mayores que 10 LOC (<5 en lo posible)
* Evitar exceso de espacios al final
* Terminar cada archivo con una línea nueva
* Usar **snake_case** para variables, métodos y símbolos
* Usar **CamelCase** para clases y módulos
* Usar **SCREAMING_SNAKE_CASE** para constantes
* Finalizar con `?` aquellos métodos que retornen un valor lógico. Ej: `[].empty?`
* Escribir código en forma funcional, evitando mutación cuando eso tenga sentido.
* Evitar más de tres niveles de anidación de bloques
* Ser consistente
* Usar el sentido común


## Ruby tips

### ¿qué hace? vs ¿qué es?

Muchos programadores estamos acostumbrados a pensar a los métodos como una serie de pasos a ejecutar que finalmente retornan un resultado. Pero ruby es un lenguaje muy expresivo. Salvo que explicitamente queramos expresar que un método realiza una computación, es una buena idea que nombremos a los métodos no pensando _¿qué hace?_, sino _¿qué es?_. Ejemplo:


``` ruby
# En lugar de:
def calculate_word_count
  return word.size
end

# Usar:
def word_count
  word.size
end
```



### Funciones de alto orden

Ruby cuenta con funciones de alto orden para colecciones, como `select`, `map`, `inject`, `any?`, `all?`, entre otras. Es importante conocer estas funciones para escribir código más corto y expresivo.

Es muy común ver a programadores escribir estructuras de código como las siguientes:

``` ruby
def keep_evens
  result_array = []
  for num in my_array
    result_array << num if num.even?
  end
  return result_array
end


def calculate_passengers_number(rooms)
  total = 0
  rooms.each do |room|
    total += room[:adults_number].to_i +
      room[:children_ages].size
  end
  total
end

```

Es decir, inicializar una variable con algún valor, realizar una computación para todos los elementos de una computación, y en cada iteración modificar la variable original, y finalmente retornar como resultado dicha variable.

Esa forma de escribir código suele ser señal de que el código puede ser refactorizado. Por ejemplo, estas mismas estructuras pueden escribirse de una forma más simple, segura y expresiva de la siguiente manera:


``` ruby
def even_members
  my_array.select {|item| item.even?}
end

# Aclaración: +sum+ es un método de Rails
def passengers_number(rooms)
  rooms.sum do |room|
    room[:adults_number].to_i +
    room[:children_ages].size
  end
end
```



### Usar notación **&**

``` ruby
# En lugar de:
['gato', 'perro', 'loro'].map { |x| x.upcase }
# Usar:
['gato', 'perro', 'loro'].map(&:upcase)
```

Explicación [aquí](http://blog.thoughtfolder.com/2008-02-25-a-detailed-explanation-of-ruby-s-symbol-to-proc.html).


### Usar funciones específicas de colecciones

``` ruby
# En lugar de:
[1, 2, 3].map { |x| [x, x+1] }.flatten
# Usar:
[1, 2, 3].flat_map { |x| [x, x+1] }

# En lugar de:
[1, 2, 3].select { |x| x > 2 }.count
# Usar:
[1, 2, 3].count { |x| x > 2 }

# En lugar de:
[1, 2, 3].shuffle.first
# Usar:
[1, 2, 3].sample

# En lugar de:
(1..10).select { |num| num % 3 == 0 }.first
# Usar:
(1..10).find { |num| num % 3 == 0 }
```


### El orden de las condiciones de los if es importante

Estas estructuras de control son más fácil de leer cuando comienzan con la condición positiva.

``` ruby
# En lugar de:
if !valid?
  "There is an error"
else
  "All ok"
end

# Usar:
if valid?
  "All ok"
else
  "There is an error"
end
```


## Documentación

> Documentation, when done successfully, can keep forward momentum in place and keep the team focused.

Es importante al escribir un programa, quey haya un espacio que contenga la información necesaria para que un desarrollador nuevo pueda comenzar a ser productivo cuanto antes. Este archivo debería por lo menos contar con la siguiente información:

1. En qué consiste la aplicación.
2. Pasos a seguir para instalar y usar la aplicación.
3. Estructura de la aplicación.
4. Otras explicaciones que puedan ser de utilidad al nuevo desarrollador.



### Comentarios

> Code can only tell you how the program works; comments can tell you why it works

El código por si mismo no puede explicar por qué el programa es escrito, o las razones por las que se elije un tipo de solución. Cuando el código no nos alcanza para dar las explicaciones necesarias a un nuevo programador, es buena idea comentar el código.

Pero es importante tener en cuenta que los comentarios también necesitan mantenimiento. Si no se los mantiene adecuadamente pueden ser confusos, obsoletos, o peor: incorrectos. Para lograr comentarios fáciles de mantener es importante no incluir información redundante.

El mejor tipo de comentarios es el que no necesitamos, y si se aprovecha la capacidad de expresión de Ruby, la necesidad de comentarios se ve reducida.

Un comentario ocasional para clarificar está bien, pero si nos encontramos escribiendo frecuentemente código con partes complicadas y comentarios, quizás llegó el momento de refactorizar.

-----------


### Palabras finales:

Las guías de estilos son una herramienta muy importante a la hora de trabajar en equipo, especialmente si queremos contribuir a proyectos de software libre. En estos casos, no ajustarse a una guía de estilos implica casi siempre que la contribución sea rechazada.

Considero que leer una guía de estilos me ha ayudado mucho a mejorar la forma en que escribo código. Usarlas es mi mejor recomendación. Sin más para agregar, espero que este artículo te haya sido de ayuda. Exitos! Y a trabajar en equipo!

### Lecturas interesantes:

* [Why coding style matters?](https://www.smashingmagazine.com/2012/10/why-coding-style-matters/)
* [Why use a style guide?](http://www.codereadability.com/why-use-a-style-guide/)
* [Writting great documentation](https://jacobian.org/writing/great-documentation/)
