---
layout: page
title: About me
id: about
---

<small>[Leer en español](/acerca-de-mi).</small>


<img style="width:100%;" src="../img/nica.jpg"/>

Hi. My name is Nicanor Perera and I'm a web developer with more than
<code id="years-of-experience"></code> years of experience.

<script>
function timeSince(date) {
  var miliseconds = Math.floor((new Date() - date));
  return Math.floor(miliseconds / 31536000000);
}
var yearsOfExperience = timeSince(new Date('2010-01-01'));
document.getElementById("years-of-experience").innerHTML = yearsOfExperience;
</script>

I'm currently working for [Brandkit](https://www.brandkit.io/) as an [Elixir][elixir] and Rails developer.

Before that, I worked for [Harmoney](http://harmoney.co.nz), [Snappler](http://snappler.com/)
and [Xaver](http://www.xaver.com.ar).

I have a degree in computer science from *La Plata's National University*.

I'm always interested in new technologies.

## Contact me:
* [{{ site.email }}]({{ site.email | prepend: "mailto:" }})
* [{{ site.github_username | prepend: "github.com/" }}]({{ site.github_username | prepend: "https://github.com/" }})
* [{{ site.twitter_username | prepend: "twitter.com/" }}]({{ site.twitter_username | prepend: "https://twitter.com/" }})

[elixir]: http://elixir-lang.org/
