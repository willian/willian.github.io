---
layout: post
title: Desenvolvimento Web com Python, SQLObject e PSE - Parte 2
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
Continuando o <a href="http://willianfernandes.com.br/desenvolvimento-web-com-python-sqlobject-e-pse-parte-1/">post anterior</a>, vamos agora instalar e configurar nosso ambiente para começar o desenvolvimento com Python, SQLObject e PSE.

Vou assumir que você utiliza Ubuntu, ou qualquer outra distribuição Linux baseada no Debian. Caso você utilize outro Sistema Operacional, verifique na página oficial dos programas (<a href="http://willianfernandes.com.br/desenvolvimento-web-com-python-sqlobject-e-pse-parte-1/">veja no post anterior</a>) como instalar cada um deles.

O Elcio publicou um <a href="http://blog.elcio.com.br/instalando-o-pse-no-ubuntu-710-gutsy-gibbon/">post</a> explicando, detalhadamente, como instalar o <a href="http://www.apache.org/">apache2</a>, o <a href="http://www.modpython.org/">mod_python</a> e o <a href="http://nick.borko.org/pse/">PSE</a> na versão 7.10 do Ubuntu, incluindo uma correção necessária para essa versão do Ubuntu.

Após executar os passos descritos pelo Elcio, falta apenas instalar o <a href="http://sqlobject.org/">SQLObject</a>:

<code class="prettyprint">sudo apt-get install python-sqlobject</code>
<strong>[ATUALIZADO]</strong> Seguindo a dica do Elcio:
<code class="prettyprint">sudo apt-get install python-mysqldb python-setuptools<br />sudo easy_install sqlobject</code>

Tudo instalado e configurado? Ok, agora vamos entender um pouco o funcionamento do PSE para depois desenvolvermos algo funcional.

O PSE trabalha com arquivos na extensão <em>.pt</em>, então vamos fazer um teste criando um arquivo chamado <em>hello_world.pt</em> no diretório do apache (no Ubuntu esse diretório fica em /var/www):

<pre class="html4strict"><code><span class="sc2"><span class="kw2">&lt;</span>?=<span class="st0">&quot;Hello World&quot;</span>?<span class="kw2">&gt;</span></span></code></pre>

As tags <em>&lt;?</em> e <em>?&gt;</em> indicam a abertura e o fechamento de código Python e tags especiais do PSE, que veremos mais adiante.

Execute no navegador: <a href="http://localhost/hello_world.pt">http://localhost/hello_world.pt</a>.

Vamos alterar agora nosso arquivo para integrar código Python com o PSE gerado:

<h3>hello_world.pt</h3>
<pre class="html4strict"><code><span class="sc2"><span class="kw2">&lt;</span>?= msg ?<span class="kw2">&gt;</span></span></code></pre>

<h3>hello_world.py</h3>
<pre class="python"><code><span class="kw1">import</span> <span class="kw3">datetime</span>
msg = <span class="st0">&quot;Hello Word&lt;br&gt;Hoje é %s&quot;</span> % <span class="kw3">datetime</span>.<span class="me1">date</span>.<span class="me1">today</span><span class="br0">&#40;</span><span class="br0">&#41;</span>.<span class="me1">strftime</span><span class="br0">&#40;</span><span class="st0">&quot;%d/%m/%Y&quot;</span><span class="br0">&#41;</span></code></pre>

Execute novamente no navegador: <a href="http://localhost/hello_world.pt">http://localhost/hello_world.pt</a>.

Perceba que escrevemos código Python normalmente e que o arquivo <em>hello_world.pt</em> identificou a variável <em>msg</em> e escreveu seu conteúdo na tela. Isso acontece porque o PSE integra automaticamente arquivos que tenham o mesmo nome, ou seja, ele sempre executara <em>hello_world.py</em> junto com <em>hello_world.pt</em>.

No próximo post mostrarei como trabalhar com includes no PSE e formulários. Prometo que os próximos posts não demorarão tanto quanto este. ;)
