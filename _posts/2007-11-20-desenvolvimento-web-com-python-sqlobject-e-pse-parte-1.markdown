---
layout: post
title: Desenvolvimento Web com Python, SQLObject e PSE - Parte 1
categories:
- desenvolvimento
- internet
- linguagens
- python
- web
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
---
Já faz um tempo que estou ensaiando para escrever sobre como <a href="http://boo-box.com/link/aff:submarinoid/uid:255486/tags:programação site" class="bbli">desenvolvemos aplicações web<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a> lá na <a href="http://visie.com.br/afiliados/3/visie.com.br/cursos">Visie</a>. Nós utilizamos Python porque amamos essa linguagem e achamos uma dupla excelente para auxiliar no desenvolvimento Web. Estou falando do <a href="http://nick.borko.org/pse/">PSE</a> e do <a href="http://sqlobject.org/">SQLObject</a>.

Existem muitas <a href="http://www.pythonbrasil.com.br/moin.cgi/PythonParaWeb">alternativas que permitem a criação de aplicações web com Python</a>, mas a que irei apresentar nessa série de artigos é a que prefiro.

Primeiro explicarei do que se trata cada ingrediente que utilizaremos e depois como instalá-los, configurá-los e como utilizá-los.

<strong>Python</strong>
Uma linguagem dinâmica, interativa e orientada a objetos. Diferente de linguagens como o <a href="http://boo-box.com/link/aff:submarinoid/uid:255486/tags:php" class="bbli">PHP<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a>, Python possui tipagem forte, mas não necessita de declarações de variáveis. É uma linguagem interpretada e não compilada, como <a href="http://boo-box.com/link/aff:submarinoid/uid:255486/tags:java" class="bbli">JAVA<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a> e <a href="http://boo-box.com/link/aff:submarinoid/uid:255486/tags:.net c vb" class="bbli">DotNet<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a>.

Já <a href="http://willianfernandes.com.br/o-fantastico-mundo-do-python-parte-1/">falei sobre Python anteriormente</a>, citando exemplos comparativos com PHP. Mas se você ainda não conhece a linguagem e quiser aprender sobre ela, segue abaixo uma lista de sites que recomendo:

<ul>
    <li><a href="http://www.pythonbrasil.com.br/">PythonBrasil</a>
        <ul>
            <li><a href="http://www.pythonbrasil.com.br/moin.cgi/InicieSe">Inicie-se: instalando Python no seu sistema.</a></li>
            <li><a href="http://www.pythonbrasil.com.br/moin.cgi/AprendaMais">Aprenda Mais: dicas de como aprender a programar em Python.</a></li>
            <li><a href="http://www.pythonbrasil.com.br/moin.cgi/AprendaProgramar">Aprenda a Programar</a></li>
        </ul>
    </li>
    <li><a href="http://www.python.org/">Site Oficial</a></li>
    <li><a href="http://visie.com.br/afiliados/3/visie.com.br/cursos/python.pt">Treinamento</a></li>
</ul>

<strong>SQLObject</strong>
Trata-se de uma biblioteca de <a href="http://boo-box.com/link/aff:submarinoid/uid:255486/tags:mapeamento objeto relacional" class="bbli">mapeamento objeto-relacional<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a> escrita em Python.
O objetivo do SQLObject é o mesmo do <a href="http://boo-box.com/link/aff:submarinoid/uid:255486/tags:hibernate" class="bbli">Hibernate<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a> para JAVA e do nHibernate para DotNet: permitir que as tabelas de um banco de dados sejam mapeadas e utilizadas como objetos dentro do programa.

Felizmente, o SQLObject possui uma <a href="http://sqlobject.org/SQLObject.html">documentação completa</a> disponibilizada online.

<strong>PSE</strong>
É um framework escrito em Python que permite a publicação de páginas na web. Necessita do <a href="http://www.apache.org/">Apache</a> e do <a href="http://www.modpython.org/">mod_python</a> instalados e configurados para funcionar.
Seu funcionamento é parecido com o <a href="http://smarty.php.net/">Framework SmartyTemplate</a>, feito para PHP. Mas ele vai muito além, pois nos permite: efetuar requisições de dados enviados por formulários (POST) e de QueryStrings (GET), a criação de Sessões e Cookies, a criação de tags customizadas (Custom Tags), a recuperação do IP do usuário, etc.

Maiores informações podem ser encontradas no <a href="http://nick.borko.org/pse/">site oficial</a> e no <a href="http://nick.borko.org/pse/manual/index.html">manual</a>.

<p>&nbsp;</p>

Após apresentar os ingredientes necessários para a utilização do Python no desenvolvimento web, mostrarei como instalar e configurar todos os ingredientes para podermos colocar a mão na massa.
Para este post não ficar muito extenso, publicarei a instalação e a configuração em um próximo post.
