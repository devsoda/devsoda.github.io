---
layout: post
title:  "Entendendo o Document Fragment"
date:   2014-11-22 12:27:17
categories: javascript fragment dev js
---

Cada vez que alteramos o DOM causamos um reflow no documento e isso pode ser muito custoso em termos de performance. Utilizando Document Fragment podemos diminuir bastante o custo de performance.

Vejamos o seguinte trecho.

{% highlight js %}
var list = document.getElementById("carsList"),
cars = ["Fusca", "Gol", "Tempra", "BMW", "Tipo", "Chevette", "Kombi"];


for (var i = 0, x = cars.length; i < x; i++;) {
    var e = document.createElement("li");
    e.appendChild(document.createTextNode(cars[i]));
    list.appendChild(e);
}
{% endhighlight %}

Toda vez que a lista é inserida (append), o DOM é acessado e causa um reflow inteiro do documento. Se sua lista for muito grande, esse processo fará com que sua página perca muito em performance.

O ideal é que a lista seja inserida apenas uma vez. Neste caso, podemos usar o Document Fragment para inserir a lista toda de uma só vez.

Os Fragments vão funcionar como containers invisíveis para guardar todas as li criadas.

Primeiramente vamos criar um fragment.

{% highlight js %}
var list = document.getElementById("carsList"),
cars = ["Fusca", "Gol", "Tempra", "BMW", "Tipo", "Chevette", "Kombi"];

var fragment = document.createDocumentFragment();

for (var i = 0, x = cars.length; i < x; i++;) {
    var e = document.createElement("li");
    e.appendChild(document.createTextNode(cars[i]));
    list.appendChild(e);
}
{% endhighlight %}

Agora vamos inserir todas as li no fragment.

{% highlight js %}
var list = document.getElementById("carsList"),
cars = ["Fusca", "Gol", "Tempra", "BMW", "Tipo", "Chevette", "Kombi"];

var fragment = document.createDocumentFragment();

for (var i = 0, x = cars.length; i < x; i++) {
    var e = document.createElement("li");
    e.appendChild(document.createTextNode(cars[i]));
    fragment.appendChild(e);
}
{% endhighlight %}

E finalmente vamos inserir de uma vez só no DOM todos os elementos guardados no fragment.

{% highlight js %}
var list = document.getElementById("carsList"),
cars = ["Fusca", "Gol", "Tempra", "BMW", "Tipo", "Chevette", "Kombi"],
fragment = document.createDocumentFragment();

for (var i = 0, x = cars.length; i < x; i++) {
    var e = document.createElement("li");
    e.appendChild(document.createTextNode(cars[i]));
    fragment.appendChild(e);
}

list.appendChild(fragment);
{% endhighlight %}