---
layout: post
title: Ambiente de desenvolvimento Ruby on Rails no Mac OS Snow Leopard
categories:
- desenvolvimento
- ruby
- vim
tags:
- desenvolvimento
- gvim
- macvim
- mvim
- rails
- ror
- ruby
- ruby on rails
- ruby1.9
- snow leopard
- textmate
- vim
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  bb-custom-tags: ruby on rails
---
Recentemente atualizei meu Mac para o <a href="http://sledge.boo-box.com/list/page/U25vdytMZW9wYXJkXyMjX2JveF8jI190YWdnaW5nLXRvb2wtd3BfIyNf-56" class="bbli">Snow Leopard<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a> e fui logo configurar meu ambiente de <a href="http://sledge.boo-box.com/list/page/ZGVzZW52b2x2aW1lbnRvXyMjX2JveF8jI190YWdnaW5nLXRvb2wtd3BfIyNf-60" class="bbli">desenvolvimento<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a>.

Como alguns já sabem, programo em <a href="http://sledge.boo-box.com/list/page/UHl0aG9uXyMjX2JveF8jI190YWdnaW5nLXRvb2wtd3BfIyNf-48" class="bbli">Python<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a>, mas atualmente estou afastado da linguagem, utilizando 100% <a href="http://sledge.boo-box.com/list/page/UmFpbHNfIyNfYm94XyMjX3RhZ2dpbmctdG9vbC13cF8jI18=-48" class="bbli">Rails<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a>.

Uma das coisas que aproveitei quando resolvi instalar o <a href="http://sledge.boo-box.com/list/page/U25vdytMZW9wYXJkXyMjX2JveF8jI190YWdnaW5nLXRvb2wtd3BfIyNf-56" class="bbli">Snow Leopard<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a> foi formatar todo o HD. Com o tempo fui acumulando alguns lixos, então juntei o útil com o agradável e fiz uma bela faxina.

Outra coisa: meu Vim estava todo bagunçado. Fiz uma cagada nele e estava difícil trabalhar com ele, então estava usando somente o <a href="http://sledge.boo-box.com/list/page/VGV4dE1hdGVfIyNfYm94XyMjX3RhZ2dpbmctdG9vbC13cF8jI18=-52" class="bbli">TextMate<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a>. Adoro o TextMate, é um baita editor, mas não é meu <a href="http://sledge.boo-box.com/list/page/ZWRpdG9yK1ZpbV8jI19ib3hfIyNfdGFnZ2luZy10b29sLXdwXyMjXw==-56" class="bbli">Vim<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a>. Com o Vim me sinto mais em casa e não sofro quando preciso programar em uma máquina que não seja meu <a href="http://sledge.boo-box.com/list/page/TWFjXyMjX2JveF8jI190YWdnaW5nLXRvb2wtd3BfIyNf-44" class="bbli">Mac<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a>, afinal, o Vim é free e roda até no <a href="http://sledge.boo-box.com/list/page/V2luZG93c18jI19ib3hfIyNfdGFnZ2luZy10b29sLXdwXyMjXw==-52" class="bbli">Windows<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a> (eca!).

Bom, vamos lá!

<h3>O Vim</h3>
Para facilitar sua vida, criei um <a href="http://github.com/willian/willvim">repositório</a> do meu Vim, todo configurado, pronto para uso.

Para instalá-lo, basta fazer o clone:
<code>
<pre>
$ git clone git://github.com/willian/willvim.git
</pre>
</code>

Entre no diretório criado pelo comando acima e execute o comando abaixo:
<code>
<pre>
$ chmod +x install.sh
$ ./install.sh
</pre>
</code>

Os comandos acima baixam os repositórios dos plugins e faz a instalação dos arquivos no seu diretório <code>$HOME/.vim</code>.

ATENÇÃO: Esses comandos não funcionarão no <a href="http://sledge.boo-box.com/list/page/V2luZG93c18jI19ib3hfIyNfdGFnZ2luZy10b29sLXdwXyMjXw==-52" class="bbli">Windows<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a>. Em breve configurarei isso.

<h4>MacVim</h4>
Gosto de usar o <a href="http://sledge.boo-box.com/list/page/TWFjVmltXyMjX2JveF8jI190YWdnaW5nLXRvb2wtd3BfIyNf-48" class="bbli">MacVim<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a> (ou o gVim quando estou no Linux), pois tem uma aparência melhor do que o Vim no terminal.

Entre na <a href="http://code.google.com/p/macvim/">página de download do MacVim</a> e baixe a versão mais nova. A versão <code>"stable"</code> até a data deste post é a <a href="http://macvim.googlecode.com/files/MacVim-7_2-stable-1_2.tbz">MacVim-7_2-stable-1_2.tbz</a>.

Se você está no <a href="http://sledge.boo-box.com/list/page/TGludXhfIyNfYm94XyMjX3RhZ2dpbmctdG9vbC13cF8jI18=-48" class="bbli">Linux<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a> e usa <a href="http://sledge.boo-box.com/list/page/VWJ1bnR1XyMjX2JveF8jI190YWdnaW5nLXRvb2wtd3BfIyNf-48" class="bbli">Ubuntu<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a>, basta rodar o comando abaixo:
<code>
<pre>
$ sudo apt-get install vim vim-gnome vim-full vim-python vim-rails vim-ruby
</pre>
</code>

Agora basta rodar o comando <code>mvim</code> ou <code>gvim</code> (caso você esteja no Linux) no terminal para abrir o Vim no modo gráfico.

<h3>Ruby on Rails</h3>
Tanto a linguagem quando o framework já estão instalados no seu Mac, mas precisamos atualizá-los. Na verdade, você pode apenas atualizar o <a href="http://sledge.boo-box.com/list/page/UnVieStvbitSYWlsc18jI19ib3hfIyNfdGFnZ2luZy10b29sLXdwXyMjXw==-60" class="bbli">Rails<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a>, e é exatamente isso que vou mostrar aqui.

<h4>Atualizando o RubyGems</h4>
<code>
<pre>
$ sudo gem install rubygems-update
</pre>
</code>

Esse comando instala a nova versão do <a href="http://sledge.boo-box.com/list/page/UnVieUdlbXNfIyNfYm94XyMjX3RhZ2dpbmctdG9vbC13cF8jI18=-52" class="bbli">RubyGems<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a>. Para verificar a versão instalada, rode o comando abaixo:
<code>
<pre>
$ gem -v
1.3.5
</pre>
</code>

Até a data deste post a versão mais nova é a 1.3.5.

<h4>Atualizando suas gems</h4>
<code>
<pre>
$ sudo gem update
</pre>
</code>

<h4>Atualizando o Ruby on Rails</h4>
Nesse ponto a versão do Rails já deve estar atualizada, mas caso não esteja, rode o comando abaixo:
<code>
<pre>
$ sudo gem install rails
</pre>
</code>

<h3>MySQL</h3>
Apesar de poder rodar o Rails com o <a href="http://sledge.boo-box.com/list/page/U1FMaXRlXyMjX2JveF8jI190YWdnaW5nLXRvb2wtd3BfIyNf-48" class="bbli">SQLite<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a>, gosto de usar o <a href="http://sledge.boo-box.com/list/page/TXlTUUxfIyNfYm94XyMjX3RhZ2dpbmctdG9vbC13cF8jI18=-48" class="bbli">MySQL<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a> no ambiente de desenvolvimento. Para isso, acesso a página de <a href="http://dev.mysql.com/downloads/">download do MySQL</a> e busque a versão mais nova. Na data de criação deste post a versão mais nova é a <code>MySQL 5.1</code>.

ATENÇÃO: Só fique atento à arquitetura escolhida. O <a href="http://sledge.boo-box.com/list/page/U25vdytMZW9wYXJkXyMjX2JveF8jI190YWdnaW5nLXRvb2wtd3BfIyNf-56" class="bbli">Snow Leopard<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a> roda com <a href="http://sledge.boo-box.com/list/page/NjRiaXRzXyMjX2JveF8jI190YWdnaW5nLXRvb2wtd3BfIyNf-48" class="bbli">64bits<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a>, então baixe a versão <code>x86_64</code>.

Feito isso, hora de instalar a gem do MySQL:
<code>
<pre>
$ sudo env ARCHFLAGS="-arch x86_64" gem install mysql -- --with-mysql-config=/usr/local/mysql/bin/mysql_config
</pre>
</code>

<h3>Testando tudo</h3>
Vamos criar um aplicação de teste para verificar se o Rails está rodando corretamente, incluindo o MySQL:
<code>
<pre>
$ rails blog -d mysql
$ cd blog/
$ script/generate scaffold Post title:string body:string
$ rake db:create
$ rake db:migrate
</pre>
</code>

Se não aparecer nenhuma mensagem de erro, os procedimentos acima foram executados corretamente e você agora tem um ambiente completo para desenvolver seus aplicativos com Rails.
