---
layout: post
title:  "Rendimiento Phoenix vs Rails"
category: articles
tags: programming español elixir phoenix rails
location: Auckland, New Zealand
visible: true
---

<style>
.content p code, .content pre {font-size: 1.2em;}
</style>

Muchas personas afirman que Phoenix (el framework web de Elixir más usado) es más rápido que Rails (el framework web de Ruby). ¿Pero cuánto más rápido? La respuesta es por supuesto: Depende!

Lo que haré a continuación es crear dos sitios web sencillos uno en Phoenix y otro en Rails
usando los generadores por defecto.
Compararé su rendimiento y trataré de defender la idea que
Phoenix es una buena opción por sobre Rails,
incluso en aplicaciones web simples en las que las capacidades de tiempo real no sean una prioridad.

Para evitar polémicas, quiero aclarar que esto va a ser una comparación super informal.
Simplemente haré pruebas y compartiré los resultados de 2 aplicaciones puntuales en mi computadora.
Estos resultados pueden ser diferentes en otras computadoras y haciendo cambios en las aplicaciones,
por ejemplo usando algún tipo de caché.

Usaré Rails 5.2 con Ruby 2.3 y Phoenix 1.3 con Elixir 1.6.

[Click aquí para saltar el setup de las aplicaciones](#comparación)

## Rails setup:

El primer paso es crear la aplicación web, correr los generadores y preparar la base de datos:

```
rails new prueba-rails -d postgresql
cd prueba-rails
rails g scaffold Articulo nombre descripcion:text contenido:text
```

Para ser justos en la comparación correremos el código en modo producción. Modificamos el archivo
database.yml con nuestras credenciales y ejecutamos:
```
RAILS_ENV=production rake assets:precompile
RAILS_ENV=production rake db:create
RAILS_ENV=production rake db:migrate
```

Corremos el comando `RAILS_ENV=production rake secret` y agregamos la clave secreta al archivo
*config/secrets.yml*.

El siguiente paso es crear 20 artículos para mostrar en el índice de artículos.
Para esto, modificar el archivo *seed.rb* y ejecutar el comando `RAILS_ENV=production rake db:seed`.

``` ruby
DESCRIPCION = 'Lorem ipsum ultricies libero sit amet massa vulputate venenatis. Morbi lobortis elementum eros.'

CONTENIDO = 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vestibulum volutpat odio elit, id sollicitudin augue ullamcorper sit amet. Curabitur id pulvinar libero. Donec ultricies libero sit amet massa vulputate venenatis. Morbi lobortis elementum eros, eget pulvinar tortor fringilla ullamcorper. Quisque tellus neque, aliquam sit amet ultricies ac, interdum at est. Nullam lectus arcu, bibendum ac accumsan interdum, malesuada vel purus. Quisque odio erat, scelerisque at auctor ac, auctor nec est. Nulla facilisi.'

20.times do |n|
  Articulo.create(
    nombre: "Articulo #{n}",
    descripcion: DESCRIPCION,
    contenido: CONTENIDO
  )
end
```

### Resultados:
En una terminal, ejecutar el comando `rails s` y en otra el comando

`ab -n 1000 -c 50 http://0.0.0.0:3000/articulos`

```
Server Software:
Server Hostname:        0.0.0.0
Server Port:            3000

Document Path:          /articulos
Document Length:        20402 bytes

Concurrency Level:      50
Time taken for tests:   6.940 seconds
Complete requests:      1000
Failed requests:        0
Total transferred:      21065000 bytes
HTML transferred:       20402000 bytes
Requests per second:    144.08 [#/sec] (mean)
Time per request:       347.024 [ms] (mean)
Time per request:       6.940 [ms] (mean, across all concurrent requests)
Transfer rate:          2963.95 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    0   0.4      0       3
Processing:    83  340  32.1    344     431
Waiting:       82  339  32.2    343     431
Total:         85  340  31.9    344     432

Percentage of the requests served within a certain time (ms)
  50%    344
  66%    354
  75%    359
  80%    362
  90%    369
  95%    374
  98%    383
  99%    390
 100%    432 (longest request)
```

La respuesta promedio fue de `340 ms`.




## Phoenix setup:

El primer paso es crear nuestra aplicación web, correr los generadores y preparar la base de datos:

```
mix phx.new prueba_phoenix
cd prueba_phoenix
MIX_ENV=prodmix ecto.create
mix phx.gen.html CMS Articulo articulos nombre descripcion:text contenido:text
    Add the resource to your browser scope in lib/prueba_phoenix_web/router.ex:
        resources "/articulos", ArticuloController
```

Phoenix recomienda agregar una linea al archivo de rutas.
Una vez agregada la linea, correr el comando `MIX_ENV=prod mix ecto.migrate`.

Modificar el archivo *priv/repo/seeds.exs*:

``` elixir
defmodule PruebaPhoenix.Seeder do
  alias PruebaPhoenix.Repo
  alias PruebaPhoenix.CMS.Articulo

  @descripcion "Lorem ipsum ultricies libero sit amet massa vulputate venenatis. Morbi lobortis elementum eros."

  @contenido "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vestibulum volutpat odio elit, id sollicitudin augue ullamcorper sit amet. Curabitur id pulvinar libero. Donec ultricies libero sit amet massa vulputate venenatis. Morbi lobortis elementum eros, eget pulvinar tortor fringilla ullamcorper. Quisque tellus neque, aliquam sit amet ultricies ac, interdum at est. Nullam lectus arcu, bibendum ac accumsan interdum, malesuada vel purus. Quisque odio erat, scelerisque at auctor ac, auctor nec est. Nulla facilisi."

  def crear_articulo(n) do
    Repo.insert!(%Articulo{
      nombre: "Articulo #{n}",
      descripcion: @descripcion,
      contenido: @contenido
    })
  end

end

(1..20) |> Enum.each(fn(n) -> PruebaPhoenix.Seeder.crear_articulo(n) end)
```

Crear los artículos ejecutando el comando `MIX_ENV=prod PORT=4000 mix run priv/repo/seeds.exs`.

Ejecutamos:

```
mix deps.get --only prod
MIX_ENV=prod mix compile
```

Precompilamos los assets:

```
cd assets
brunch build --production
cd ..
mix phx.digest
```

### Resultado de Phoenix:
En una terminal:

`MIX_ENV=prod PORT=4000 mix phx.server`

y en otra terminal

`ab -n 1000 -c 50 http://0.0.0.0:4000/articulos`

```
Server Software:        Cowboy
Server Hostname:        0.0.0.0
Server Port:            4000

Document Path:          /articulos
Document Length:        25114 bytes

Concurrency Level:      50
Time taken for tests:   1.074 seconds
Complete requests:      1000
Failed requests:        0
Total transferred:      25616000 bytes
HTML transferred:       25114000 bytes
Requests per second:    930.75 [#/sec] (mean)
Time per request:       53.720 [ms] (mean)
Time per request:       1.074 [ms] (mean, across all concurrent requests)
Transfer rate:          23283.21 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    0   0.4      0       5
Processing:    10   53  19.6     50     116
Waiting:        9   51  19.1     48     116
Total:         10   53  19.7     50     118

Percentage of the requests served within a certain time (ms)
  50%     50
  66%     59
  75%     66
  80%     70
  90%     80
  95%     89
  98%     99
  99%    103
 100%    118 (longest request)
```

La respuesta promedio fue de `53 ms`.

## Comparación

La aplicación Phoenix demoró 1 segundo en completar los 1000 llamados, con un promedio de 53 ms por
respuesta. Mientras que la aplicación Rails demoró casi 7 segundos, con un promedio de 340 ms por
respuesta. Es decir, la aplicación Phoenix de ejemplo corre entre 6 y 7 veces más rápido que la
aplicación Rails.

## Mis conclusiones

Como ya mencioné antes, esto fue sólo una pequeña prueba. Posiblemente se pueda mejorar mucho la
performance de la aplicación Rails agregando algún tipo de Caché. Aunque para ser justos, eso aplica
también para la aplicación Phoenix.

Si bien no creo que la velocidad sea la principal ventaja de Phoenix por sobre Rails,
creo que la velocidad sí es importante: Significa una mejor experiencia para el usuario, pero además
mejora la experiencia al desarrollar y ayuda a simplificar el código.

En la mayoría de las aplicaciones Rails que he construido me he visto obligado a
_ensuciar_ el código con ElasticSearch, Sidekiq, Redis, RabbitMQ y distintos tipos de caché,
porque la aplicación no era lo suficientemente rápida.

Mi experiencia con Phoenix es muy distinta: usando las herramientas por defecto suelo obtener un
rendimiento más que suficiente. No suelo pensar en usar otras herramientas, que agregan complejidad
y puntos de fallo al sistema. En consecuencia el código termina siendo más fácil de mantener.

¡Pero reitero! Esto fue una prueba super informal. Mi consejo: hacé las pruebas por vos misma/o y
animate a usar Phoenix para tu próximo proyecto! Pero te advierto: *¡Va a ser difícil!*

Siempre aprender un lenguaje y un framework nuevo cuesta. Vas a encontrarte con un montón de errores
nuevos, y vas a tener una gran resistencia de entrada. Recordá que la primera vez que tocaste Rails
también fue dificil. Que todo lo que hoy sabés y te resulta tan claro, lo tuviste que aprender en
algún momento. ¡Y te costó!

Esto también va a costar. Mi sugerencia es que arranques con un proyecto pequeño.
¿Te animás?
