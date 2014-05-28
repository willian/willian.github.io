---
layout: post
title: 'Subversion: você só sente falta quando perde!'
categories:
- blog
tags: []
status: publish
type: post
published: true
meta: {}
---
Nos aqui da [Visie](http://visie.com.br) estamos acostumados a criar um repositorio no [Subversion](http://subversion.tigris.org/) para cada novo projeto que iremos trabalhar.

É muito bom trabalhar com o Subversion, ainda mais quando podemos trabalhar longe do escritorio. Acontece que, nos ultimos tres meses estou alocado em um cliente, desenvolvendo um gigantesco projeto em PHP.

Aqui (no cliente) nao podemos utilizar nenhum controle de versao, muito menos Linux nas estaçoes de trabalho. O servidor e um AS/400 e o banco de dados e DB2. Entao, deu para imaginar como acessamos os arquivos do servidor?

Temos uma mapeamento no Windows para o diretorio do projeto no servidor AS/400. Ou seja, todos os programadores acessam o mesmo arquivo, ao mesmo tempo, no mesmo lugar. Ah! Este servidor e o mesmo para Desenvolvimento, Testes (Homologaçao) e Produçao.

Para evitar que alguem edite os arquivos de produçao foi criada a seguinte estrutura de diretorios:


* PROJETO_D
* PROJETO_H
* PROJETO_P


Assim ficou melhor, nao e? Olha so que coisa mais inteligente e organizada:


1. Depois que eu terminar de desenvolver basta copiar os arquivos do diretorio PROJETO_D e colocar no diretorio PROJETO_H;
2. Se alguma coisa estiver errada e so copiar o(s) arquivo(s) que sera(ao) corrigido(s) do PROJETO_H e colar no PROJETO_D;
3. Assim que editar esses arquivos e so fazer o primeiro passo novamente;
4. Se tudo for homologado e so copiar os arquivos do PROJETO_H para o PROJETO_P e pronto!


Acontece que, estava eu alterando um arquivo quando de repente aparece a seguinte mensagem:
!["Alguém](http://willianfernandes.com.br/wp-content/uploads/2007/09/alguem_fucando1.PNG)

Pois e, isso acontece porque todas as pessoas envolvidas no projeto estao com o diretorio mapeado em seus Windows e sempre que eu for alterar um arquivo tenho que verificar se alguem esta alterando o mesmo arquivo para evitar esses tipos de conflitos.

Que falta eu sinto do Subversion! :(

PS.: O backup dos arquivo do sistema e feito em um diretorio chamado backup que possui outros diretorios com os nomes mais ou menos assim: PROJETO_D_20070906. Esse "backup" esta no mesmo HD que o sistema, ou seja, se o HD um dia "morrer" o sistema e o backup morrerao tambem.
