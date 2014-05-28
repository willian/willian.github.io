---
layout: post
title: Como gerar validações client-side em projetos Rails usando jQuery Validator
  com ClientValidations
categories:
- client-side
- desenvolvimento
- javascript
- jquery
- rails
tags:
- client_validations
- jquery
- rails
status: publish
type: post
published: true
meta:
  _edit_last: '1'
---
Estou fazendo uma nova aplicação aqui na empresa e teremos muitos formulários. Para não precisar criar um script de validação para cada formulário, fui atrás de um plugin que gerasse as validação JavaScript automáticamente, com base nas validações do modelo.

Sem maiores problemas, encontrei o plugin <a href="http://github.com/augustl/live-validations/">Live Validations</a>. Ele faz tudo o que preciso, quer dizer, quase tudo. :(

Alguns dos formulários dessa aplicação são <a href="http://railscasts.com/episodes/196-nested-model-form-part-1">Nested Model Form</a> e o <em>Live Validations</em> não suporta esse tipo de formulário.

Sendo assim, resolvi fazer meu próprio plugin, chamado <a href="http://github.com/willian/client_validations">Client Validations</a>. O que ele faz é basicamente ler as validações definidas no <em>Model</em> e traduzi-las para JavaScript usando <a href="http://willianfernandes.com.br/validacao-de-formularios-com-jquery/">jQuery Validator</a>.

<h3>Instalação</h3>
<pre class="bash"><code>script/plugin install git://github.com/willian/client_validations.git</code></pre>

Como o <strong><em>Client Validations</em></strong> depende do plugin <strong><em>Validation Reflection</em></strong>, preciaremos instalar ele também:
<pre class="bash"><code>script/plugin install git://github.com/redinger/validation_reflection.git</code></pre>

E por último basta instalar o jQuery e o jQuery Validator:

<ul>
	<li><a href="http://code.jquery.com/jquery-latest.min.js">http://code.jquery.com/jquery-latest.min.js</a></li>
	<li><a href="http://ajax.microsoft.com/ajax/jquery.validate/1.6/jquery.validate.min.js">http://ajax.microsoft.com/ajax/jquery.validate/1.6/jquery.validate.min.js</a></li>
</ul>


Não esqueça de carregar o jquery e o validator no seu HTML:
<pre class="rails"><code>&lt;%= <span class="kw5">javascript_include_tag</span> <span class="st0">'jquery-latest.min.js'</span>, <span class="st0">'jquery.validate.min.js'</span> %&gt;</code></pre>

Supondo que temos o modelo abaixo:
<pre class="rails"><code><span class="kw1">class</span> Task &lt; <span class="re2">ActiveRecord::Base</span>
  <span class="kw5">validates_presence_of</span> <span class="re3">:name</span>
<span class="kw1">end</span>
&nbsp;</code></pre>

E o formulário desse modelo:
<pre class="rails"><code>&lt;% <span class="kw5">form_for</span><span class="br0">&#40;</span>@task<span class="br0">&#41;</span> <span class="kw1">do</span> |f| %&gt;
  &lt;%= f.<span class="me1">error_messages</span> %&gt;
&nbsp;
  &lt;p&gt;
    &lt;%= f.<span class="me1">label</span> <span class="re3">:name</span> %&gt;&lt;br /&gt;
    &lt;%= f.<span class="kw5">text_field</span> <span class="re3">:name</span> %&gt;
  &lt;/p&gt;
  &lt;p&gt;
    &lt;%= f.<span class="me1">submit</span> <span class="st0">'Create'</span> %&gt;
  &lt;/p&gt;
&lt;% <span class="kw1">end</span> %&gt;</code></pre>

Tudo o que precisamos fazer para a validação client-side funcionar é adicionar o helper <strong><em>client_validations</em></strong> no formulário. Ficará assim:
<pre class="rails"><code>&lt;% <span class="kw5">form_for</span><span class="br0">&#40;</span>@task<span class="br0">&#41;</span> <span class="kw1">do</span> |f| %&gt;
  &lt;%= f.<span class="me1">error_messages</span> %&gt;
&nbsp;
  &lt;p&gt;
    &lt;%= f.<span class="me1">label</span> <span class="re3">:name</span> %&gt;&lt;br /&gt;
    &lt;%= f.<span class="kw5">text_field</span> <span class="re3">:name</span> %&gt;
  &lt;/p&gt;
  &lt;p&gt;
    &lt;%= f.<span class="me1">submit</span> <span class="st0">'Create'</span> %&gt;
  &lt;/p&gt;
  &lt;%= f.<span class="me1">client_validations</span> %&gt;
&lt;% <span class="kw1">end</span> %&gt;</code></pre>

Provavelmente você receberá a seguinte mensagem de validação:
<pre><code>translation missing: en, activerecord, attributes, task, name can't be blank</code></pre>

Para resolver esse problema, basta criar o arquivo de internacionalização em config/locales.

O plugin ainda está na versão 0.1.0 e muita coisa pode ser feita para melhorá-lo. Se tiver alguma sugestão, crie um comentário ou use a página do GitHub: <a href="http://github.com/willian/client_validations">http://github.com/willian/client_validations</a>
