---
layout: post
title: Desabilitando Asset Pipeline no Rails 3.1
categories:
- blog
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
---
Se você é como eu e não gostou do assets pipeline que vem habilitado nativamente no rails 3.1, saiba que você pode desabilitá-lo. Para isso, basta editar o arquivo <code>application.rb</code>:

<pre class="ruby"><code><span class="co1"># Enable the asset pipeline</span>
config.<span class="me1">assets</span>.<span class="me1">enabled</span> = <span class="kw2">false</span></code></pre>

Essa notícia não é nova, porém poucos sabem que ao desabilitar este recurso os arquivos <code>controller_name.js</code> e <code>controller_name.css</code> continuam sendo gerados no diretório <code>app/assets/</code>. Veja:

<pre class="bash"><code>$ rails g controller users
  create  app/controllers/users_controller.rb
  invoke  erb
  create    app/views/users
  invoke  rspec
  create    spec/controllers/users_controller_spec.rb
  invoke  helper
  create    app/helpers/users_helper.rb
  invoke    rspec
  create      spec/helpers/users_helper_spec.rb
  invoke  assets
  invoke    js
  create      app/assets/javascripts/users.js
  invoke    css
  create      app/assets/stylesheets/users.css</code></pre>

Para evitar que isso aconteça basta fazer a configuração abaixo também no arquivo <code>application.rb</code>:

<pre class="ruby"><code>config.<span class="me1">generators</span> <span class="kw1">do</span> |g|
  g.<span class="me1">assets</span> <span class="kw2">false</span>
<span class="kw1">end</span></code></pre>

Com isso ao rodar o generator de controller teremos:

<pre class="bash"><code>$ rails g controller users
  create  app/controllers/users_controller.rb
  invoke  erb
  create    app/views/users
  invoke  rspec
  create    spec/controllers/users_controller_spec.rb
  invoke  helper
  create    app/helpers/users_helper.rb
  invoke    rspec
  create      spec/helpers/users_helper_spec.rb</code></pre>

Fica então a dica.
