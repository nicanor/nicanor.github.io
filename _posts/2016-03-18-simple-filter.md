---
layout: post
title:  "Simple vanilla javascript filter"
category: articles
tags: programming
location: La Plata
---

In this post I'll show you how to implement a simple filter in vanilla javascript, like this one:

<label for="color-select">Color</label>
<select id="color-select" name="color-select">
  <option value="">All</option>
  <option value="red">Red</option>
  <option value="green">Green</option>
  <option value="blue">Blue</option>
</select>

<ul id="colorful-animals-list">
  <li data-color="blue"  style="color:blue;">Blue Bird</li>
  <li data-color="blue"  style="color:blue;">Blue Cat</li>
  <li data-color="red"   style="color:red;">Red Rabbit</li>
  <li data-color="green" style="color:green;">Green Chicken</li>
  <li data-color="blue"  style="color:blue;">Blue Dog</li>
  <li data-color="red"   style="color:red;">Red Cow</li>
  <li data-color="red"   style="color:red;">Red Frog</li>
  <li data-color="green" style="color:green;">Green Bee</li>
  <li data-color="blue"  style="color:blue;">Blue Dolphin</li>
  <li data-color="green" style="color:green;">Green Octopus</li>
  <li data-color="red"   style="color:red;">Red Iguana</li>
  <li data-color="green" style="color:green;">Green Human</li>
</ul>

<script>

var Refresh = (function () {
  var elements = document.getElementById('colorful-animals-list').children,
      length   = elements.length,
      select   = document.getElementById('color-select');

  select.addEventListener('change', function(event) {
    Refresh();
    event.preventDefault();
  });

  return function () {
    var selected_color = select.value;
    for (var i = 0; i < length; i++) {
      elements[i].style.display =
        (!selected_color || elements[i].dataset.color === selected_color) ? '' : 'none';
    }
  };
})();

</script>


Let's say that we have a very long list of colorful animals like the following:
<div style="clear:both;"></div>


``` html
<ul id="colorful-animals-list">
  <li data-color="blue" >Blue Bird</li>
  <li data-color="blue" >Blue Cat</li>
  <li data-color="red"  >Red Rabbit</li>
  <li data-color="green">Green Chicken</li>
  <li data-color="red"  >Red Dog</li>
  <li data-color="red"  >Red Cow</li>
  <li data-color="green">Green Pig</li>
</ul>
```

And we want to be able to filter animals by color (because otherwise it would be really difficult to find the ones we are looking for).

<!-- This is not the algorithm. -->
<!-- This algorithm can't find Jesus. -->
<!-- Keep looking for the algorithm. -->

#### The algorithm:

For hiding the elements, we will change their <code>display</code> property to <code>none</code>.

So we will implement the function <code>Refresh</code> to perform this task.

We have to create a select input with the values we want to filter. Something like this:

``` html
<select id="color-select" name="color-select">
  <option value=""></option>
  <option value="red">Red</option>
  <option value="green">Green</option>
  <option value="blue">Blue</option>
</select>
```

And add an event listener for that select input, so that it triggers the <code>Refresh</code> function every time it changes.

Here is the complete code:

``` javascript
var elements = document.getElementById('colorful-animals-list').children,
    length   = elements.length,
    select   = document.getElementById('color-select');

Refresh = function () {
  var selected_color = select.value;
  for (var i = 0; i < length; i++) {
    elements[i].style.display =
      (!selected_color || elements[i].dataset.color === selected_color) ? '' : 'none';
  }
};

select.addEventListener('change', function(event) {
  Refresh();
  event.preventDefault();
});
```

That's it! Check out the [repo][gh].


[gh]: https://github.com/nicanor/javascript-filter
[vanilla]: http://vanilla-js.com/