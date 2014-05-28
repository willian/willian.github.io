---
layout: post
title: Desenvolvimento Web com Python, SQLObject e PSE - Parte 5
categories:
- desenvolvimento
- internet
- python
- web
tags: []
status: draft
type: post
published: false
meta:
  _edit_last: '1'
---
Depois de mais uma longa pausa e um post da série exclusivo sobre como configurar o ambiente no Mac OS X (tive que fazê-lo já que migrei para o sistema operacional da maçã), volto com o andamento original da série do ponto de <a href="http://willianfernandes.com.br/desenvolvimento-web-com-python-sqlobject-e-pse-parte-3/">onde paramos</a>.

Até agora temos dois arquivos de include (cabecalho.pt e rodape.pt) e uma página (index.pt) que contém nosso formulário de login. Como não colocamos nenhuma action no formulário de login ao submetermos a página index.pt será chamada.

Então vamos criar um arquivo chamado <strong>index.py</strong> e recuperar os dados digitados no formulário de login.

<pre lang="python" line="1">
from pse.plugins import request

print request.form['email']
</pre>

O que fiz ali foi importar o modulo request que, além de outras funcionalidades, é responsável em retornar os dados recebidos em um formulário. Para isso ele armazena cada campo do formulário em um dicionário onde a chave é o nome do campo e o valor é o que foi digitado do campo.

Da mesma forma que fizemos com o e-mail faremos com a senha, mas como se trata de senha utilizaremos <a href="http://pt.wikipedia.org/wiki/Md5">MD5</a> para "esconder" a senha do usuário, buscando assim um pouco de segurança para nosso sistema.

<pre lang="python" line="1">
import md5 
from pse.plugins import request
       
if len(request.form):
    email = request.form['email']
    senha = md5.new(request.form['senha']).hexdigest()
                                                                                                                                                                                                                                            
    print 'email: %s<br />senha: %s' % (email, senha)
</pre>

