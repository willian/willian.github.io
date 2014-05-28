---
layout: post
title: Faye - Como eu criei um simples chat usando Rails
categories:
- blog
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
---
Recentemente precisei criar um chat para integrar com a aplicação da empresa que trabalho. Sim, mais um desenvolvimento de chat. Como dizem por ai, chat é o novo Hello World.

Já tinha ouvido falar do <a href="http://faye.jcoglan.com/">Faye</a>, até o Ryan Bates fez um <a href="http://railscasts.com/episodes/260-messaging-with-faye">Railscasts sobre o assunto</a>.

O Faye tem módulos para Ruby e Node.js.

Minha primeira tentativa foi utilizar a <a href="http://faye.jcoglan.com/ruby.html">versão ruby do Faye</a>. Essa versão nada mais é que uma aplicação Rack. Funcionou muito bem, até chegar em produção. O servidor que ele utiliza é o thin, e para a quantidade de requests que minha aplicação faz ao chat o servidor não durava 3 minutos em pé.

Depois de muito quebrar a cabeça resolvi partir para a <a href="http://faye.jcoglan.com/node.html">versão em Node.js do Faye</a> que resolveu perfeitamente esse problema. Vou mostrar abaixo como fiz para utilizando Faye, Node.js e Rails:

<h2>Vamos ao código</h2>

Primeiro você precisa ter o <a href="http://nodejs.org">Node.js</a> e o <a href="http://npmjs.org">NPM</a> instalados.

Na raiz da aplicação, instale o faye utilizando o npm:
<pre class="bash"><code>$ npm install faye</code></pre>

Logo em seguida, também na raiz da aplicação, criei o arquivo abaixo:
<strong>faye_server.js</strong>
<pre class="javascript"><code><span class="kw2">var</span> http = require<span class="br0">&#40;</span><span class="st0">'http'</span><span class="br0">&#41;</span>
  , faye = require<span class="br0">&#40;</span><span class="st0">'faye'</span><span class="br0">&#41;</span>;
&nbsp;
<span class="kw2">var</span> Logger = <span class="br0">&#123;</span>
	incoming: <span class="kw2">function</span><span class="br0">&#40;</span>message, callback<span class="br0">&#41;</span> <span class="br0">&#123;</span>
		console.<span class="me1">log</span><span class="br0">&#40;</span>message<span class="br0">&#41;</span>;
		console.<span class="me1">log</span><span class="br0">&#40;</span><span class="st0">'===================='</span><span class="br0">&#41;</span>;
&nbsp;
		callback<span class="br0">&#40;</span>message<span class="br0">&#41;</span>;
	<span class="br0">&#125;</span>
<span class="br0">&#125;</span>;
&nbsp;
<span class="kw2">var</span> bayeux = <span class="kw2">new</span> faye.<span class="me1">NodeAdapter</span><span class="br0">&#40;</span><span class="br0">&#123;</span>mount: <span class="st0">'/faye'</span>, timeout: <span class="nu0">60</span><span class="br0">&#125;</span><span class="br0">&#41;</span>;
bayeux.<span class="me1">addExtension</span><span class="br0">&#40;</span>Logger<span class="br0">&#41;</span>;
bayeux.<span class="me1">listen</span><span class="br0">&#40;</span><span class="nu0">9292</span><span class="br0">&#41;</span>;
&nbsp;</code></pre>

Para testar se o faye está corretamente instalado e funcionando, rode o servidor:
<pre class="bash"><code>$ node faye_server.js</code></pre>

E abra no seu nevegador a URL <a href="http://localhost:9292/faye.js">http://localhost:9292/faye.js</a>. Se um arquivo JavaScript for carregar, então o Faye está funcionando corretamente. #WIN

<h2>Client-side</h2>

No seu arquivo de layouts (ex.: application.html.erb) você precisa adicionar o JavaScript do Faye:
<pre class="html4strict"><code><span class="sc2">&lt;%= javascript_include_tag <span class="st0">&quot;http://localhost:9292/faye.js&quot;</span> %<span class="kw2">&gt;</span></span></code></pre>

Agora basta criar uma instância para o Client do Faye e o canal que receberá as mensagens do nosso chat:
<strong>application.js</strong>
<pre class="javascript"><code>$<span class="br0">&#40;</span><span class="kw2">function</span><span class="br0">&#40;</span><span class="br0">&#41;</span> <span class="br0">&#123;</span>
	<span class="kw2">var</span> faye_client = <span class="kw2">new</span> Faye.<span class="me1">Client</span><span class="br0">&#40;</span><span class="st0">'http://localhost:9292/faye'</span><span class="br0">&#41;</span>;
	faye_client.<span class="me1">subscribe</span><span class="br0">&#40;</span><span class="st0">'/chat'</span> , <span class="kw2">function</span><span class="br0">&#40;</span>data<span class="br0">&#41;</span> <span class="br0">&#123;</span>
		<span class="kw1">eval</span><span class="br0">&#40;</span>data<span class="br0">&#41;</span>;
	<span class="br0">&#125;</span><span class="br0">&#41;</span>;
<span class="br0">&#125;</span><span class="br0">&#41;</span>;
&nbsp;</code></pre>

<h2>Back-end</h2>

Criei um simples formulário que faz um POST para MessagesController::create utilizando AJAX:
<strong>app/views/messages/index.html.erb</strong>
<pre class="rails"><code>&lt;h1&gt;Messages&lt;/h1&gt;
&nbsp;
&lt;div id=<span class="st0">&quot;messages&quot;</span>&gt;
	&lt;ol&gt;&lt;/ol&gt;
&lt;/div&gt;
&nbsp;
&lt;%= <span class="kw5">form_for</span> <span class="re1">@message</span>, remote: <span class="kw2">true</span> <span class="kw1">do</span> |f| %&gt;
	&lt;%= f.<span class="me1">label</span> <span class="re3">:content</span> %&gt;
	&lt;%= f.<span class="kw5">text_field</span> <span class="re3">:content</span> %&gt;
	&lt;%= f.<span class="me1">submit</span> <span class="st0">&quot;Send&quot;</span> %&gt;
&lt;% <span class="kw1">end</span> %&gt;
&nbsp;</code></pre>

E no controller MessagesController:
<pre class="rails"><code><span class="kw1">class</span> MessagesController &lt; ApplicationController
  <span class="kw1">def</span> index
    <span class="re1">@message</span> = Message.<span class="kw5">new</span>
  <span class="kw1">end</span>
&nbsp;
  <span class="kw1">def</span> create
    <span class="re1">@message</span> = Message.<span class="kw5">create</span><span class="br0">&#40;</span>params<span class="br0">&#91;</span><span class="re3">:message</span><span class="br0">&#93;</span><span class="br0">&#41;</span>
  <span class="kw1">end</span>
<span class="kw1">end</span>
&nbsp;</code></pre>

Simples, certo?

O segredo está na view <code>app/views/messages/create.js.erb</code>:
<pre class="rails"><code>&lt;% broadcast <span class="st0">&quot;/chat&quot;</span> <span class="kw1">do</span> %&gt;
	$<span class="br0">&#40;</span><span class="st0">&quot;#messages ol&quot;</span><span class="br0">&#41;</span>.<span class="me1">append</span><span class="br0">&#40;</span>$<span class="br0">&#40;</span><span class="st0">&quot;&lt;li&gt;&lt;%= @message.content %&gt;&lt;/li&gt;&quot;</span><span class="br0">&#41;</span><span class="br0">&#41;</span>;
&lt;% <span class="kw1">end</span> %&gt;
$<span class="br0">&#40;</span><span class="st0">&quot;#message_content&quot;</span><span class="br0">&#41;</span>.<span class="me1">val</span><span class="br0">&#40;</span><span class="st0">''</span><span class="br0">&#41;</span>;
&nbsp;</code></pre>

Seguindo a dica do Ryan Bates, criei um helper para facilitar o envio das mensagens para o Faye Server. Ele será responsável em fazer o broadcast para todos os usuários conectados no chat.

<code>app/helpers/messages_helper.rb</code>
<pre class="rails"><code><span class="kw1">module</span> MessagesHelper
  <span class="kw1">def</span> broadcast<span class="br0">&#40;</span>channel, &amp;block<span class="br0">&#41;</span>
    message = <span class="br0">&#123;</span> channel: channel, data: capture<span class="br0">&#40;</span>&amp;block<span class="br0">&#41;</span> <span class="br0">&#125;</span>
    uri     = <span class="kw4">URI</span>.<span class="me1">parse</span><span class="br0">&#40;</span><span class="st0">&quot;http://localhost:9292/faye&quot;</span><span class="br0">&#41;</span>
    <span class="re2">Net::HTTP</span>.<span class="me1">post_form</span><span class="br0">&#40;</span>uri, message: message.<span class="me1">to_json</span><span class="br0">&#41;</span>
  <span class="kw1">end</span>
<span class="kw1">end</span>
&nbsp;</code></pre>

Como este helper está usando o <code>Net::HTTP</code>, precisamos adicioná-lo na nossa aplicação. Eu normalmente faço o <code>require</code> dessa lib no arquivo <code>config/application.rb</code>:
<pre class="rails"><code><span class="co1"># ...</span>
&nbsp;
<span class="kw3">require</span> <span class="st0">'rails/all'</span>
<span class="kw3">require</span> <span class="st0">'net/http'</span>
&nbsp;
<span class="co1"># ...</span></code></pre>

Com isso nosso chat está pronto!

Lógico que na minha aplicação existem processos um pouco mais complexos, lidando com chat privado (estilo Facebook) e autenticação de usuários. Mas para exemplo, esse caso mais simples vale.

Você pode baixar a aplicação completa diretamente do meu GitHub:
<a href="https://github.com/willian/faye_chat_example">https://github.com/willian/faye_chat_example</a>

Fácil, não!? :)
