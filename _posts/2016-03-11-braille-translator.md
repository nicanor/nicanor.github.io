---
layout: post
title:  "Braille translator in ruby (with TDD)"
category: articles
tags: programming
location: La Plata
---

This post is about *Test Driven Development* in Ruby, and how to implement it even in small projects.
I recently watched a talk from *Uncle Bob* about TDD as a discipline, and jumped to this [article][uncle].
I've never done TDD before, so I wanted to give it a try. The [3 laws of TDD][laws] are:

1. You can't write any production code until you have first written a failing unit test.
2. You can't write more of a unit test than is sufficient to fail, and not compiling is failing.
3. You can't write more production code than is sufficient to pass the currently failing unit test.

Aparently there are [Unicode Braille patterns][unicode] So, in order to implement something with TDD, let's make a ruby program to translate letters to their [spanish braille][spanish-braille] equivalent.

I'll use rspec for testing.

Here is the convertion we want to make:

```
⠁ a, 1    ⠞ t   ⠷ á
⠃ b, 2    ⠥ u   ⠮ é
⠉ c, 3    ⠧ v   ⠌ í
⠙ d, 4    ⠺ w   ⠬ ó
⠑ e, 5    ⠭ x   ⠾ ú
⠋ f, 6    ⠽ y   ⠳ ü
⠛ g, 7    ⠵ z
⠓ h, 8    ⠨ Signo de mayúsculas
⠊ i, 9    ⠼ Signo de número
⠚ j, 0    ⠄ Punto (.) (punto 3)
⠅ k   ⠂ Coma (,) (punto 2)
⠇ l
⠢ Signos de interrogación (¿?)
⠍ m   ⠆ Punto y coma (;)
⠝ n   ⠖ Signos de exclamación (¡ !)
⠻ ñ   ⠒ Dos puntos (:)
⠕ o   ⠦ Comillas (de cualquier tipo)
⠏ p   ⠣ Abrir paréntesis "("
⠟ q   ⠜ Cerrar paréntesis ")"
⠗ r   ⠤ Guion (-)
⠎ s   ⠀ Espacio (ningún punto)
```


Let's start with a simple test:

``` ruby
it "changes 'a' to '⠁'" do
  translator = Braille::Translator.new
  expect(translator.call('a')).to eq('⠁')
end
```

Excelent! we have our first test!. If we try to run it, the test will fail. And that is what it is supoused to do.
Now, let's make the test pass with some code:

``` ruby
class Translator
  def call(word)
    return "⠁"
  end
end
```

I know it seems silly, but it is a good start.
For every iteration of testing and programming, you will have a completelly tested code that works.
If we run the test suite now, the test will pass, and in order to continue we should add a new test.


### The result

Working this way was very interesting for learning, and it was very funny.
The final code was very clean, and I finished with a very reliable code.
And I am using this gem in production for my [website][acordes-totales].

### The complete algorithm:

<!-- Every day you get closer and closer -->
<!-- But this is not the algorithm either -->
<!-- You can find it! Be like the penguin! -->

``` ruby
class Translator
  def call(group_of_words)
    group_of_words.split(' ').map do |word|
      translate_word(word)
    end.join('⠀')
  end

  def translate_word(word)
    if /\d+/.match(word)
      translate_number(word)
    else
      word.split('').map do |char|
        translate_character(char)
      end.join
    end
  end

  def translate_number(number_in_letters)
    '⠼' + number_in_letters.tr('1234567890','⠁⠃⠉⠙⠑⠋⠛⠓⠊⠚')
  end

  def translate_character(character)
    case character
    when ('a'..'z')
      character.tr('abcdefghijklmnopqrstuvwxyz',
                   '⠁⠃⠉⠙⠑⠋⠛⠓⠊⠚⠅⠇⠍⠝⠕⠏⠟⠗⠎⠞⠥⠧⠺⠭⠽⠵')
    when ('A'..'Z')
      '⠨' + translate_character(character.downcase)
    when /á|é|í|ó|ú|ü|ñ/
      character.tr('áéíóúüñ','⠷⠮⠌⠬⠾⠳⠻')
    when /.|;|¡|!|:|"|\'|(|)|-/
      character.tr('.;¡!:"\'()-','⠄⠆⠖⠖⠒⠦⠦⠣⠜⠤')
    else
      ''
    end
  end
end
```

Check out the [repo][gh] and analize the commits if you want to see how I did it testing function by function.


[gh]:       https://github.com/nicanor/braille
[laws]: http://programmer.97things.oreilly.com/wiki/index.php/The_Three_Laws_of_Test-Driven_Development
[uncle]: http://blog.cleancoder.com/uncle-bob/2014/12/17/TheCyclesOfTDD.html
[unicode]:  http://www.unicode.org/charts/PDF/U2800.pdf
[spanish-braille]: https://en.wikipedia.org/wiki/Spanish_Braille
[acordes-totales]: http://acordestotales.com/
