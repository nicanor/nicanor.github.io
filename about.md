---
layout: page
title: About
---

{% for post in site.categories.about %}
{% include summary.html post=post %}
{{ post.content }}
* * *
{% endfor %}

<img src="../img/nica.jpg"/>

Hi. My name is Nicanor Perera and I'm a Ruby on Rails developer with more than
<span id="years-of-experience">7</span> years of experience.

I was born in Argentina and I'm currently living in New Zealand.

I worked in [Xaver](http://www.xaver.com.ar) as web developer and in
[Snappler](http://snappler.com/) as project leader.

I'm always interested in new technologies and right now
I'm feeling very enthusiastic about [Elixir][elixir] and [Phoenix][phoenix].

<script>
function timeSince(date) {
  var miliseconds = Math.floor((new Date() - date));
  return Math.floor(miliseconds / 31536000000);
}
var yearsOfExperience = timeSince(new Date('2009-01-01'));
document.getElementById("years-of-experience").innerHTML = yearsOfExperience;
</script>

[{{ site.email }}]({{ site.email | prepend: "mailto:" }})
[{{ site.github_username | prepend: "github.com/" }}]({{ site.github_username | prepend: "https://github.com/" }})
[{{ site.twitter_username | prepend: "twitter.com/" }}]({{ site.twitter_username | prepend: "https://twitter.com/" }})

### About this website

The code from this blog was copied and adapted from [Christopher Adams][chris] website.

[elixir]: http://elixir-lang.org/
[phoenix]: http://www.phoenixframework.org/
[chris]: https://christopheradams.io
