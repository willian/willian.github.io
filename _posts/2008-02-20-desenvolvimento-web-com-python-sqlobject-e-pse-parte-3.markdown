---
layout: post
title: Desenvolvimento Web com Python, SQLObject e PSE - Parte 3
categories:
- desenvolvimento
- internet
- python
- web
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
---
<p>Continuando com a série sobre <a href="http://boo-box.com/link/aff:submarinoid/uid:255486/tags:desenvolvimento+web" class="bbli">desenvolvimento web<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a> com <a href="http://boo-box.com/link/aff:submarinoid/uid:255486/tags:livro+programação+python" class="bbli">Python<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a>, vou mostrar agora como deixar as coisa mais interessante com includes e formulários.</p>

<h3>Includes</h3>
<p>É muito comum utilizar arquivos separados que estarão em várias partes da aplicação. Por exemplo, podemos ter um arquivo para o cabeçalho <a href="http://boo-box.com/link/aff:submarinoid/uid:255486/tags:livro+html" class="bbli">HTML<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a>, um outro para o menu e um terceiro para o rodapé do <a href="http://boo-box.com/link/aff:submarinoid/uid:255486/tags:livro+html" class="bbli">HTML<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a>.</p>

<p>Mas antes de criarmos nossos arquivos de include, teremos que configurar o PSE para apontar para nosso diretório de includes. Para isso abra o arquivo <strong>pse.conf</strong> (no Linux este arquivo fica em <strong>/etc/pse/pse.conf</strong>). Procure pela linha</p>
<pre class="ini"><code><span class="co0">;IncludePath = /app/servlet/path,/other/servlet/path</span></code></pre>

<p>E troque por:</p>

<pre class="ini"><code><span class="re1">IncludePath </span>=<span class="re2"> /var/www/includes,.</span></code></pre>

<p>Caso você não esteja usando <a href="http://boo-box.com/link/aff:submarinoid/uid:255486/tags:Linux" class="bbli">Linux<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a> (eu uso o <a href="http://boo-box.com/link/aff:submarinoid/uid:255486/tags:Ubuntu" class="bbli">Ubuntu<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a>) configure para o diretório que o Apache aponta. Isso muda de sistema para sistema.<br />Dentro deste diretório crie um sub-diretório chamado <strong>includes</strong> e dentro deste sub-diretório vamos colocar os arquivos abaixo:</p>

<h3>cabecalho.pt</h3>
<pre class="html4strict"><code><span class="sc0">&lt;!DOCTYPE html PUBLIC &quot;-//W3C//DTD XHTML 1.0 Strict//EN&quot;</span>
<span class="sc0">    &quot;http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd&quot;&gt;</span>
<span class="sc2"><span class="kw2">&lt;html</span> xmlns=<span class="st0">&quot;http://www.w3.org/1999/xhtml&quot;</span> <span class="kw3">dir</span>=<span class="st0">&quot;ltr&quot;</span> <span class="kw3">lang</span>=<span class="st0">&quot;pt-BR&quot;</span><span class="kw2">&gt;</span></span>
<span class="sc2"><span class="kw2">&lt;head&gt;</span></span>
    <span class="sc2"><span class="kw2">&lt;meta</span> <span class="kw3">http-equiv</span>=<span class="st0">&quot;Content-Type&quot;</span> <span class="kw3">content</span>=<span class="st0">&quot;text/html; charset=UTF-8&quot;</span> /<span class="kw2">&gt;</span></span>
    <span class="sc2"><span class="kw2">&lt;title&gt;</span></span>Biblioteca ABC<span class="sc2"><span class="kw2">&lt;/title&gt;</span></span>
    <span class="sc2"><span class="kw2">&lt;meta</span> <span class="kw3">http-equiv</span>=<span class="st0">&quot;Content-Type&quot;</span> <span class="kw3">content</span>=<span class="st0">&quot;text/html; charset=utf-8&quot;</span> /<span class="kw2">&gt;</span></span>
    <span class="sc2"><span class="kw2">&lt;meta</span> <span class="kw3">name</span>=<span class="st0">&quot;language&quot;</span> <span class="kw3">content</span>=<span class="st0">&quot;pt-br&quot;</span> /<span class="kw2">&gt;</span></span>
<span class="sc2"><span class="kw2">&lt;/head&gt;</span></span>
<span class="sc2"><span class="kw2">&lt;body&gt;</span></span>
    <span class="sc2"><span class="kw2">&lt;div</span> <span class="kw3">id</span>=<span class="st0">&quot;geral&quot;</span><span class="kw2">&gt;</span></span>
        <span class="sc2"><span class="kw2">&lt;div</span> <span class="kw3">id</span>=<span class="st0">&quot;topo&quot;</span><span class="kw2">&gt;</span></span>
            <span class="sc2"><span class="kw2">&lt;h1&gt;</span></span>Biblioteca ABC<span class="sc2"><span class="kw2">&lt;/h1&gt;</span></span>
        <span class="sc2"><span class="kw2">&lt;/div&gt;</span></span>
        <span class="sc2"><span class="kw2">&lt;div</span> <span class="kw3">id</span>=<span class="st0">&quot;menu&quot;</span><span class="kw2">&gt;</span></span>
            <span class="sc2"><span class="kw2">&lt;ul&gt;</span></span>
                <span class="sc2"><span class="kw2">&lt;li</span> <span class="kw3">class</span>=<span class="st0">&quot;primeiro&quot;</span><span class="kw2">&gt;</span></span><span class="sc2"><span class="kw2">&lt;a</span> <span class="kw3">href</span>=<span class="st0">&quot;home.pt&quot;</span><span class="kw2">&gt;</span></span>Home<span class="sc2"><span class="kw2">&lt;/a&gt;</span></span><span class="sc2"><span class="kw2">&lt;/li&gt;</span></span>
                <span class="sc2"><span class="kw2">&lt;li&gt;</span></span><span class="sc2"><span class="kw2">&lt;a</span> <span class="kw3">href</span>=<span class="st0">&quot;categorias_list.pt&quot;</span><span class="kw2">&gt;</span></span>Categorias<span class="sc2"><span class="kw2">&lt;/a&gt;</span></span><span class="sc2"><span class="kw2">&lt;/li&gt;</span></span>
                <span class="sc2"><span class="kw2">&lt;li&gt;</span></span><span class="sc2"><span class="kw2">&lt;a</span> <span class="kw3">href</span>=<span class="st0">&quot;livros_list.pt&quot;</span><span class="kw2">&gt;</span></span>Livros<span class="sc2"><span class="kw2">&lt;/a&gt;</span></span><span class="sc2"><span class="kw2">&lt;/li&gt;</span></span>
                <span class="sc2"><span class="kw2">&lt;li&gt;</span></span><span class="sc2"><span class="kw2">&lt;a</span> <span class="kw3">href</span>=<span class="st0">&quot;clientes_list.pt&quot;</span><span class="kw2">&gt;</span></span>Clientes<span class="sc2"><span class="kw2">&lt;/a&gt;</span></span><span class="sc2"><span class="kw2">&lt;/li&gt;</span></span>
                <span class="sc2"><span class="kw2">&lt;li</span> <span class="kw3">class</span>=<span class="st0">&quot;ultimo&quot;</span><span class="kw2">&gt;</span></span><span class="sc2"><span class="kw2">&lt;a</span> <span class="kw3">href</span>=<span class="st0">&quot;sair.pt&quot;</span><span class="kw2">&gt;</span></span>Sair<span class="sc2"><span class="kw2">&lt;/a&gt;</span></span><span class="sc2"><span class="kw2">&lt;/li&gt;</span></span>
            <span class="sc2"><span class="kw2">&lt;/ul&gt;</span></span>
        <span class="sc2"><span class="kw2">&lt;/div&gt;</span></span></code></pre>

<h3>rodape.pt</h3>
<pre class="html4strict"><code>        <span class="sc2"><span class="kw2">&lt;address</span> <span class="kw3">class</span>=<span class="st0">&quot;rodape&quot;</span><span class="kw2">&gt;</span></span>
            <span class="sc1">&amp;copy;</span> Biblioteca ABC
        <span class="sc2"><span class="kw2">&lt;/address&gt;</span></span>
    <span class="sc2"><span class="kw2">&lt;/div&gt;</span></span>
<span class="sc2"><span class="kw2">&lt;/body&gt;</span></span>
<span class="sc2"><span class="kw2">&lt;/html&gt;</span></span></code></pre>

<p>Ok, os arquivos estão criados!<br />
Agora vamos criar o arquivo principal do nosso sistema. Este arquivo terá um formulário de login, porém ele fará include do cabeçalho e do rodapé.<br />Salve o arquivo abaixo na raiz de onde ficará a sua aplicação, ou seja, em um diretório acima do sub-diretório <strong>includes</strong>.</p>

<h3>index.pt</h3>
<pre class="html4strict"><code><span class="sc2"><span class="kw2">&lt;</span>?= pse.include<span class="br0">&#40;</span><span class="st0">&quot;cabecalho.pt&quot;</span><span class="br0">&#41;</span> ?<span class="kw2">&gt;</span></span>
<span class="sc2"><span class="kw2">&lt;form</span> <span class="kw3">id</span>=<span class="st0">&quot;frm-login&quot;</span> <span class="kw3">method</span>=<span class="st0">&quot;post&quot;</span> <span class="kw3">action</span>=<span class="st0">&quot;&quot;</span><span class="kw2">&gt;</span></span>
    <span class="sc2"><span class="kw2">&lt;fieldset&gt;</span></span>
        <span class="sc2"><span class="kw2">&lt;legend&gt;</span></span>Logar no Sistema<span class="sc2"><span class="kw2">&lt;/legend&gt;</span></span>
        <span class="sc2"><span class="kw2">&lt;label&gt;</span></span>E-mail: <span class="sc2"><span class="kw2">&lt;input</span> <span class="kw3">type</span>=<span class="st0">&quot;text&quot;</span> <span class="kw3">id</span>=<span class="st0">&quot;email&quot;</span> <span class="kw3">name</span>=<span class="st0">&quot;email&quot;</span> /<span class="kw2">&gt;</span></span><span class="sc2"><span class="kw2">&lt;/label&gt;</span></span>
        <span class="sc2"><span class="kw2">&lt;label&gt;</span></span>Senha: <span class="sc2"><span class="kw2">&lt;input</span> <span class="kw3">type</span>=<span class="st0">&quot;password&quot;</span> <span class="kw3">id</span>=<span class="st0">&quot;senha&quot;</span> <span class="kw3">name</span>=<span class="st0">&quot;senha&quot;</span> /<span class="kw2">&gt;</span></span><span class="sc2"><span class="kw2">&lt;/label&gt;</span></span>
        <span class="sc2"><span class="kw2">&lt;input</span> <span class="kw3">type</span>=<span class="st0">&quot;submit&quot;</span> <span class="kw3">id</span>=<span class="st0">&quot;entrar&quot;</span> <span class="kw3">name</span>=<span class="st0">&quot;entrar&quot;</span> <span class="kw3">value</span>=<span class="st0">&quot;Entrar&quot;</span> <span class="kw3">class</span>=<span class="st0">&quot;botao&quot;</span> /<span class="kw2">&gt;</span></span>
    <span class="sc2"><span class="kw2">&lt;/fieldset&gt;</span></span>
<span class="sc2"><span class="kw2">&lt;/form&gt;</span></span>
<span class="sc2"><span class="kw2">&lt;</span>?= pse.include<span class="br0">&#40;</span><span class="st0">&quot;rodape.pt&quot;</span><span class="br0">&#41;</span> ?<span class="kw2">&gt;</span></span>
&nbsp;</code></pre>

<p>Perceberam o quanto é simples?<br />
Toda página PSE possui um objeto chamado <strong>pse</strong> que contém vários métodos e objetos e no exemplo acima utilizamos o método <strong>include</strong>. Mais para frente mostrarei outras funcionalidades do objeto <strong>pse</strong>.</p>

<p>O método <strong>include</strong> recebe como parâmetro o nome do arquivo que iremos incluir. O PSE procura este arquivo nos diretórios que configuramos no arquivo <strong>pse.conf</strong>.</p>

<p>Para não prolongar muito, explicarei como trabalhar com formulários utilizando PSE no próximo post.</p>

<p>Prometo não demorar muito para postar o próximo post da série e aproveito para pedir o feedback de vocês em relação à esta série.</p>
