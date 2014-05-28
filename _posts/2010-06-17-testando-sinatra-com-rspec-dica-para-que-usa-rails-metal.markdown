---
layout: post
title: Testando Sinatra com RSpec (dica para quem usa Rails Metal)
categories:
- blog
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  _wp_old_slug: ''
---
Após ler o <a href="http://www.mouseoverstudio.com/blog/2010/06/16/testando-sinatra-com-rspec/">post do Diego Carrion</a> sobre como usar <a href="http://sledge.boo-box.com/list/page/cnVieStyYWlscytSU3BlY18jI19jbG91ZF8jI190YWdnaW5nLXRvb2wtd3BfIyNf-64" class="bbli">RSpec<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a> para testar uma aplicação <a href="http://www.sinatrarb.com/">Sinatra</a>, lembrei que tive um problema com os testes quando trouxe a aplicação feita em Sinatra para uma outra feita em <a href="http://sledge.boo-box.com/list/page/cnVieStSYWlsc18jI19jbG91ZF8jI190YWdnaW5nLXRvb2wtd3BfIyNf-56" class="bbli">Rails<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a> usando <a href="http://railscasts.com/episodes/150-rails-metal">Rails Metal</a>.

Vou usar o exemplo do Carrion para mostrar o que precisei mudar para os testes rodarem dentro do Rails Metal. Se no Sinatra usamos o <em>spec_helper.rb</em> assim:

<pre class="ruby"><code><span class="kw3">require</span> <span class="kw4">File</span>.<span class="me1">join</span><span class="br0">&#40;</span><span class="kw4">File</span>.<span class="me1">dirname</span><span class="br0">&#40;</span><span class="kw2">__FILE__</span><span class="br0">&#41;</span>, <span class="st0">'..'</span>, <span class="st0">'main.rb'</span><span class="br0">&#41;</span>
&nbsp;
<span class="kw3">require</span> <span class="st0">'spec'</span>
<span class="kw3">require</span> <span class="st0">'rack/test'</span>
&nbsp;
<span class="re2">Spec::Runner</span>.<span class="me1">configure</span> <span class="kw1">do</span> |conf|
  conf.<span class="kw1">include</span> <span class="re2">Rack::<span class="kw4">Test</span>::Methods</span>
<span class="kw1">end</span>
&nbsp;
<span class="kw1">def</span> app
  <span class="re2">Sinatra::Application</span>
<span class="kw1">end</span></code></pre>

No Rails Metal precisamos usar o arquivo <em>spec_helper.rb</em> normal, da forma como ele for gerado pelo RSpec.

A classe Api é um rails metal, mas nesse caso ela deve extender a classe <strong>Sinatra::Base</strong> (<strong>rails_root/app/metal/api.rb</strong>):

<pre class="rails"><code><span class="kw3">require</span> <span class="st0">'sinatra'</span>
&nbsp;
<span class="co1"># Allow the metal piece to run in isolation</span>
<span class="kw3">require</span><span class="br0">&#40;</span><span class="kw4">File</span>.<span class="me1">dirname</span><span class="br0">&#40;</span><span class="kw2">__FILE__</span><span class="br0">&#41;</span> + <span class="st0">'/../../config/environment'</span><span class="br0">&#41;</span> <span class="kw1">unless</span> <span class="kw1">defined</span>?<span class="br0">&#40;</span>Rails<span class="br0">&#41;</span>
&nbsp;
<span class="kw1">class</span> Api &lt; <span class="re2">Sinatra::Base</span>
  <span class="co1"># Code</span>
<span class="kw1">end</span></code></pre>

E no arquivo <em>api_spec.rb</em> definimos o método app assim:

<pre class="rails"><code><span class="kw3">require</span> <span class="st0">'spec_helper'</span>
&nbsp;
describe <span class="st0">&quot;Api&quot;</span> <span class="kw1">do</span>
  <span class="kw1">include</span> <span class="re2">Rack::<span class="kw4">Test</span>::Methods</span>
&nbsp;
  <span class="kw1">def</span> app
    Api.<span class="kw5">new</span>
  <span class="kw1">end</span>
&nbsp;
  <span class="co1"># code</span>
<span class="kw1">end</span></code></pre>

No exemplo acima precisei fazer <em>require 'rack/test'</em> no <em>spec_helper.rb</em>. Para isso, basta instalar a gem <a href="http://github.com/brynary/rack-test">rack-test</a>.

Como você pode ver, com uma simples mudança você pode usar Sinatra com Rails e fazer seus testes com RSpec.
