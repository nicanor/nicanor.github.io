---
layout: page
title: About
---

{% for post in site.categories.about %}
{% include summary.html post=post %}
{{ post.content }}
* * *
{% endfor %}

Nicanor Perera is a software developer with more than <span id="years-of-experience">7</span> years of experience, who lives and works in La Plata (Buenos Aires, Argentina). Nicanor started his career as a freelance, while he studied computer science in *La Plata's National University*.

Nicanor developed dozens of projects until 2012, when he started to work as a web programmer in [Xaver](http://www.xaver.com.ar) and specialized in Rails technologies.

On July 2014, Nicanor left Xaver to become a software developer in  [Snappler](http://snappler.com/), where he currently works as project leader.

<script>
function timeSince(date) {
  var miliseconds = Math.floor((new Date() - date));
  return Math.floor(miliseconds / 31536000000);
}
var yearsOfExperience = timeSince(new Date('2009-01-01'));
document.getElementById("years-of-experience").innerHTML = yearsOfExperience;
</script>

Nicanor loves free software and to share his code with everybody. He is always interested in new technologies and right now, he feels very enthusiastic about [Elixir][elixir] and [Phoenix][phoenix]


[{{ site.email }}]({{ site.email | prepend: "mailto:" }})
[{{ site.github_username | prepend: "github.com/" }}]({{ site.github_username | prepend: "https://github.com/" }})
[{{ site.twitter_username | prepend: "twitter.com/" }}]({{ site.twitter_username | prepend: "https://twitter.com/" }})

### About this website

This website Jekyll project was copied and adapted from awesome [Christopher Adams][chris] website, who was very kind at sharing it with everybody.

[elixir]: http://elixir-lang.org/
[phoenix]: http://www.phoenixframework.org/
[chris]: https://christopheradams.io