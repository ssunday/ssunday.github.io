---
title: Web Templates with Stencil
description: Creating web pages using Stencil, a Mustache implementation
date: 29/3/2016
---

[Mustache](https://mustache.github.io/) is a flexible way of making web templates. There are implementations in a plethora of different languages, including Clojure. Clojure has a few implementations, [Clostache](https://github.com/fhd/clostache) and [Stencil](https://github.com/davidsantiago/stencil) being the more notable of them.

Considering they both implement the same thing, they are very, very similar. Nearly identical. So close together in how they work that when the documentation for Stencil was lacking in one area, I simply read the Clostache one and it worked. I really can't tell much of a difference between Stencil and Clostache, except that the former claims to be faster and has much less documentation. They work the same; their point is to implement Mustache to have html templates with interpolation from code. And that is what they do.

Here is an example of one of my Stencil templates:

```html
<head>
  <meta charset="UTF-8">
  <style>
    body {background-color:lightgrey;
          padding: 60px;
          font-size: 20px;}
    h1 {border-style: dashed;}
  </style>
  <title>{header}</title>
  <h1>{header}</h1>
</head>
<body>
  <a href="/settings">{play-game}</a>
  <br><br>
  <a href="/scores">{see-scores}</a>
</body>
```

The curly brackets (they are double in reality, syntax highlighting doesn't like double brackets) are how Stencil/Mustache interpolates strings. I am interpolating them into the template because I need to localize to either English or German. The interpolation can even do quasi if-this then display this blocks with using {% highlight %}{% raw %} {#some-case}{% endraw %}  {% endhighlight %} to start and closing out with {% highlight %}{% raw %}{/some-case} {% endraw %} {% endhighlight %}. {% highlight %}{% raw %} some-case {% endraw %} {% endhighlight %} is something that can be tested for true/false passed in with all the other string information as a hashmap when rendering the file.

The render-file for an arbitrary case with the if-block could look like this:

```clojure
(stencil/render-file "/default-template" {:header "Some string" :some-case true})
```

And if some-case is true, it displays whatever is inside the region denoted by the curly brackets and does not show if it is false. Pretty simple.

Mustache/Stencil can also display arrays or lists relatively easily, among other features. I didn't need to use them so I didn't look into them all that much. It was pretty simple to use, once I got the hang of it.
