---
layout: post
title: Desenvolvimento Web com Python, SQLObject e PSE - Parte 4
categories:
- desenvolvimento
- internet
- python
- web
tags: []
status: publish
type: post
published: true
meta:
  _edit_last: '1'
---
Depois de mais uma longa pausa na série de desenvolvimento web com <a href="http://boo-box.com/link/aff:buscapeid/uid:4781/tags:python+livro" class="bbli">python<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a> cá estou, de volta com os posts.

Mas desta vez a pausa foi por um motivo nobre. Recentemente adquiri um <a href="http://boo-box.com/link/aff:buscapeid/uid:4781/tags:Apple+Mac" class="bbli">MacBook<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a> e logo resolvi configurar o <a href="http://boo-box.com/link/aff:buscapeid/uid:4781/tags:servidor+Apache+livro" class="bbli">Apache2<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a> + <a href="http://www.modpython.org/">mod_python</a> + <a href="http://nick.borko.org/pse/">PSE</a> + <a href="http://www.sqlobject.org/">SQLObject</a> + <a href="http://mysql-python.sourceforge.net/">MySQL-python (MySQLdb)</a>. Precisava desta configuração para dar continuidade à série.

Então resolvi dedicar a 4ª parte da série exclusivamente para mostrar como configurar o ambiente no <a href="http://boo-box.com/link/aff:buscapeid/uid:4781/tags:Mac+OS+X+Leopard" class="bbli">Mac OS X Leopard<img src="http://boo-box.com/bbli" alt="[bb]" class="bbic" /></a>.

Antes de efetuar os passos abaixo você precisará do Xcode instalado. Basta executar o 2º Disco do MAC OS X e executar o pacote de instalação do Xcode.

<h4>Apache</h4>
O Apache já vem instalado no MAC OS X, por isso precisaremos apenas habilitá-lo:
Vá em <strong>Preferências do Sistema</strong>, na opção <strong>Compartilhamento</strong> ative o serviço <strong>Compartilhamento Web</strong>.
Agora basta acessar <a href="http://localhost">http://localhost</a> para ver o apache funcionando. Dentro do seu diretório <strong>home</strong> existe um diretório chamado <strong>Sites</strong>, basta colocar os arquivos lá e acessar pelo endereço <a href="http://localhost/~SEU_LOGIN">http://localhost/~SEU_LOGIN</a>.

<h4>Mod_Python</h4>
Agora chegou a hora de compilar o mod_python e configurá-lo no Apache.
Primeiramente faça o <a href="http://www.apache.org/dist/httpd/modpython/mod_python-3.3.1.tgz">download do mod_python 3.3.1</a> (última versão disponível até a data deste post).

No terminal execute:
<pre class="bash"><code>$ gunzip mod_python<span class="nu0">-3.3</span><span class="nu0">.1</span>.tgz 
$ tar xvf mod_python<span class="nu0">-3.3</span><span class="nu0">.1</span>.tar
$ <span class="kw3">cd</span> mod_python<span class="nu0">-3.3</span><span class="nu0">.1</span>
$ ./configure --with-<span class="re2">apxs=</span>/usr/sbin/apxs</code></pre>

Após executar os comandos acima o arquivo <strong>src/Makefile</strong> foi criado. Abra-o em seu editor de texto preferido e altere a linha 27:
<pre class="bash"><code><span class="re2">LIBS=</span>-lm  -framework  Python    -ldl
<span class="re2">LDFLAGS=</span> -Wl,-framework,Python  -u _PyMac_Error -framework Python   -Wl,-F.
<span class="re2">OPT=</span></code></pre>
por:
<pre class="bash"><code><span class="re2">LIBS=</span>-lm  -framework  Python    -ldl
<span class="re2">LDFLAGS=</span> -Wl,-framework,Python  -u _PyMac_Error -framework Python   -Wl,-F. -arch x86_64
<span class="re2">OPT=</span></code></pre>

Altere também a linha 49:
<pre class="bash"><code>mod_python.so: $<span class="br0">&#40;</span>SRCS<span class="br0">&#41;</span>
    @<span class="kw3">echo</span>
    @<span class="kw3">echo</span> <span class="st0">'Compiling for DSO.'</span>
    @<span class="kw3">echo</span>
    $<span class="br0">&#40;</span>APXS<span class="br0">&#41;</span> $<span class="br0">&#40;</span>INCLUDES<span class="br0">&#41;</span> -c $<span class="br0">&#40;</span>SRCS<span class="br0">&#41;</span> $<span class="br0">&#40;</span>LDFLAGS<span class="br0">&#41;</span> $<span class="br0">&#40;</span>LIBS<span class="br0">&#41;</span> 
    @rm -f mod_python.so
    @ln -s .libs/mod_python.so mod_python.so</code></pre>
por:
<pre class="bash"><code>mod_python.so: $<span class="br0">&#40;</span>SRCS<span class="br0">&#41;</span>
    @<span class="kw3">echo</span>
    @<span class="kw3">echo</span> <span class="st0">'Compiling for DSO.'</span>
    @<span class="kw3">echo</span>
    $<span class="br0">&#40;</span>APXS<span class="br0">&#41;</span> $<span class="br0">&#40;</span>INCLUDES<span class="br0">&#41;</span> -c -Wc,<span class="st0">&quot;-arch x86_64&quot;</span> $<span class="br0">&#40;</span>SRCS<span class="br0">&#41;</span> $<span class="br0">&#40;</span>LDFLAGS<span class="br0">&#41;</span> $<span class="br0">&#40;</span>LIBS<span class="br0">&#41;</span>
    @rm -f mod_python.so
    @ln -s .libs/mod_python.so mod_python.so</code></pre>
Cuidado para não quebrar a indentação. O arquivo todo está indentado por TAB se você utilizar espaço dará erro na hora de rodar o <strong>make</strong>.
Salve o arquivo e execute os comandos abaixo no terminal:
<pre class="bash"><code>$ make
$ sudo make install</code></pre>

Precisamos efetuar uma alteração no mod_python para que ele funcione corretamente no Apache. Para isso abra o arquivo $ <strong>/Library/Python/2.5/site-packages/mod_python/importer.py</strong> como root e troque a linha 304 por esta:

<pre class="python"><code>        <span class="kw1">return</span> <span class="kw2">__import__</span><span class="br0">&#40;</span>module_name, <span class="br0">&#123;</span><span class="br0">&#125;</span>, <span class="br0">&#123;</span><span class="br0">&#125;</span><span class="br0">&#41;</span></code></pre>

Agora precisamos habilitar o mod_python no apache, para isso abra o arquivo <strong>/etc/apache2/httpd.conf</strong> (você precisará abrir o arquivo como root) e adicione a linha abaixo após a linha 116 (pelo menos foi a linha do meu arquivo):

<pre class="bash"><code>LoadModule python_module libexec/apache2/mod_python.so</code></pre>

Pronto, agora é só reiniciar o Apache e o mod_python já estará configurado.

<h4>PSE</h4>

<a href="http://nick.borko.org/pse/PSE-3.0.6.tar.gz">Baixe o PSE</a> e execute os comandos abaixo no terminal:
<pre class="bash"><code>$ tar xvf PSE<span class="nu0">-3.0</span><span class="nu0">.6</span>.tar
$ <span class="kw3">cd</span> PSE<span class="nu0">-3.0</span><span class="nu0">.6</span>
$ sudo python setup.py install</code></pre>

Agora vamos configurar o Apache para aceitar os arquivos escritos usando o PSE. Abra o arquivo <strong>/etc/apache2/httpd.conf</strong> e adicione as linhas abaixo no final do arquivo:

<pre class="bash"><code>PythonHandler pse_handler
AddHandler python-program .pt</code></pre>

Reinicie mais uma vez o Apache e crie dois arquivos de testes para ver se tudo está funcionando corretamente:
<strong>teste.py</strong>
<pre class="python"><code>msg = <span class="st0">&quot;Hello World!&quot;</span></code></pre>

<strong>teste.pt</strong>
<pre class="php"><code><span class="kw2">&lt;?</span>= <span class="re0">msg</span> <span class="kw2">?&gt;</span></code></pre>

Basta executar no navegador: <a href="http://localhost/teste.pt">http://localhost/teste.pt</a> ou <a href="http://localhost/~SEU_LOGIN/teste.pt">http://localhost/~SEU_LOGIN/teste.pt</a>.

<h4>SQLObject</h4>
Instalar o SQLObject é simples, basta executar no terminal:
<pre class="bash"><code>$ sudo easy_install -U sqlobject</code></pre>

<h4>MySQLdb</h4>
Instalar o MySQL-python exige uma pequena configuração. Primeiro <a href="http://osdn.dl.sourceforge.net/sourceforge/mysql-python/MySQL-python-1.2.2.tar.gz">baixe o arquivo</a> e execute no terminal:
<pre class="bash"><code>$ tar xzvf MySQL-python<span class="nu0">-1.2</span><span class="nu0">.2</span>.tar.gz
$ <span class="kw3">cd</span> MySQL-python<span class="nu0">-1.2</span><span class="nu0">.2</span></code></pre>

Abra o arquivo <strong>setup_posix.py</strong> e na linha 26 altere:
<pre class="python"><code>mysql_config.<span class="me1">path</span> = <span class="st0">&quot;mysql_config&quot;</span></code></pre>
por:
<pre class="python"><code>mysql_config.<span class="me1">path</span> = <span class="st0">&quot;/usr/local/mysql/bin/mysql_config&quot;</span></code></pre>

Agora abra o arquivo <strong>_mysql.c</strong> e remova as linhas 34, 37, 38 e 39:
<pre class="c"><code><span class="co2">#else</span>
<span class="co2">#include &quot;my_config.h&quot;</span>
<span class="co2">#endif</span>
<span class="co2">#ifndef uint</span>
<span class="co2">#define uint unsigned int</span>
<span class="co2">#endif</span></code></pre>
Também será preciso alterar as linhas 480 e 481:
<pre class="c"><code>    uint port = MYSQL_PORT;
    uint client_flag = <span class="nu0">0</span>;</code></pre>
por:
<pre class="c"><code>    <span class="kw4">unsigned</span> port = MYSQL_PORT;
    <span class="kw4">unsigned</span> client_flag = <span class="nu0">0</span>;</code></pre>

No terminal execute:
<pre class="bash"><code>$ sudo ln -s /usr/<span class="kw3">local</span>/mysql/lib /usr/<span class="kw3">local</span>/mysql/lib/mysql
$ sudo python setup.py build
$ sudo python setup.py install</code></pre>

Quando fizer o comando de <strong>sudo python setup.py build</strong> você poderá receber algumas mensagens de warning, ignore-as.

Para testar o SQLObject execute o script python abaixo:
<pre class="python"><code><span class="kw1">from</span> sqlobject <span class="kw1">import</span> *
sqlhub.<span class="me1">processConnection</span> = connectionForURI<span class="br0">&#40;</span><span class="st0">'mysql://root:SUA_SENHA@localhost/test'</span><span class="br0">&#41;</span>
<span class="kw1">class</span> Usuario<span class="br0">&#40;</span>SQLObject<span class="br0">&#41;</span>:
    nome = StringCol<span class="br0">&#40;</span><span class="br0">&#41;</span>
&nbsp;
Usuario.<span class="me1">createTable</span><span class="br0">&#40;</span><span class="br0">&#41;</span></code></pre>

Após executar o script acima a tabela usuario deverá existir no banco de dados test.

Se você tiver problemas para executar o SQLObject com MySQL verifique se a <a href="http://dev.mysql.com/get/Downloads/MySQL-5.0/mysql-5.0.51b-osx10.5-x86.dmg/from/http://mysql.cce.usp.br/">versão do MySQL instalada é a de 32bits</a>.

Pronto, o ambiente está completamente configurado no MAC OS X.

Agora voltaremos com nossa programação normal!
;)
