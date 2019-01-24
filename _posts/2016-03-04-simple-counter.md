---
layout: post
title:  "Simple counter for my website"
category: articles
tags: programming
location: "La Plata"
visible: false
---

In this post I'll show you how to implement a counter that starts when the user loads the page. Something like this.

<ul class="counter"><!-- counter -->
  <li><span id="counter-0">0</span> chickens</li>
  <li><span id="counter-1">0</span> ducks</li>
  <li><span id="counter-2">0</span> pigs</li>
  <li><span id="counter-3">0</span> turkeys</li>
  <li><span id="counter-4">0</span> sheeps</li>
  <li><span id="counter-5">0</span> goats</li>
  <li><span id="counter-6">0</span> cows</li>
  <li><span id="counter-7">0</span> buffalos</li>
  <li><span id="counter-8">0</span> horses</li>
  <li><span id="counter-9">0</span> camelids</li>
</ul>

<div style="clear:both;"></div>

<script>
  var quantities =  [ 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 ];
  var velocities =  [ 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 ];

  function StartCounter() {

    var units = [
    49877536490, // gallinas
     2676365000, // patos
     1375940758, // cerdos
      635382008, // pavos
      564785251, // ovejas
      402611664, // cabras
      301275455, // vacas y terneros
       23199336, // bufalos
        5018470, // caballos
        1501799  // camellos y otros camelidos
    ];

    var bySecond = 4;
    for (var i = 0; i < quantities.length; ++i){
      velocities[i] = units[i] / 365 / 24 / 60 / 60 / bySecond;
    }
    setInterval(UpdateCounter, 1000 / bySecond);
  }

  function UpdateCounter() {
    var num, thous, str;
    for (var i = 0; i < quantities.length; ++i) {
      quantities[i] += velocities[i];
      num = Math.round(quantities[i]);
      str = "";
      while (num > 1000) {
        thous = num % 1000;
        if (thous < 10)
          thous = "00" + thous;
        else if (thous < 100)
          thous = "0" + thous;
        str = "," + thous + str;
        num = Math.floor(num / 1000);
      }
      str = num + str;
      document.getElementById("counter-" + i).innerHTML = str;
    }
  }

  StartCounter();
</script>

I wanted to have a counter on my [website][servegano] so the visitors would have a feeling about the number of animals killed by humans for food in the world every minute. And I wanted to implement this counter in [vanilla][vanilla] Javascript. I already had the number of animals killed by year, by species:

{% highlight html %}
<ul class="counter">
  <li><span id="counter-0">0</span> chickens</li>
  <li><span id="counter-1">0</span> ducks</li>
  <li><span id="counter-2">0</span> pigs</li>
  <li><span id="counter-3">0</span> turkeys</li>
  <li><span id="counter-4">0</span> sheeps</li>
  <li><span id="counter-5">0</span> goats</li>
  <li><span id="counter-6">0</span> cows</li>
  <li><span id="counter-7">0</span> buffalos</li>
  <li><span id="counter-8">0</span> horses</li>
  <li><span id="counter-9">0</span> camelids</li>
</ul>  
{% endhighlight %}


<!-- This is not the algorithm either. -->
<!-- But you are getting closer every time. -->
<!-- Keep looking for the algorithm. -->

### The algorithm


{% highlight javascript %}

var quantities =  [ 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 ];
var velocities =  [ 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 ];

function StartCounter() {

  var units = [
  49877536490, // chickens
   2676365000, // ducks
   1375940758, // pigs
    635382008, // turkeys
    564785251, // sheeps
    402611664, // goats
    301275455, // cows
     23199336, // buffalos
      5018470, // horses
      1501799  // camelids
  ];

  var bySecond = 4;
  for (var i = 0; i < quantities.length; ++i){
    velocities[i] = units[i] /
      365 / 24 / 60 / 60 / bySecond;
  }
  setInterval(UpdateCounter, 1000 / bySecond);
}

function UpdateCounter() {
  var num, thous, str;
  for (var i = 0; i < quantities.length; ++i) {
    quantities[i] += velocities[i];
    num = Math.round(quantities[i]);
    str = "";
    while (num > 1000) {
      thous = num % 1000;
      if (thous < 10)
        thous = "00" + thous;
      else if (thous < 100)
        thous = "0" + thous;
      str = "," + thous + str;
      num = Math.floor(num / 1000);
    }
    str = num + str;
    document.
      getElementById("counter-" + i).
      innerHTML = str;
  }
}

{% endhighlight %}


### Explanation

The function <code>setInterval</code> executes a function after waiting a specified number of milliseconds, and repeats the execution of that function continuously.

The function <code>UpdateCounter</code> updates the numbers on the list, using the quantities array and adding to it the number of animals killed since the last interval.

The function <code>StartCounter</code> calculates and initializes the <code>velocities</code> array, with the average number of animals killed by interval of time for each animal species.

That's it! Check out the [repo][gh] for more info.


### Side notes

The counter shows the number of animals killed in the world by the meat, dairy and egg industries, since you opened this webpage. This does not include the billions of fish and other aquatic animals killed annually.

It's based on 2007 statistics from the [Food and Agriculture Organization of the United Nations' Global Livestock Production and Health Atlas.][fao]

If you want to know more about veganism, [click here][vegankit].

[gh]:       https://github.com/nicanor/animal_counter
[fao]:      http://kids.fao.org/glipha/
[vegankit]: http://vegankit.com/why/
[vanilla]: http://vanilla-js.com/
[servegano]: http://servegano.com.ar/por-que-ser-veganos
