---
layout: post
title:  "Elixir La Plata Primera Edición"
category: articles
tags: programming talk español
location: La Plata
visible: true
---

# Bienvenida y objetivos

Hola a todos.

¿Cómo andan?

Primero que nada, muchas gracias por venir y muchas gracias a Snappler por prestarnos el lugar y ayudarnos a organizar el evento.

Mi nombre es Nicanor, y les doy la bienvenida a la primera meetup de Elixir en La Plata.

Varias personas ya me conocen. En Noviembre de 2016, dí una charla sobre Phoenix y Elixir en La Colmena.
¿Alguno fue a esa charla?

En ese momento trabajaba para Snappler, y estaba super entusiasmado por dar la charla.
Si bien recién empezaba a conocer estas tecnologías, la charla fue muy bien recibida.
Hace más de 9 años que uso Rails en mi trabajo y hace más de 3 años que uso Phoenix para mis proyectos personales.

En estos años han pasado muchas cosas en Elixir.
Ahora Elixir tiene soporte para releases, que es una herramienta invaluable para hacer deployment.
Ahora Elixir tiene un formateador automático de código, que mejora la calidad del código y el trabajo en equipo.
Ahora Phoenix te incentiva a organizar tu código en contextos, lo que ayuda a desacoplar código en celulas independientes.
La comunidad ha crecido muchísimo.
Hoy en día, en Github, hay 3 veces más repositorios en Elixir que en Erlang.

Y yo, 3 años después, sigo igual de entusiasmado que cuando dí esa primera charla.

Nuestros objetivos hoy son contagiarles nuestro entusiasmo, compartir lo que hemos aprendido en estos años con ustedes, ayudarlos a dar los primeros pasos con estas tecnologías y generar comunidad. Si nos sale bien, vamos a haber puesto las bases para que este sea el primero de muchos eventos de este tipo.

Hoy tenemos 2 charlas.

La primera la voy a dar yo, voy a hablarles de Erlang, Elixir, Phoenix, por qué existen, por qué son como son y cómo nos podemos beneficiar de estas tecnologías. La primera charla que dí hablé de muchos temas muy superficialmente. Hoy voy a ser un poco más selectivo, y le voy a dedicar un poco más de tiempo a esos temas que considero importantes.

La segunda la va a dar Federico y va a enfocarse en cómo aprender Elixir, y ayudarlos a dar los primeros pasos.

---

## Comienzo con unas preguntas:

_Preguntar quienes saben lo que es Elixir,
quienes han escrito alguna linea de código
y quienes lo han usado en producción.

Preguntar también quienes son programadores Rails,
y los que no lo sean, preguntar qué hacen_


## Máquina virtual de Erlang

Elixir es un lenguaje de programación dinámico, diseñado para desarrollar aplicaciones escalables y mantenibles.
Corre sobre la máquina virtual de Erlang.

Esta máquina virtual fue creada para resolver los problemas de la telefonía.
Específicamente de equipos de conmutación, que son necesarios para la operación de llamadas telefónicas.

Los lenguajes que usaban no cumplían con los requisitos, y decidieron crear un lenguaje nuevo.
Necesitaban un lenguaje con alta capacidad de concurrencia, de alta disponibilidad, tolerante a fallos y de baja latencia y con soporte para programación distribuída. Y crearon Erlang.

La concurrencia es un problema difícil.
Muchos lenguajes no tienen buen soporte para concurrencia.

Hay distintas estrategias para abordar este problema.
Algunos lenguajes, como rust, afrontan este problema con threads.
Otros como Go, lo hacen a través de rutinas y canales.

La forma en que implementaron concurrencia en Erlang fue a través de procesos ligeros.
Estos procesos no son threads de sistema operativo, sino que son procesos que maneja la máquina virtual de Erlang.
Son muy ligeros, muy fáciles de crear y muy fáciles de destruir.

Los procesos de la máquina virtual de Erlang son tan ligeros, que en una misma computadora puede haber cientos de miles de procesos vivos al mismo tiempo.

Es el caso de Whatsapp, cuya infraestructura está implementada en Erlang.
Cada computadora en la que corre el servidor de *Whatsapp* puede manejar **2 millones de conexiones** al mismo tiempo.
*Whatsapp* tiene **500 millones de usuarios activos por día** y sólo **50 ingenieros**.

Estos procesos funcionan de forma aislada y se comunican entre ellos a través de mensajes.
En computadoras con varios núcleos, estos procesos pueden correr de forma paralela.
Si tenemos una computadora con 32 nucleos, y tenemos 32 procesos, es posible que en un momento dado cada proceso corra sobre un núcleo diferente.

La máquina virtual de Erlang aprovecha la capacidad de la computadora al máximo.

Y eso es importante, porque cada año las computadoras vienen con más núcleos.
Y eso aplica también para las computadores que usamos de servidor.

## Elixir

En 2010, José Valim estaba trabajando en mejorar la velocidad de Rails en sistemas de múltiples núcleos, ya que las máquinas que usaba en producción cada vez venían con más núcleos.

Como cuenta él, toda la experiencia fue muy frustrante. Rails no proveía las herramientas apropiadas para resolver problemas de concurrencia. Ahí fue cuando José comenzó a mirar otras tecnologías y eventualmente se topó con la Máquina Virtual de Erlang.

José comenzó a usar *Erlang*, y se dio cuenta que Erlang era una base sólida para resolver los problemas que él quería resolver.
Pero también notó que extrañaba algunas construcciones que estaban presentes en otros lenguajes.

Fue ahí que decidió crear Elixir, en un intento de traer novedosas herramientas por encima de la máquina virtual de Erlang.

## Un vistazo a Elixir

Antes de arrancar con las partes más técnicas, vamos a echar un vistazo a cómo se ve Elixir.

``` elixir
defmodule Math do
  # Esto es un comentario
  def sum(a, b) do
    a + b
  end

  def duplicate(a) do
    2 * a
  end
end

Math.sum(1,2) #=> 3
Math.duplicate(5) #=> 10
```

Lo primero que van a notar es que la sintaxis se parece mucho a la de Ruby.

* Hay números,
* hay booleanos,
* hay strings,
* hay símbolos (que en elixir se llaman átomos),
* hay arreglos (que en elixir se llaman listas),
* hay hashes (que en elixir se llaman maps),
* hay rangos,
* hay fechas

* al igual que en Ruby, no hace falta poner puntos y comas al final de la línea,
* al igual que en Ruby, toda expresión retorna un valor
* al igual que en Ruby, la última expresión es lo que retorna la función (no hace falta usar **return**)

Hay muchas construcciones parecidas, y esto es porque José Valim se baso fuertemente en la sintaxis de Ruby.
Si les gusta Ruby por ser un lenguajes Expresivo, Elegante, Flexible, Simple, fácil de leer y de entender, y que les permite hacer mucho con poco código, entonces por las mismas razones les va a encantar Elixir.

----

Pero Elixir se parece más a Erlang que a Ruby.

Elixir no es un lenguaje Orientado a Objetos. No hay clases, no hay herencia, no hay *new* ni *initialize*, no hay variables de instancia, no hay variables globales, no hay objetos. No hay estado mutable oculto.

Y esto no es un capricho.

Erlang fue diseñado con la concurrencia en mente, y es muy difícil implementar concurrencia cuando tenemos **estado mutable** distribuido por toda nuestra aplicación.

### Estado mutable

El estado mutable es aquel que cambia a través del tiempo.
El tiempo es una fuente de complejidad, porque agrega muchas partes en movimiento a nuestro sistema.
Terminamos con varias piezas de datos cambiando a distintos intervalos.

Es por eso que si estamos diseñando un lenguaje concurrente, no queremos que el estado mutable sea una primitiva del lenguaje, sino una abstracción a la que acudimos cuando la necesitamos. Y lo hacemos de forma explícita.

### Acoplamiento

Los objetos acoplan

* representación de datos
* lógica de programa
* organización de código
* manejo de estado y
* polimorfismo por herencia.

En Elixir todas estas cuestiones son tenidas en cuenta por separado.

``` ruby
  # Ruby
  "HOLA".downcase #=> "hola"
```

``` elixir
  # Elixir
  String.downcase("HOLA") #=> "hola"
```

En Ruby, `"HOLA"` es un objeto de clase String, que define el método `downcase`.
El objeto `"HOLA"` sabe como ponerse en minúsculas.
Decimos que la representación de datos está acoplada a la lógica de programa.

En Elixir en cambio el string `"HOLA"` no es un objeto. Es un valor.

Y los valores no tienen comportamiento.

* No saben cómo ponerse en minúsculas.
* No saben cómo calcular su largo.
* No saben cómo concatenarse con otro valor.

No arrastran consigo nada más que a sí mismos.
No tienen un puntero a sus métodos ni a su clase, ni a sus ancestros, ni tampoco variables de instancia.

`"Hola"` no es una cajita donde guardo un valor. Ni es un puntero a un valor.
`"Hola"` es el valor en sí mismo.

La lógica de programa la definen las funciones, no los valores.

En Elixir los valores son simples.
Son fáciles de crear y son fáciles de compartir.


### Identidad

¿Qué nos retorna la siguiente expresión?

``` ruby
  # Ruby
  "Hola".equal?("Hola")
```

Nos retorna `false`.


``` ruby
  # Ruby
  a = "Hola"
  b = "Hola"
  a.object_id #=> 70227497266080
  b.object_id #=> 70227497236260
```

Como pueden ver, tienen diferentes `object_id`. Son objetos diferentes.
Por más que ambos estén conformados por las mismas letras en el mismo orden, no podemos decir que sean el mismo string.
Son objetos guardados en distintas posiciones de memoria.

En Elixir en cambio no existe el concepto de `equal?`, porque no existe el concepto de `object_id`.

``` elixir
  # Elixir
  "Hola" == "Hola" #=> true
```

Si dos strings tienen las mismas letras en el mismo orden, decimos que son el mismo valor.
La identidad de un valor está dada por el valor en sí mismo.
Decimos que los valores en Elixir son identificables por sí mismos.

Y esto aplica también para las estructuras de datos.

``` elixir
  # Elixir
  [1, 2, 3] == [1, 2, 3] #=> true
```

Si tenemos la lista `[1, 2, 3]` en nuestra computadora, y la lista `[1, 2, 3]` en una computadora en China, decimos que son la misma lista.

Lo que define a un valor no es su posición en la memoria.

En elixir nos abstraemos de la memoria. No necesitamos proteger una porción de memoria con locks, semáforos o monitores.
No tenemos punteros. No tenemos valores por referencia. Eso facilita implementar sistemas concurrentes.


### Valores inmutables

Y también son inmutables.
Los valores nunca se modifican.

``` ruby
  # Ruby
  a = "HOLA"
  a.downcase! #=> "nil"
  a #=> "hola"
```

``` elixir
  # Elixir
  a = "HOLA"
  String.downcase(a) #=> "hola"
  a #=> "HOLA"
```

Si los datos son inmutables, entonces se eliminan los problemas de interacción entre hilos de ejecución por mutación de datos. Es mucho más fácil implementar un sistema concurrente.


### Funciones

Cuando se pasa parámetros por referencia hacemos que sea posible que la función modifique el dato.
Y en ruby, los métodos tienen acceso al estado interno del objeto.

En cambio, en Elixir, los parámetros de las funciones se pasan por valor, no por referencia.
Recuerden que en Elixir nos importa qué valor es. No donde está.
Pasar parámetros por valor hace que sea fácil implementar funciones puras.

Una función pura es aquella en la que los valores que retorna dependen únicamente de los parámetros de entrada.
Ante los mismos parámetros, una función pura retorna siempre el mismo resultado.

Si una funcion depende sólo de sus parámetros de entrada es mucho más sencillo predecir su comportamiento.
Y es mucho más facil de testearla. Y es mucho más fácil razonar sobre la función.

----- Acá me quedé -----

No siempre podemos escapar de los efectos secundarios. Eventualmente vamos a querer escribir algo en pantalla, o acceder a una base de datos o a un servidor.

En programación funcional se pasan los datos a través de secuencias de funciones y los datos nunca mutan. La salida de una función es la entrada de la función siguiente. Cuando ocurre un error es más fácil descifrar qué pasa y dónde pasa. La mutación significa pérdida de información, y no hay mutación en programación funcional.

Les ha pasado en Ruby, tener un bug que sólo ocurren cuando un objeto está en un estado en particular.

Reproducir el problema puede ser complicado porque no siempre es facil decifrar el estado internos de un objeto.
Y una vez que se lo hace puede ser difícil reproducirlo, porque quizás sólo ocurre luego de que lo activa una cadena particular de eventos.

En programación funcional se pasan los datos a través de un conjunto de funciones y los datos nunca mutan. La salida de una función es la entrada de la función siguiente. Cuando ocurre un error es más fácil descifrar qué pasa y dónde pasa. La mutación significa pérdida de información, y no hay mutación en programación funcional.

## Procesos

Como les dije hoy, la mutación no es una primitiva del lenguaje, sino una abstracción a la cual acudimos cuando la necesitamos, y cuando lo hacemos lo hacemos explícitamente. Si tenemos que lidiar con datos que cambian con el tiempo, lo podemos hacer a través de procesos.

``` elixir
  # Elixir
  spawn(fn -> 1 + 2 end)
  #=> #PID<0.111.0>
```

La función spawn es la función mas básica para crear procesos.
Lo que devuelve es el PID, que es el identificador único de proceso.
Los procesos son creados, hacen lo que tienen que hacer y mueren.
Hay funciones para crearlos, hay funciones para enviar y recibir mensajes, hay funciones para linkear procesos entre sí.

Pero en la vida real, nunca usamos estas funciones directamente, sino que acudimos a abstracciones.

Si queremos implementar un modelo de productor/consumidor, vamos a usar `GenEvent`.
Si queremos implementar una tarea simple, vamos a usar `Task`.
Si queremos implementar un modelo cliente/servidor, vamos a usar `Agent` o `GenServer`.
Si queremos que un proceso supervise a otro, vamos a usar `Supervisor`.

Un proceso puede supervisar a otro.
Y si un proceso falla, el proceso supervisor puede revivirlo en un estado seguro.
En elixir podemos crear arboles de supervición, que dan a la aplicación tolerancia a fallos y permiten el self-healing [mejorar]

Se que esto es mucha información.
Pero no se preocupen. No necesitan saber todo esto para empezar a programar en Elixir y Phoenix.

Phoenix ya aprovecha por si mismo todo el poder de los procesos de Erlang en todas sus partes.
Cada vez que recibe una petición HTML, se crea un proceso nuevo, lo que permite que miles de personas puedan acceder simultáneamente a su sitio web, sin ningún problema.

[Caso 2.000.000]

Phoenix usa eficientemente los procesos para acceder a la base de datos, para correr los tests e incluso para compilar la aplicación. Sin necesidad de acudir a todas estas abstracciones, ya van a disfrutar de todos los beneficios que les ofrece la máquina virtual de Erlang de forma gratuita.

Todas estas cuestiones las pueden aprender sobre la marcha, y aún así ser sumamente productivos.

## Phoenix

*Phoenix* es un framework web escrito en Elixir.

La mayor parte del equipo detrás de Phoenix viene de la comunidad Rails, por lo que es natural que hayan tomado algunas de las excelentes ideas que trae Rails.

Ambos son frameworks MVC que se centran en la productividad. Proveen una estructura de directorio por defecto y generadores, ambos tienen un archivo de rutas, ambos usan bases de datos relacionales por defecto (sqlite3 en Rails y Postgresql en Phoenix). Ambos promueven mejores practicas de seguridad por defecto y vienen equipados con herramientas de testing.

Así se ve una vista en Phoenix:
[codigo]

Así se ve un controlador
[codigo]

Así se ve una migración
[codigo]

Así se ven las rutas
[codigo]

Esta es la estructura de directorio de Rails y esta la de Phoenix.

Si vienen del mundo Rails y quieren aprender Phoenix corren con una gran ventaja.

La mayoría de los conceptos mapea 1 a 1.

[Imagen con flechitas]

En poco tiempo de empezar van a ser productivos.

## Websockets

Phoenix tiene un soporte excelente para websockets.
Los websockets permiten comunicación ida y vuelta entre cliente y servidor, sin refrescar la página.

Esto significa que en Phoenix es trivial implementar

- Chats en tiempo real. Yo escribo, e inmediatamente le llega el mensaje a la otra persona, sin recargar la página (websockets)
- Notificaciones en tiempo real, por ejemplo cuando alguien me puso me gusta.
- Herramientas colaborativas con muchas personas conectadas al mismo tiempo
- Ver quienes están conectados, y cuando se conecta o desconecta alguien. (Presence)
- Un buscador que le pegue a varios 3rd parties y retorne resultados a medida que van llegando.
- Hacer streaming a la base de datos, trabajar los datos y crear un reporte CSV en tiempo real, y enviarselo al usuario a través de HTTP streaming.

Así como Rails tiene su famoso tutorial de como hacer un blog en 15 minutos, Phoenix tiene su tutorial de cómo hacer un chat en tiempo real en 15 minutos. Pueden hacer un chat en vivo con la misma facilidad con que definen una vista y un controlador.

## Rendimiento

Algunas personas me dicen que no tienen necesidad de alta concurrencia.
A su sitio web entran 2 o 3 personas al mismo tiempo máximo.

Igualmente hay buenas razones para usar Phoenix.

Una de ellas es el rendimiento.

En Phoenix es común ver reportes como este:

```
Sent 200 in 517µs
```

Esos son microsegundos. Eso es medio milisegundo.

Hace poco hice una comparación informal entre una aplicación básica Phoenix y Rails.
Y la aplicación Phoenix, con acceso a bases de datos corriendola localmente era alrededor de 7 veces más rápida.
La pueden leer en mi página web.

Me acuerdo que una vez logre mejorar un código para que vaya un 50% más rápido. Y lo festejé. Y para mí era una mejora increíble. Acá estoy hablando de 7 veces más rápido.

Y eso es muy importante, especialmente en la web.
Está demostrado que si una página tarda más de 100 milisegundos en cargar, afecta negativamente la atención de las personas. Hacen cambio de contexto. Hay estudios de cómo compañías multiplicaron sus conversiones simplemente reduciendo el tiempo de espera unos cuantos milisegundos.

Y también es importante para el programador durante el desarrollo.
Nosotros tenemos los mismos problemas de atención.
Cuando corren el servidor, no tienen que esperar varios segundos para ver la página.
Cada navegan el sitio localmente se siente inmediato, como si fuera una pagina web estática.
Cuando corren los tests tarda segundos en lugar de minutos.
Esto impacta positivamente en nuestra atención.

El rendimiento es importante.

E incluso si tampoco les parece importante, un sitio sencillo de bajo riesgo es un buen candidato para darle una oportunidad a Phoenix y empezar a familiarizarse con el framework.

Y se me ocurre también que una de las razones por la que hacemos sitios web pequeños es porque no nos animamos a hacer cosas mas grandes. Elixir hace que problemas históricamente complicados sean de repente triviales.

Y el rendimiento no es sólo velocidad, sino también memoria.

Bleacher Report hizo la transición de Rails a Elixir, y pasaron de usar 150 servidores a usar 5 servidores, y al mismo tiempo mejoraron sus tiempos de respuesta para sus 200 millones de notificaciones push diarias.

Cuando contás con todo el poder de la máquina virtual de Erlang en tus manos, te animás a desafíos que no pensabas que estaban a tu alcance. Phoenix tiene la capacidad de darles una ventaja competitiva a sus clientes, y también a ustedes como empresa y a ustedes como programadores.

# Final

La web está evolucionando. La web moderna es **altamente conectada** y necesita sistemas en tiempo real. Requiere incluir dispositivos conectados como teléfonos, relojes y sistemas embebidos. Necesita sistemas de alta disponibilidad. Sistemas escalables, tolerantes a fallos y distribuidos. Necesita sistemas que puedan aprovechar al máximo la capacidad de procesamiento de las computadoras.

La programación web tiene muchos problemas en común con la telefonía. Erlang y Elixir fueron creados para resolver este tipo de problemas. *Phoenix* fue construido desde el primer día para enfrentarse a los retos de la web moderna. Las tecnologías avanzan muy rápidamente y en nuestro rubro es importante poder adaptarnos a los nuevos requerimientos.

Simplemente tenemos que vencer los miedos y animarnos.

Así que les pregunto: **Nos animamos a enfrentar los desafíos de la nueva web?**
