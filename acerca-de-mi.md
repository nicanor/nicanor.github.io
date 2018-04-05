---
layout: page
title: Acerca de mí
id: acerca-de-mi
---

(Read in [english](/about-me)).

<img style="width:100%;" src="../img/nica.jpg"/>

Hola. Mi nombre es Nicanor Perera y soy un desarrollador Ruby on Rails con más
de <code id="years-of-experience"></code> años de experiencia.

<script>
function timeSince(date) {
  var miliseconds = Math.floor((new Date() - date));
  return Math.floor(miliseconds / 31536000000);
}
var yearsOfExperience = timeSince(new Date('2010-01-01'));
document.getElementById("years-of-experience").innerHTML = yearsOfExperience;
</script>

Me recibí de
[Licenciado en Informática](http://info.unlp.edu.ar/carreras-de-grado-lic-en-informatica/)
en la _Universidad Nacional de La Plata_.

Mi último trabajo fue como desarrollador Ruby on Rails en
[Harmoney](http://harmoney.co.nz), una empresa de _prestamos peer to peer_
localizada en Auckland, Nueva Zelanda, donde vivo actualmente.

Antes trabajé para [Snappler](http://snappler.com/) durante 3 años como
desarrollador Ruby on Rails y en [Xaver](http://www.xaver.com.ar) como desarrollador web.

Siempre estoy interesado en nuevas tecnologías. Hoy en día estoy muy interesado
en el lenguaje de programación [Elixir][elixir] y el framework web
[Phoenix][phoenix].


### Contactame:
* [{{ site.email }}]({{ site.email | prepend: "mailto:" }})
* [{{ site.github_username | prepend: "github.com/" }}]({{ site.github_username | prepend: "https://github.com/" }})
* [{{ site.twitter_username | prepend: "twitter.com/" }}]({{ site.twitter_username | prepend: "https://twitter.com/" }})

[elixir]: http://elixir-lang.org/
[phoenix]: http://www.phoenixframework.org/
