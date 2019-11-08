---
layout: post
title:  "Elixir, Phoenix y los desafíos de la nueva web"
category: articles
tags: programming talk español
location: La Plata
visible: true
---

<style>
@media print {
  h2 {
    page-break-before: always;
  }
}
</style>

Transcripción de la charla que dí el 7 de Noviembre para la [primera Elixir meetup de La Plata](https://elixir-la-plata.github.io/events/meetup-2019-11-07.html).

[Acá pueden descargar las diapositivas]({{ site.url }}/img/elixir-meetup-pdf.pdf)

-------

## Erlang

Elixir es un lenguaje de programación dinámico, diseñado para desarrollar aplicaciones escalables y mantenibles, que corre sobre la máquina virtual de Erlang.

Esta máquina virtual fue creada por Ericcson para resolver los problemas de la telefonía.
Específicamente de equipos de conmutación, que son necesarios para la operación de llamadas telefónicas.


Tenían requisitos de alta capacidad de concurrencia, alta disponibilidad, tolerancia a fallos, baja latencia y soporte para programación distribuída.

Como era muy difícil para ellos programar en los lenguajes a los que estaban acostumbrados, decidieron crear su propio lenguaje. Y así nació Erlang.


La concurrencia es un problema difícil. Algunos lenguajes no tienen buen soporte para concurrencia y otros usan distintas estrategias para abordar este problema.

La forma en que implementaron concurrencia en Erlang fue a través de procesos ligeros.

Estos procesos no son hilos de sistema operativo, sino que son procesos que maneja la máquina virtual de Erlang.

Estos procesos funcionan de forma aislada y se comunican entre ellos a través de mensajes.

Y son muy ligeros. Tan ligeros, que en una misma computadora puede haber cientos de miles de procesos vivos al mismo tiempo.

En computadoras con varios núcleos, estos procesos pueden correr de forma paralela.

Si tenemos una computadora con 32 nucleos, y tenemos 32 procesos, es posible que en un momento dado cada proceso corra sobre un núcleo diferente.

La máquina virtual de Erlang puede aprovechar la capacidad de las computadoras al máximo.

Y eso es importante, porque cada año las computadoras vienen con más núcleos.


## Elixir

En 2010, José Valim estaba trabajando en mejorar la velocidad de Rails en sistemas de múltiples núcleos, ya que las máquinas que usaba en producción cada vez venían con más núcleos.

Como cuenta él, toda la experiencia fue muy frustrante. Rails no proveía las herramientas apropiadas para resolver problemas de concurrencia. Ahí fue cuando José comenzó a mirar otras tecnologías y eventualmente se topó con la Máquina Virtual de Erlang.

José comenzó a usar *Erlang*, y se dio cuenta que Erlang era una base ideal para resolver los problemas que él quería resolver. Pero también notó que extrañaba algunas construcciones que estaban presentes en otros lenguajes.

Fue ahí que decidió crear Elixir.

## Un vistazo a Elixir

Lo primero que van a notar cuando es que la sintaxis se parece mucho a la de Ruby.

``` elixir
defmodule Math do
  # Esto es un comentario
  def sum(a, b) do
    a + b
  end
end

Math.sum(1,2) #=> 3
```

``` elixir
1        # Hay números,
true     # hay booleanos,
"Hola"   # hay strings,
:chau    # hay símbolos (que en elixir se llaman átomos),
[1,2,3]  # hay arreglos (que en elixir se llaman listas o tuplas),
%{key: "value"} # hay hashes (que en elixir se llaman mapas),
1..5  # hay rangos
```

Y además
* al igual que en Ruby, no hace falta poner puntos y comas al final de cada línea,
* al igual que en Ruby, toda expresión retorna un valor
* al igual que en Ruby, la última expresión es lo que retorna la función (no hace falta usar **return**)

Hay muchas construcciones parecidas, y esto es porque José Valim se baso fuertemente en la sintaxis de Ruby.

Si les gusta Ruby por ser un lenguajes expresivo, elegante, flexible, simple, fácil de leer y de entender, y que les permite hacer mucho con poco código, entonces por las mismas razones les va a encantar Elixir.

## Pero Elixir se parece más a Erlang que a Ruby.

Elixir no es un lenguaje Orientado a Objetos. No hay clases, no hay herencia, no hay *new* ni *initialize*, no hay variables de instancia, no hay variables globales, no hay objetos. No hay estado mutable.

Y esto no es un capricho.

Erlang fue diseñado con la concurrencia en mente, y es muy difícil implementar concurrencia cuando tenemos estado mutable distribuido por toda nuestra aplicación.

El estado mutable es aquel que cambia a través del tiempo.
El tiempo es una fuente de complejidad, porque agrega muchas partes en movimiento a nuestro sistema.
Terminamos con varias piezas de datos cambiando a distintos intervalos.

Es por eso que si estamos diseñando un lenguaje concurrente, no queremos que el estado mutable sea una primitiva del lenguaje, sino una abstracción a la que acudimos cuando la necesitamos.

## En Ruby, los objetos acoplan

* representación de datos
* lógica de programa
* organización de código
* manejo de estado y
* polimorfismo (por herencia).

En Elixir todas estas cuestiones son tenidas en cuenta por separado.

Por ejemplo, comparemos los siguientes códigos en Ruby y en Elixir:

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

En Elixir en cambio separamos la representación de datos (El string "Hola") de la lógica del programa (La función String.downcase).

El string `"HOLA"` no es un objeto. Es un valor.
Y los valores no tienen comportamiento.

* No saben cómo ponerse en minúsculas.
* No saben cómo calcular su largo.
* No saben cómo concatenarse con otro valor.

No arrastran consigo nada más que a sí mismos.
No tienen un puntero a sus métodos ni a su clase, ni a sus ancestros, ni tampoco variables de instancia.

En Elixir los valores son simples.
Son fáciles de crear y son fáciles de compartir.


## Identidad

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

Los strings del ejemplo tienen diferentes `object_id`. Son objetos diferentes.

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

`"Hola"` no es una cajita donde guardo un valor. Ni es un puntero a un valor.
`"Hola"` es el valor en sí mismo.

Y esto aplica también para las estructuras de datos.

``` elixir
  # Elixir
  [1, 2, 3] == [1, 2, 3] #=> true
```

Si tenemos la lista `[1, 2, 3]` en nuestra computadora, y la lista `[1, 2, 3]` en una computadora en China, decimos que son la misma lista.

Lo que define a un valor no es su posición en la memoria.

En elixir nos abstraemos de la memoria. Y esto tampoco es un capricho. Si no tenemos punteros y tenemos valores por referencia no necesitamos proteger una porción de memoria con locks, semáforos o monitores. Eso facilita implementar sistemas concurrentes.


## Valores inmutables

Y como consecuencia los valores son inmutables.
Los valores nunca se modifican.

En Ruby puedo instanciar un objeto, llamar un método destructivo y modificar el objeto original:

``` ruby
  # Ruby
  a = "HOLA"
  a.downcase! #=> "nil"
  a #=> "hola"
```

En Elixir en cambio, los valores no pueden ser modificados.
Cuando llamo a la función downcase, le paso un valor por parámetro y la función no lo modifica, sino que retorna un nuevo valor:

``` elixir
  # Elixir
  a = "HOLA"
  String.downcase(a) #=> "hola"
  a #=> "HOLA"
```

Si los datos son inmutables, entonces se eliminan los problemas de interacción entre procesos por mutación de datos.
Esto hace mucho más fácil implementar un sistema concurrente.


## Funciones

En Elixir, los parámetros de las funciones se pasan por valor, no por referencia, y esto hace que sea fácil implementar funciones puras.

Una función pura es aquella en la que los valores que retorna dependen únicamente de los parámetros de entrada.
Ante los mismos parámetros, una función pura retorna siempre el mismo resultado.

Si una función depende sólo de sus parámetros de entrada es mucho más sencillo predecir su comportamiento.
Y es mucho más facil de testearla. Y es mucho más fácil razonar sobre la función.
Si las funciones son puras es más fácil implementar un sistema concurrente.

En Ruby pasamos los parámetros por referencia.
Hacemos sea posible que un método modifique el objeto original fuera de la llamada a la función.
Y además en Ruby, los métodos tienen acceso al estado interno del objeto.
Las variables de instancia pueden ser accedidas y modificadas por métodos.

En Ruby, puede pasarnos que tegamos un bug que sólo ocurre cuando un objeto está en un estado en particular.

Reproducir el problema puede ser complicado porque no siempre es fácil descifrar el estado interno de un objeto.
Y una vez que se lo hace puede ser difícil reproducirlo, porque quizás sólo ocurre luego de que lo activa una cadena particular de eventos.

En programación funcional se pasan los datos a través de un conjunto de funciones y los datos nunca mutan.
La salida de una función es la entrada de la función siguiente.
Cuando ocurre un error es más fácil descifrar qué pasa y dónde pasa.
La mutación significa pérdida de información, y no hay mutación en Elixir.

Lo que no significa que no haya efectos secundarios.
Eventualmente vamos a querer escribir algo en pantalla, o acceder a una base de datos o a un servidor.
O crear un proceso.
Y todo eso se puede hacer perfectamente en Elixir.

## Procesos

``` elixir
  # Elixir
  spawn(fn -> 1 + 2 end)
  #=> #PID<0.111.0>
```

La función spawn es la función mas básica para crear procesos.
Lo que devuelve es el PID, que es el identificador único de proceso.
Los procesos son creados, hacen lo que tienen que hacer y mueren.

Hay funciones para crearlos, hay funciones para enviar y recibir mensajes,
hay funciones para linkear procesos entre sí.

Pero en la vida real, nunca llamamos *spawn* directamente, sino que acudimos a abstracciones.

* Si queremos implementar un modelo de productor/consumidor, vamos a usar `GenStage`.
* Si queremos implementar una tarea simple, vamos a usar `Task`.
* Si queremos implementar un modelo cliente/servidor, vamos a usar `Agent` o `GenServer`.
* Si queremos que un proceso supervise a otro, vamos a usar `Supervisor`.

Y si un proceso falla, el proceso supervisor puede revivirlo en un estado seguro.
En elixir podemos crear arboles de supervisión, que dan a la aplicación tolerancia a fallos y permiten la autoreparación. Hay aplicaciones Erlang que están corriendo hace 20 años.

La buena noticia es que no es necesario saber todo esto para empezar a programar en Elixir y Phoenix.
Todas estas cuestiones se pueden aprender sobre la marcha a medida en que se necesitan, y aún así ser sumamente productivos.

## Phoenix

*Phoenix* es un framework web escrito en Elixir.

Phoenix ya aprovecha por si mismo todo el poder de los procesos de Erlang en todas sus partes.
Cada vez que recibe una petición HTML, se crea un proceso nuevo, lo que permite que miles de personas puedan acceder simultáneamente a su sitio web, sin ningún problema.

La mayor parte del equipo detrás de Phoenix viene de la comunidad Rails, por lo que es natural que haya tomado prestadas algunas buenas ideas:

* Ambos son frameworks MVC que se centran en la productividad.
* Proveen una estructura de directorio por defecto y generadores.
* Usan bases de datos relacionales por defecto.
* Promueven mejores practicas de seguridad por defecto.
* Vienen equipados con herramientas de testing.


## Migraciones

Así se ve una migración en Rails y en Phoenix:

``` ruby
class CreateArticles < ActiveRecord::Migration[6.0]
  def change
    create_table :articles do |t|
      t.string :name
      t.text :description        
      t.timestamps
    end
  end
end
```
Para poder usar los métodos de migración, en Rails se hereda de `ActiveRecord::Migration`.


``` elixir
defmodule MyWeb.Repo.Migrations.CreateArticle do
  use Ecto.Migration

  def change do
    create table(:articles) do
      add :title, :string
      add :description, :string
      timestamps
    end
  end
end
```

En Phoenix, no existe la herencia, así que en su lugar se usa la linea `use Ecto.Migration`.


## Rutas

En Rails tenemos la filosofía de **convención sobre configuración**.
En la medida en que nos apeguemos a las convenciones, Rails nos permite escribir menos código.

``` ruby
resources :articles do
  resources :comments, only: [:comment]
end
post "login", to: "sessions#login"
root to: "pages#index"
```

En Elixir tenemos la filosofía de **explicito es mejor que implicito**.
En las rutas siempre tengo que decir explicitamente cual es el controlador que se encarga de cada acción.

``` elixir
resources "/articles", ArticleController do
  resources "/comments", CommentController, only: [:show]
end
post "/login", SessionController, :login
get "/", PageController, :index
```


Escribimos un poco más de código, pero tenemos mucha más flexibilidad.

Para apegarnos a la convención, en Rails tenemos que usar el nombre del modelo en plural.
Y si es irregular, tenemos que definir las reglas de pluralización en `Inflector`.

Phoenix es mucho más flexible. Podemos usar los nombres que queramos.
Después de todo, siempre los vamos a nombrar de forma explícita.


## Controladores

Hay varios puntos para tener en cuenta.

``` ruby
class ArticlesController < ApplicationController
  def show
    @article = Article.find(params[:id])
    # render "show.html"
  end
end
```

En primer lugar, en Rails la acción show no recibe ningún parámetro.
Tengo acceso directo a `params`, al objeto `request` y a cualquier variable de instancia creada en un `before_action`.


``` elixir
defmodule MyWeb.ArticleController do
  use MyWeb.Web, :controller

  def show(conn, %{"id" => id}) do
    article = Blog.get_article!(id)
    render(conn, "show.html", article: article)
  end
end
```


En Phoenix tengo que pasar todo lo que uso por parámetro. La variable `conn` vendría a ser el equivalente al request object de Rails. La acción show es una función como cualquier otra y la ventaja de recibir todo por parámetro es que puedo testearla de forma aislada.

El segundo punto es que la acción show de Rails llama implicitamente a **render "show.html"**.
El render copia todas las variables de instancia del controlador a la instancia de la vista.

En Phoenix, en cambio, siempre hay que escribir render de forma explícita.
Todo lo que necesite usar en la vista lo mando en la función render.
Eso significa que puedo testear las vistas de forma aislada.

Convención sobre configuración es algo bueno, pero hay un punto en el que el comportamiento implícito sacrifica la claridad. **Phoenix optimiza por claridad**.


## Vistas

Las vistas se parecen mucho en su sintáxis a las vistas de Rails:

``` elixir
<h1><%= @article.title %></h1>
<p><%= @article.description %></p>
<%= for comment <- @article.comments do %>
  <p class="comment"><%= comment.content %></p>
<% end %>
<%= link "Editar", to: article_path(@conn, :edit, @article) %>
<%= link "Volver", to: article_path(@conn, :index) %>
```


## Estructura de Directorio

Si vienen del mundo Rails y quieren aprender Phoenix corren con una gran ventaja.
La estructura de directorios creada por Phoenix tiene muchos puntos en común con la de Rails

La mayoría de los conceptos mapea uno a uno.

![Mapeo uno a uno](/img/mapeo-uno-a-uno.png){:style="width: 100%"}


En poco tiempo de empezar van a ser productivos.


## Channels

Así como Rails tiene su famoso tutorial de como hacer un blog en 15 minutos, Phoenix tiene su tutorial de cómo hacer un chat en tiempo real en 15 minutos. Phoenix tiene un soporte excelente para websockets.

Los websockets permiten comunicación ida y vuelta entre cliente y servidor, sin refrescar la página.

Esto significa que en Phoenix es muy fácil implementar
- Chats en tiempo real.
- Notificaciones en tiempo real.
- Herramientas colaborativas con muchas personas conectadas al mismo tiempo
- Ver quienes están conectados, y cuando se conecta o desconecta alguien.
- Un buscador que se comunique a varias APIs y retorne resultados a medida que van llegando.

Definimos un socket, un channel y un poco de código Javascript y ya tenemos el chat andando.
Casi con la misma facilidad con que definimos una vista y un controlador.

Los canales se manejan con procesos de Erlang, lo que permite que haya millones de personas conectadas al mismo tiempo usando una sola computadora de servidor. Phoenix provee gran soporte para alta concurrencia totalmente gratis.


## Rendimiento

Algunas personas me dicen que no tienen necesidad de alta concurrencia.
A su sitio web entran 2 o 3 personas al mismo tiempo máximo.

Igualmente hay buenas razones para usar Phoenix.

Aunque hoy no necesiten alta concurrencia, puede ser que en algún momento lo necesiten.
¿Y que mejor oportunidad para empezar a familiarizarse con el lenguaje y el framework que un sitio web pequeño y de bajo riesgo?

Otra razón para usar Phoenix es el rendimiento.

Hace un tiempo hice una [comparación informal entre una aplicación básica Phoenix y Rails]({% post_url 2019-01-23-rendimiento-phoenix-vs-rails %}).
Y la aplicación Phoenix, con acceso a bases de datos corriendola localmente era alrededor de 7 veces más rápida.

Y sin acceso a bases de datos, la diferencia era aún mayor.
En Phoenix es común ver reportes como este:

```
Sent 200 in 517µs
```

Ese símbolo significa microsegundos. Eso es medio milisegundo.

El rendimiento es muy importante, especialmente en la web.

Está demostrado que si una página tarda más de 100 milisegundos en cargar, afecta negativamente la atención de las personas. Hay estudios de cómo compañías multiplicaron sus conversiones reduciendo el tiempo de respuesta unos cuantos milisegundos.

Y también es importante para el programador durante el desarrollo.
Nosotros tenemos los mismos problemas de atención.

¿Nunca les pasó esperar tanto a que pase algo de no acordarse de lo que estaban haciendo?

En Phoenix, correr el servidor es casi instantaneo.
La navegación es inmediata, se siente como si fuera una pagina web estática.
Los tests tardan segundos en lugar de minutos.
Esto impacta positivamente en nuestra atención y en nuestra experiencia en la programación.

Y el rendimiento no es sólo mejor en velocidad, sino también en memoria.

Bleacher Report hizo la transición de Rails a Elixir, y pasaron de usar 150 servidores a usar 5 servidores, y al mismo tiempo mejoraron sus tiempos de respuesta para sus 200 millones de notificaciones push diarias.

Pienso que una de las razones por la que hacemos sitios web pequeños es porque no nos animamos a hacer cosas más grandes.

Cuando contás con todo el poder de la máquina virtual de Erlang en tus manos, te animás a desafíos que no pensabas que estaban a tu alcance.

Elixir hace fáciles problemas históricamente complicados, y gracias a que estas soluciones ahora están a tu alcance, te animás a ofrecerle a tus clientes funcionalidades mucho más emocionantes.

Phoenix tiene la capacidad de darles una ventaja competitiva a sus clientes, y también a ustedes como empresa y a ustedes como programadores.


## Los retos de la web moderna

La web está evolucionando. La web moderna es **altamente conectada** y necesita sistemas en tiempo real.
Requiere incluir dispositivos conectados como tables, teléfonos y relojes.

Necesita sistemas de alta disponibilidad, escalables, tolerantes a fallos y distribuidos.
Necesita sistemas que puedan aprovechar al máximo la capacidad de procesamiento de las computadoras.

Erlang y Elixir fueron creados para resolver este tipo de problemas.
*Phoenix* fue construido desde el primer día para enfrentarse a los retos de la web moderna.

Las tecnologías avanzan muy rápidamente y en nuestro rubro es importante poder adaptarnos a los nuevos requerimientos.
Simplemente tenemos que vencer los miedos y animarnos.

**¿Nos animamos a enfrentar los desafíos de la nueva web?**
