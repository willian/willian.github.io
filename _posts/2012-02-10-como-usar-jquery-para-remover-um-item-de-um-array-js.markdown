---
layout: post
title: Como usar jQuery para remover um item de um Array JS
categories:
- desenvolvimento
- javascript
- jquery
- web
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
---
Quem trabalha com JavaScript sabe que para remover um item de um array basta utilizar o metodo _splice_. Como o codigo abaixo:


{% highlight javascript %}
frutas = ['maça', 'banana', 'pera', 'uva'];
frutas.splice(1,1);
{% endhighlight %}


O codigo acima retira a _banana_ do _array frutas_. Isso porque no 1º parametro do metodo _splice_ informamos qual a posiçao do item no array que queremos remover. O 2º parametro indica quantos itens, contando do item que informamos, queremos remover. Sendo assim, se quisermos remover a _banana_ e a _pera_ basta fazer assim:


{% highlight javascript %}
frutas = ['maça', 'banana', 'pera', 'uva'];
frutas.splice(1,2);
{% endhighlight %}


Mas em muitos casos nao sabemos qual a posiçao do item que queremos remover e sim qual o valor do item. Uma abordagem e procurar qual a posiçao do item percorrendo o Array e comparando os valores com o valor que temos. Um tanto quanto chato, concorda?



## jQuery para todas as horas!



Como e mais que comum termos jQuery em projetos web, realizar o trabalho acima fica facil. Pra isso precisaremos da funçao _$.grep_. Esta funçao encontra todos os elementos de um array de acordo com uma expressao. Vamos aplicar nosso exemplo removendo a fruta _banana_ do nosso _array_, mas agora nao sabemos qual a posiçao que essa fruta se encontra no _array_. Nosso codigo ficara assim:


{% highlight javascript %}
frutas = ['maça', 'banana', 'pera', 'uva'];
frutas = $.grep(frutas, function(val, index) {
	return val != 'banana';
});
{% endhighlight %}


Com a funcao _$.grep_ podemos ir muito alem. Por exemplo, ter um array com somente os elementos que forem pares:


{% highlight javascript %}
numeros = [1, 2, 3, 4, 5, 6, 7, 8];
pares = $.grep(numeros, function(v) {
	return v % 2 == 0;
});

// Valor do array pares: [2, 4, 6, 8]
{% endhighlight %}


A funçao $.grep recebe 2 parametros obrigatorios: o array original e uma funçao _callback_. Esse _callback_ recebe, por sua vez, 2 parametros: o valor do item atual e o indice (posiçao) desse valor no array.
Existe um terceiro parametro (nao obrigatorio) da funçao _$.grep_ chamado _inverse_, que por padrao tem o valor _false_. Esse parametro inverte a condiçao dentro do _callback_, fazendo exatamente o contrario que mandamos ela fazer. Se adicionarmos o parametro _inverse_ no exemplo acima, teremos:


{% highlight javascript %}
numeros = [1, 2, 3, 4, 5, 6, 7, 8];
pares = $.grep(numeros, function(v) {
	return v % 2 == 0;
}, true); // Perceba que adicionamos um novo parametro

// Valor do array pares: [1, 3, 5, 7]
// pares agora so contem os valores impares
{% endhighlight %}


Perceba que a funçao _$.grep_ **nao altera o array original**. Nos exemplos acima o array _numeros_ continuara tendo todos os elementos.

Bom, e isso. Espero que agora remover itens de um array JavaScript utilizando o valor seja mais facil no seu dia-a-dia.

**[ATUALIZADO]**

Algumas pessoas se manifestaram no Twitter dizendo que isso e errado. Realmente, existe uma forma bem simples de remover um item de um Array em JavaScript sem saber a posiçao desse item e sem usar jQuery. Segue abaixo:


{% highlight javascript %}
frutas = ['maça', 'banana', 'pera', 'uva'];
index = frutas.indexOf('banana');
frutas.splice(index, 1);
{% endhighlight %}


Utilizamos o _indexOf_ para descobrir qual a posiçao do valor que queremos remover e depois conseguiremos utilizar o _splice_ normalmente.

Agora, sobre a parte de retornar somente os numeros pares, o [Nando Vieira](http://twitter.com/fnando) deu uma dica boa:


{% highlight javascript %}
[1, 2, 3, 4, 5, 6, 7, 8].filter(function(item) {
	return item % 2 == 0;
});
{% endhighlight %}


**OBS.:** Navegadores antigos nao suportam a funçao _filter()_. Use por sua conta e risco.
