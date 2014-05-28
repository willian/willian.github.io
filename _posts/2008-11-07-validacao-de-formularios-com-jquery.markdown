---
layout: post
title: Validação de Formulários com jQuery
categories:
- client-side
- desenvolvimento
- javascript
- jquery
tags:
- client-side
- formulários
- javascript
- jquery
- validação
status: publish
type: post
published: true
meta:
  _edit_last: '1'
---
Não é difícil fazer validações de formulários no lado do cliente usando JavaScript. E com <a href="http://jquery.com/" rel="external">jQuery</a> a brincadeira fica ainda mais fácil.

A primeira coisa a fazer é baixar o <a href="http://jquery.com/" rel="external">jQuery</a>: <a href="http://jqueryjs.googlecode.com/files/jquery-1.2.6.min.js" rel="external">http://jqueryjs.googlecode.com/files/jquery-1.2.6.min.js</a>
Renomei o arquivo para <strong>jquery.js</strong>.

Depois precisaremos baixar o <a href="http://bassistance.de/jquery-plugins/jquery-plugin-validation/" rel="external">plugin de validação</a>, feito em jQuery: <a href="http://jquery.bassistance.de/validate/jquery.validate.zip" rel="external">http://jquery.bassistance.de/validate/jquery.validate.zip</a>
Descompacte o zip. Utilizaremos apenas o arquivo <strong>jquery.validate.js</strong>.

Agora vamos ao código!

<h3>O Formulário</h3>
<pre class="html4strict"><code><span class="sc2"><span class="kw2">&lt;form</span> <span class="kw3">id</span>=<span class="st0">&quot;form-signup&quot;</span> <span class="kw3">action</span>=<span class="st0">&quot;#&quot;</span> <span class="kw3">method</span>=<span class="st0">&quot;post&quot;</span> <span class="kw3">accept-charset</span>=<span class="st0">&quot;utf-8&quot;</span><span class="kw2">&gt;</span></span>
    <span class="sc2"><span class="kw2">&lt;fieldset&gt;</span></span>
        <span class="sc2"><span class="kw2">&lt;legend&gt;</span></span>Formulário de Cadastro<span class="sc2"><span class="kw2">&lt;/legend&gt;</span></span>
        <span class="sc2"><span class="kw2">&lt;label&gt;</span></span>
            Nome:
            <span class="sc2"><span class="kw2">&lt;input</span> <span class="kw3">type</span>=<span class="st0">&quot;text&quot;</span> <span class="kw3">name</span>=<span class="st0">&quot;nome&quot;</span> /<span class="kw2">&gt;</span></span>
        <span class="sc2"><span class="kw2">&lt;/label&gt;</span></span>
        <span class="sc2"><span class="kw2">&lt;label&gt;</span></span>
            E-mail:
            <span class="sc2"><span class="kw2">&lt;input</span> <span class="kw3">type</span>=<span class="st0">&quot;text&quot;</span> <span class="kw3">name</span>=<span class="st0">&quot;email&quot;</span> /<span class="kw2">&gt;</span></span>
        <span class="sc2"><span class="kw2">&lt;/label&gt;</span></span>
        <span class="sc2"><span class="kw2">&lt;label&gt;</span></span>
            Sexo:
            <span class="sc2"><span class="kw2">&lt;select</span> <span class="kw3">name</span>=<span class="st0">&quot;sexo&quot;</span><span class="kw2">&gt;</span></span>
                <span class="sc2"><span class="kw2">&lt;option</span> <span class="kw3">value</span>=<span class="st0">&quot;&quot;</span><span class="kw2">&gt;</span></span>Selecione<span class="sc2"><span class="kw2">&lt;/option&gt;</span></span>
                <span class="sc2"><span class="kw2">&lt;option</span> <span class="kw3">value</span>=<span class="st0">&quot;F&quot;</span><span class="kw2">&gt;</span></span>Feminino<span class="sc2"><span class="kw2">&lt;/option&gt;</span></span>
                <span class="sc2"><span class="kw2">&lt;option</span> <span class="kw3">value</span>=<span class="st0">&quot;M&quot;</span><span class="kw2">&gt;</span></span>Masculino<span class="sc2"><span class="kw2">&lt;/option&gt;</span></span>
            <span class="sc2"><span class="kw2">&lt;/select&gt;</span></span>
        <span class="sc2"><span class="kw2">&lt;/label&gt;</span></span>
        <span class="sc2"><span class="kw2">&lt;input</span> <span class="kw3">type</span>=<span class="st0">&quot;submit&quot;</span> <span class="kw3">value</span>=<span class="st0">&quot;Cadastrar&quot;</span> /<span class="kw2">&gt;</span></span>
    <span class="sc2"><span class="kw2">&lt;/fieldset&gt;</span></span>
<span class="sc2"><span class="kw2">&lt;/form&gt;</span></span></code></pre>

<h3>A Validação JavaScript</h3>
<pre class="javascript"><code><span class="co1">// Inicia o validador ao carregar a página</span>
$<span class="br0">&#40;</span><span class="kw2">function</span><span class="br0">&#40;</span><span class="br0">&#41;</span> <span class="br0">&#123;</span>
    <span class="co1">// valida o formulário</span>
    $<span class="br0">&#40;</span><span class="st0">'#form-signup'</span><span class="br0">&#41;</span>.<span class="me1">validate</span><span class="br0">&#40;</span><span class="br0">&#123;</span>
        <span class="co1">// define regras para os campos</span>
        rules: <span class="br0">&#123;</span>
            nome: <span class="br0">&#123;</span>
                required: <span class="kw2">true</span>,
                minlength: <span class="nu0">2</span>
            <span class="br0">&#125;</span>,
            email: <span class="br0">&#123;</span>
                required: <span class="kw2">true</span>,
                email: <span class="kw2">true</span>
            <span class="br0">&#125;</span>,
            sexo: <span class="br0">&#123;</span>
                required: <span class="kw2">true</span>
            <span class="br0">&#125;</span>
        <span class="br0">&#125;</span>,
        <span class="co1">// define messages para cada campo</span>
        messages: <span class="br0">&#123;</span>
            nome: <span class="st0">&quot;Preencha o seu nome&quot;</span>,
            email: <span class="st0">&quot;Preencha seu e-mail de contato&quot;</span>,
            sexo: <span class="st0">&quot;Informe seu sexo&quot;</span>
        <span class="br0">&#125;</span>
    <span class="br0">&#125;</span><span class="br0">&#41;</span>;
<span class="br0">&#125;</span><span class="br0">&#41;</span>;</code></pre>

<a href="http://willianfernandes.com.br/demos/validacao_jquery/form.html">Veja o exemplo!</a>
