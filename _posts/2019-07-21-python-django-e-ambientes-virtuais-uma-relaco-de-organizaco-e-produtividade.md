---
title: 'Python, Django e Ambientes Virtuais: uma relação de organização e produtividade'
date: 2016-02-24 22:44
headerImage: false
tag:
- python
- django
- environment
star: true
category: blog
author: lucasferreira
---

> O texto que você vai ler a partir de agora está publicado no meu perfil do Medium e, como eu optei pro criar meu próprio site, migrei o texto pra o site dando uma  repaginada no texto.

### Um breve conto
Quem desenvolve com Python e trabalha com mais de um projeto sabe que volta e meia rola uma dor de cabeça em relação a versões da linguagem e conflitos entre bibliotecas. Meses atrás eu estava iniciando meus estudo em Machine Learning e Data Science no laboratório da universidade e também trabalhava em um outro projeto com Django, e a partir daí começaram a surgir alguns problemas: nem conseguia rodar o Jupyter Notebook e nem um servidor Django localmente… e em meio ao caos me surgiu uma luz: **ambientes virtuais!**

![](http://www.reactiongifs.com/wp-content/uploads/2012/12/this-is-beautiful.gif)

Depois que lembrei disso, fui pesquisar pra aprender como fazer da melhor forma e no tutorial das meninas do [Django Girls](https://tutorial.djangogirls.org/pt/?source=post_page---------------------------) tinha lá tudo explicadinho, lindo de se ver! *-*

E como eu defendo a ideia de que conhecimento bom é conhecimento disseminado, resolvi (re)escrever aqui o passo-a-passo do tutorial das meninas de como criar um ambiente virtual de desenvolvimento Python.

### Antes de mais nada, o que são ambientes virtuais?
De forma resumida, os ambientes virtuais são um conjunto de diretórios que isolam versões do Python e de bibliotecas de forma local, separando-as das versões globais que acompanham o sistema operacional. Agora, vamos fazer a mágica acontecer!

### Organizando diretórios
Django passou a adotar exclusivamente Python 3.x após a release do Django 2.0, mais precisamente Python 3.6 e como eu utilizava inicialmente Anaconda só para Data Science e o Anaconda utiliza Python 3.7 (versões do Python utilizadas pelas tecnologias citadas no momento da escrita dessa publicação), surge a necessidade de se utilizar ambientes virtuais.

Para fins didáticos, vamos supor que você vai criar um blog em Django (que inclusive é bem legal de fazer). Então, crie um diretório para o projeto que você vai trabalhar e, em seguida, entre nele:

```
$ mkdir blogproject
$ cd blogproject
```

Depois que você entrar no diretório, seu terminal deve ficar assim:

![](https://miro.medium.com/max/700/1*-fVLijIdxTTOohheDNWs-A.png)

O comando ```mkdir``` cria diretórios e o comando ```cd``` acessa um diretório.

### Criando um ambiente virtual

Até onde eu sei, existem três ambientes virtuais por aí: [pyenv](https://github.com/pyenv/pyenv), [virtualenv](https://virtualenv.pypa.io/en/latest/) e [venv](https://docs.python.org/3/library/venv.html). Qual a diferença entre eles? Em linhas gerais, os dois primeiros precisam ser instalados na sua máquina e o último já vem no conjuntos de módulos padrão do Python desde a versão 3.3 da linguagem em algumas distribuições Linux e eu utilizo o Manjaro 18 Illyria e, por conta disso, utilizarei a **venv**.

Dentro do diretório ```blogproject``` vamos criar nosso ambiente virtual chamado blog com o seguinte comando:

```
~/blogproject$ python3 -m venv blog
```

Este comando cria um diretório chamado ```blog``` que contém nosso ambiente virtual (que é basicamente composto por diretórios e arquivos). Para ativarmos o nosso ambiente virtual, vamos rodar o seguinte comando:

```
~/blogproject$ source blog/bin/activate
```

Acabamos de ativar nosso ambiente virtual! Com o ambiente ativado, seu terminal deve ficar assim:

![](https://miro.medium.com/max/700/1*n3SlzBrbi6kgBXEuEhnfnw.png)

Nesse estado, toda e qualquer instalação de módulos Python e até configurações de versões do Python será feita localmente no seu ambiente sem alterar Python globalmente no seu sistema operacional.

### Instalando Django
Agora com o ambiente virtual ativo, podemos instalar o Django. O primeiro passo agora é verificar se a última versão do ```pip``` está instalada. O ```pip``` é o gerenciador de pacotes Python e é com ele que instalamos módulos e frameworks Python necessárias para seu projeto. Com o comando a seguir, faremos a instalação ou atualização do ```pip```:

```
~/blogproject$ python3 -m pip install --upgrade pip
```

Feito isso, vamos instalar o Django através de requisitos, utilizando um arquivo chamado ```requirements.txt```, que guarda as dependências necessárias para instalação utilizando o ```pip install```. Dentro do diretório ```blogproject``` crie um arquivo chamado ```requirements.txt```. Em seguida, abra o arquivo e escreva Django~=2.1.4 (ou a versão que você preferir), salve o arquivo e feche-o.

**Informação legal antes de executar esse comando:** no comando salvo em requirements.txt existe uma espécie de operador: ```~=```. Ele vai dizer ao pip “pip, favor, instale a versão do Django igual ou superior a 2.1.4”. Se você preferir instalar exatamente a versão que você explicitou no arquivo, use ```==``` que significa dizer “pip, por favor, instale exatamente a versão solicitada”. Agora, execute o comando:

```
~/blogproject$ pip install -r requirements.txt
```

### Bonus Track: Django Hello World!
Como bônus, vou te ajudar a fazer um “Hello World” em Django. Talvez você que tá lendo esse texto esteja começando com Django e por algum motivo veio parar aqui. Se você só tem interesse em saber dos ambientes virtuais, pode rolar a página um pouco mais.

Para criar seu projeto Django, rode esse comando:

```
~/blogproject$ django-admin startproject meublog
```

E pronto! Seu projeto Django foi criado!

![](https://miro.medium.com/max/480/1*mNGFX8u39v3fGLgzS9k3pA.gif)

Agora, digite ```ls``` no seu terminal e veja o que tem dentro dele:

![](https://miro.medium.com/max/700/1*ZMLY3eFkhqiT65dxqNO1OA.png)

Entendendo o que estamos vendo: ```blog``` é o diretório do seu ambiente virtual, ```meublog``` é o diretório do seu projeto. Agora use novamente o comando ```cd``` para entrar no diretório ```meublog``` e em seguida rode o comando ```runserver``` para exibir seu site:

![](https://miro.medium.com/max/700/1*3upBwwc234-N_6L7JWlxPw.png)

Quando você rodar o ```runserver```, o Terminal vai te mostrar uma saída parecida com essa:

![](https://miro.medium.com/max/700/1*twCNjKZIhsrX_0iy3zuOKw.png)

> Se você estiver vendo uma parte do texto do terminal em vermelho escrito “You have 15 unapplied…”, não se preocupe: é só um aviso do Django dizendo que você deve migrar suas aplicações para o banco de dados. Mais adiante nos seus estudos você vai entender melhor isso.

Copie e cole esse endereço http://127.0.0.1:8080 no seu navegador ou então posicione o cursor do mouse e depois faça Ctrl+clique do mouse que ele te redireciona para o navegador e, em seguida, você vai ver uma tela como essa:

![](https://miro.medium.com/max/700/1*FEXvL5XivNmyWFc5WXy_6g.png)

Parabéns! Você acabou de fazer o seu Hello World em Django!

### Considerações Finais
Eu espero ter te ajudado a criar um ambiente virtual. Quando eu consegui criar meus ambientes e rodar meus projetos sem problemas eu fiquei muito feliz e fui dormir sereno. De verdade! E um recado para você que tá entrando no mundo Python (e no mundo de desenvolvimento de software): seja um desenvolvedor organizado! Python te força a ser organizado tanto na escrita de código quanto na criação de ambientes de desenvolvimento e isso pode te fazer sair na frente numa vaga de emprego, numa vaga de projetos e etc.

Quero agradecer as meninas do Django Girls por terem criado um tutorial de Django tão didático e tão completo! Escrito desde como funciona a web até você colocar a mão no código! Foi o tutorial delas que me inspirou a fazer este que, no fim das contas, é um recorte de uma parte do tutorial delas e agradeço também a Jessica Temporal que foi pelo site dela que eu descobri o venv e tive as primeiras sacadas sobre esse ambiente virtual. Obrigado meninas, vocês arrasam!

![](https://miro.medium.com/max/480/1*TlzCM3A6lRXM5FvZIge03Q.gif)

Também tô muito feliz porque esse é minha primeira publicação por aqui 😍 (foi minha primeira publicação no Medium e é a primeira no site) e espero continuar escrevendo sempre que eu tiver alguma coisa legal pra compartilhar. Bem, é isso. Abraços e até mais!