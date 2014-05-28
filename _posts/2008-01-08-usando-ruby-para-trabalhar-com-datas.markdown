---
layout: post
title: Usando Ruby para trabalhar com datas
categories:
- desenvolvimento
- linguagens
- php
- python
- ruby
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
---
Foi publicado como <a href="http://d3rf.wordpress.com/2008/01/08/converter-formato-de-data-do-mysql-para-o-formato-br-em-uma-linha-de-codigo-so/">"Converter formato de data do MySQL para o formato BR, em uma linha de código só"</a> usando <a href="http://boo-box.com/link/aff:submarinoid/uid:255486/tags:PHP+livro+linguagem" class="bbli">PHP<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a>, o <a href="http://dgmike.wordpress.com/2008/01/08/reformatando-as-datas-em-python/">DGMike mostrou como ficaria sua versão em</a> <a href="http://boo-box.com/link/aff:submarinoid/uid:255486/tags:Python+livro+linguagem" class="bbli">Python<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a>, eu até <a href="http://dgmike.wordpress.com/2008/01/08/reformatando-as-datas-em-python/#comment-4068">fiz minha contribuição lá mostrando como eu faria em Python usando um objeto datetime</a> e agora resolvi fazer o mesmo em <a href="http://boo-box.com/link/aff:submarinoid/uid:255486/tags:Ruby+livro+linguagem" class="bbli">Ruby<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a>, já que estou estudando essa linguagem:

<pre class="ruby"><code>data = <span class="st0">'2008-08-12'</span>
td = <span class="br0">&#91;</span><span class="br0">&#93;</span>
data.<span class="kw3">split</span><span class="br0">&#40;</span><span class="st0">'-'</span><span class="br0">&#41;</span>.<span class="me1">each</span><span class="br0">&#123;</span> |d| td &lt;&lt; d.<span class="me1">to_i</span><span class="br0">&#125;</span>
d = <span class="kw4">DateTime</span>.<span class="me1">new</span><span class="br0">&#40;</span>td<span class="br0">&#91;</span><span class="nu0">0</span><span class="br0">&#93;</span>, td<span class="br0">&#91;</span><span class="nu0">1</span><span class="br0">&#93;</span>, td<span class="br0">&#91;</span><span class="nu0">2</span><span class="br0">&#93;</span><span class="br0">&#41;</span>
ndata = d.<span class="me1">strftime</span><span class="br0">&#40;</span><span class="st0">'%d/%m/%Y'</span><span class="br0">&#41;</span></code></pre>

<strong>[ATUALIZADO]</strong>
Respondendo a pergunta do d3rf e aproveitando a dica do Caio Moritz:
<pre class="ruby"><code><span class="st0">'2008-08-12'</span>.<span class="kw3">split</span><span class="br0">&#40;</span><span class="st0">'-'</span><span class="br0">&#41;</span>.<span class="me1">reverse</span>.<span class="me1">join</span><span class="br0">&#40;</span><span class="st0">'/'</span><span class="br0">&#41;</span></code></pre>

Aguarde, em breve voltarei com o desenvolvimento em Python com PSE e SQLObject!!!
