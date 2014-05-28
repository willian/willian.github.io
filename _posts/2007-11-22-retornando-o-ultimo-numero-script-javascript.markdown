---
layout: post
title: Retornando o último número (script JavaScript)
categories:
- desenvolvimento
- expressões regulares
- javascript
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
O DGmike publicou o post <a href="http://dgmike.wordpress.com/2007/11/21/retornando-o-ultimo-numero-script-php/">Retornando o último número (script PHP)</a>, o Elcio mostrou a visão dele em<a href="http://blog.elcio.com.br/retornando-o-ultimo-numero-script-python/"> Retornando o último número (script Python)</a> e resolvi fazer o mesmo em <a href="http://boo-box.com/link/aff:submarinoid/uid:255486/tags:javascript livros" class="bbli">JavaScript<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a>:

<pre class="javascript"><code><span class="kw2">function</span> ultimoNumero<span class="br0">&#40;</span>str<span class="br0">&#41;</span> <span class="br0">&#123;</span>
    <span class="kw1">return</span> str.<span class="me1">match</span><span class="br0">&#40;</span><span class="re0">/\d+/g</span><span class="br0">&#41;</span>.<span class="me1">pop</span><span class="br0">&#40;</span><span class="br0">&#41;</span>;
<span class="br0">&#125;</span></code></pre>

<strong>[UPDATE]</strong>

Uma simples correção para quando não for passado uma string e para quando a string for vazio ou não tiver números:
<pre class="javascript"><code><span class="kw2">function</span> ultimoNumero<span class="br0">&#40;</span>str<span class="br0">&#41;</span> <span class="br0">&#123;</span>
    <span class="kw1">try</span> <span class="br0">&#123;</span>
        <span class="kw1">return</span> str.<span class="me1">match</span><span class="br0">&#40;</span><span class="re0">/\d+/g</span><span class="br0">&#41;</span>.<span class="me1">pop</span><span class="br0">&#40;</span><span class="br0">&#41;</span>;
    <span class="br0">&#125;</span> <span class="kw1">catch</span><span class="br0">&#40;</span>e<span class="br0">&#41;</span> <span class="br0">&#123;</span>
        <span class="kw1">return</span> <span class="st0">''</span>;
    <span class="br0">&#125;</span>
<span class="br0">&#125;</span></code></pre>

Muito simples, não?
