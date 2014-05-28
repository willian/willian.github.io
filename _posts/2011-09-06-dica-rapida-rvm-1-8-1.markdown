---
layout: post
title: 'Dica rápida: RVM 1.8.1'
categories:
- desenvolvimento
- mac
- ruby
tags:
- desenvolvimento
- mac
- ruby
- rvm
status: publish
type: post
published: true
meta:
  _edit_last: '1'
---
<a href="https://github.com/wayneeseguin/rvm/issues/403">Pelo o que parece</a>, a versão atual (1.8.1) do <a href="https://rvm.beginrescueend.com/">RVM</a> não está funcionando para usuários Mac.

Se você tentar instalar qualquer versão do ruby com essa versão do RVM terá o erro:

<code>Trying http:// URL instead.
curl: (3) malformed</code>

Para funcionar corretamente tive que instalar a versão anterior, a 1.8.0:

<code>curl -s https://rvm.beginrescueend.com/install/rvm -o rvm-installer ; chmod +x rvm-installer ; ./rvm-installer --version 1.8.0</code>

Agora é esperar que eles lancem a correção na versão 1.8.2 para que os usuários Mac possam atualizar o RVM.

#fikdik
