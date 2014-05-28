---
layout: post
title: O Fantástico Mundo do Python - Parte 1
categories:
- desenvolvimento
- linguagens
- php
- python
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
---
Gosto muito de programar, principalmente para Web. Sempre gostei muito de [PHP](http://br.php.net) e outras linguagens/tecnlogias do mundo Open Source, apesar de tambem ter trabalhado bastante com ASP/ASP.NET (C#) meu principal foco foi o mundo Open Source.





Ha um pouco menos de um ano comecei a estudar [Python](http://python.org) e cada dia que passa meu interesse por essa linguagem aumenta mais e mais.





Assim que lancei o blog recebi alguns comentarios e e-mails de pessoas pedindo conteudo de Python, pois sempre ouvem falar desta linguagem e gostariam de saber como ela e. Por isso resolvi listar algumas diferenças entre Python e PHP (umas das linguagens mais usadas no Brasil).





Abaixo segue uma lista com algumas diferenças entre a sintaxe e a estrutura de dados do PHP e do Python:




### 1. Criando listas (arrays)




#### PHP



{% highlight php %}
$numeros = array(1,2,3,4,5);
echo "O numero " . $numeros[1] . " e segundo numero da lista";
{% endhighlight %}




#### Python



{% highlight python %}
numeros = [1,2,3,4,5]
print "O numero %i e segundo numero da lista" % numeros[1]
{% endhighlight %}




### 2. Criando dicionarios (arrays associativos)




#### PHP



{% highlight php %}
$numeros = array(
    "um" => 1,
    "dois" => 2,
    "tres" => 3,
    "quatro" => 4,
    "cinco" => 5
);
echo "O numero " . $numeros["dois"] . " e segundo numero da lista";
{% endhighlight %}




#### Python



{% highlight python %}
numeros = {
    "um":1,
    "dois":2,
    "tres":3,
    "quatro":4,
    "cinco":5
}
print "O numero %i e segundo numero da lista" % numeros["dois"]
{% endhighlight %}




### 3. Percorrendo a lista (array)




#### PHP



{% highlight php %}
$numeros = array(1,2,3,4,5);
for ($i = 0; $i < count($numeros); $i++) {
    echo $numeros[$i];
}
{% endhighlight %}




#### Python



{% highlight python %}
numeros = [1,2,3,4,5]
for i in numeros:
    print i
{% endhighlight %}




### 4. Verificando se uma chave existe em um dicionario (array associativo)




#### PHP



{% highlight php %}
$numeros = array(
    "um" => 1,
    "dois" => 2,
    "tres" => 3,
    "quatro" => 4,
    "cinco" => 5
);
if (array("um", $numeros)) {
    echo "A chave existe";
}
{% endhighlight %}




#### Python



{% highlight python %}
numeros = {
    "um":1,
    "dois":2,
    "tres":3,
    "quatro":4,
    "cinco":5
}
if numeros.has_key("um"):
    print "A chave existe"
{% endhighlight %}




### 5. Replaces em String




#### PHP



{% highlight php %}
$titulo = "{NOME} e o Pe de Feijao";
$titulo = str_replace("{NOME}", "Joao", $titulo);
//Ou, para simplicar em uma unica linha
$titulo = str_replace("{NOME}", "Joao", "{NOME} e o Pe de Feijao");
{% endhighlight %}




#### Python



{% highlight python %}
titulo = "{NOME} e o Pe de Feijao"
titulo = titulo.replace("{NOME}", "Joao")
#Ou, para simplicar em uma unica linha
titulo = "{NOME} e o Pe de Feijao".replace("{NOME}", "Joao")
{% endhighlight %}




### 6. Escrevendo uma parte da String




#### PHP



{% highlight php %}
$titulo = "Joao e o Pe de Feijao";
echo substr($titulo, 9, 2);
{% endhighlight %}




#### Python



{% highlight python %}
titulo = "Joao e o Pe de Feijao"
print titulo[9:11]
{% endhighlight %}




### 7. Verificando tipo da variavel




#### PHP



{% highlight php %}
$var = "Teste";
if (is_array($var)) {
    echo "É array";
}
elseif (is_string($var)) {
    echo "É string";
}
elseif (is_integer($var)) {
    echo "É inteiro";
}
{% endhighlight %}




#### Python



{% highlight python %}
var = "Teste"
if type(var) == list:
    print "É array"
elif type(var) == str:
    print "É string"
elif type(var) == int:
    print "É inteiro"
{% endhighlight %}




### 8. Estrutura de controle




#### PHP



{% highlight php %}
$n = 4;
if ($n == 1) {
    echo "Um";
}
elseif ($n == 2) {
    echo "Dois";
}
else {
    echo "Maior que dois";
}
{% endhighlight %}




#### Python



{% highlight python %}
n = 4
if n == 1:
    print "Um"
elif n == 2:
    print "Dois"
else:
    print "Maior que dois"
{% endhighlight %}




### 9. Definindo funçoes




#### PHP



{% highlight php %}
function Teste() {
    echo "teste";
}
Teste();
{% endhighlight %}




#### Python



{% highlight python %}
def Teste():
    print "teste"
Teste()
{% endhighlight %}




### 10. Definindo classes




#### PHP



{% highlight php %}
class TestePai {
}
class Teste extends TestePai {
    public function __construct() {
        echo "Esta e a classe Teste que faz herança da classe TestePai.";
    }
}
$t = new Teste();
{% endhighlight %}




#### Python



{% highlight python %}
class TestePai:
    pass
class Teste(TestePai):
    def __init__(self):
        print "Esta e a classe Teste que faz herança da classe TestePai.";
t = Teste()
{% endhighlight %}




Perceba que, em todos os casos, acabamos escrevendo menos codigo em Python do que em PHP. Isso por que em Python temos uma estrutura de dados mais simples e sua forma de trabalhar sempre com objetos facilita muito a vida do programador. Ao inves de ficarmos decorando milhares de funçoes em PHP, decoramos somente alguns metodos em Python.





Particularmente, acho mais facil decorar metodos do que funçoes, isso porque os metodos se diferenciam entre os tipos de objetos disponiveis na linguagem. Alem disso, se eu estiver com duvida se algum metodo existe ou nao em determinado objeto, basta utilizar a funçao dir:




{% highlight python %}
>>> minha_lista = [1,2,3,4]
>>> dir(minha_lista)
['__add__', '__class__', '__contains__', '__delattr__', '__delitem__', '__delslice__', '__doc__',
'__eq__', '__ge__', '__getattribute__', '__getitem__', '__getslice__', '__gt__', '__hash__',
'__iadd__', '__imul__', '__init__', '__iter__', '__le__', '__len__', '__lt__', '__mul__',
'__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__reversed__', '__rmul__',
'__setattr__', '__setitem__', '__setslice__', '__str__', 'append', 'count', 'extend', 'index',
'insert', 'pop', 'remove', 'reverse', 'sort']
>>> lista.sort()
{% endhighlight %}




Ao digitar a funçao dir() passando como parametro o objeto minha_lista, podemos ver todos os metodo que um objeto do tipo list possui.





Em posts futuros colocarei exemplos mais complexos, e quem sabe envolvendo outras linguagens tambem...





Voce pode sugerir um exemplo, basta escrever nos comentarios...
