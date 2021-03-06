# Instalando e configurando o Git

Antes de utilizarmos o Git, é fundamental instalá-lo. Para isso, você deve verificar seu **sistema operacional**, que é aonde você irá realizar a instalação de forma apropriada e mãos à obra!

Abaixo, se encontra tópicos relacionados a maneira de instalá-lo em diferentes **sistemas operacionais**.

## Instalando no Windows

Acesse a seguinte URL, faça o download e instale a última versão disponível: http://msysgit.github.io/

A instalação é bastante simples. Escolha as opções padrão. Serão instalados alguns programas, sendo o mais importante o Git Bash, que permite que o Git seja executado pela linha de comando no Windows.
Dê duplo clique no ícone do Git Bash e será aberto um terminal, com o seguinte prompt na linha de comando:

``$``

Esse prompt será seu amigo a partir de agora. Não tenha medo! Sempre que falarmos de terminal, estaremos falando do Git Bash.

## Instalando no Mac

Baixe a última versão do instalador gráfico do Git para Mac OS X a partir do link: https://code.google.com/p/git-osx-installer/downloads

Abra um terminal e prepare-se para utilizar o Git!

## Instalando no Linux

Para instalar o Git no Ubuntu, ou em uma outra distribuição baseada em Debian, execute em um terminal:

``$ sudo apt-get install git``

No Fedora, utilize:

``$ sudo yum install git``

Para as demais distribuições do Linux, veja o comando em: http://git-scm.com/download/linux

## Configurações básicas

É importante nos identificarmos para o Git, informando nosso nome e e-mail. Em um terminal, execute os comandos a seguir:

``$ git config --global user.name "Fulano da Silva"``

``$ git config --global user.email fulanodasilva.git@gmail.com``

Claro, utilize seu nome e e-mail!

# Criar um repositório

O primeiro passo para trabalhar com Git é criar um repositório. Um repositório é um diretório de arquivos versionados. Para criar um repositório, basta rodar o comando:

``$ git init NOME_DO_REPOSITORIO``

Exemplo:

``$ git init games`` cria a pasta chamada games, que é um repositório Git.

# Adicionar arquivos

Do ponto do vista do Git, existem quatro estados no qual um determinado arquivo pode estar.

*  Commited: O arquivo está sob controle de versão e não apresenta nenhuma modificação.

*  Commit candidate: Caso você crie um conjunto de modificações (commit), esses serão os arquivos incluídos.

*  Modified: Arquivos que foram modificados.

*  Untracked: Arquivos novos, que ainda não estão no controle de versão.

Para mudar um arquivo de untracked ou modified para Commit candidate, você usa o comando git add CAMINHO. O git add é inteligente, então se você passar um caminho parcial para ele, ele muda o estado de todos os arquivos que contém esse caminho parcial.

Exemplo:

* ``$ git add . `` mudaria o estado de todos os arquivos a partir do diretório atual.

* ``$ git add arquivo.txt `` mudaria o estado do arquivo arquivo.txt

* ``$ git add pasta `` mudaria o estado do arquivo pasta/arq1.txt e do pasta/arq2.txt, mas não mudaria do outra_pasta/arq1.txt

# Fazer Commits

Agora que você já sabe como selecionar as modificações que quer incluir em um pacote de modificações (um commit), chegou a hora de aprender como gerar esse pacote. 
O comando utilizado para criar um commit em git é *git commit*. Com esse comando, todos os arquivos que estiverem marcados como Commit candidate serão incluídos no commit. Se você também quiser incluir os arquivos que estão marcados como modified, você pode incluir a flag *-a*.

Uma coisa muito importante de qualquer commit é uma mensagem que explique o que significa aquele commit. Para isso, você pode passar a opção *-m "mensagem de commit" *. Caso você não passe, o git vai abrir um editor de texto para que você digite a mensagem.

Exemplo:

`` $ git commit -m "commit" `` cria um commit com todos os Commit candidate e a mensagem *commit*

`` $ git commit -a -m "segundo commit"`` cria um commit com os arquivos marcados como Commit candidate e os modified e junta com a mensagem *segundo commit*

Uma outra possibilidade para commit utiliza da flag ``-s``. Essa flag permite que o mesmo commit tenho vários autores, ou seja, você e outro desenvolvedor podem coolaborar para um mesmo fim e commitarem "juntos".  
  
É importante lembrar que esse tipo de commit leva em consideração o usuário configurado no git como principal e dá status de coolaborador para os demais.  
  
Para usar essa flag basta digitar, ``git commit -s``.   
Com Enter pressionado você será redirecioado para seu editor de texto padrão, visualizando algo semelhante:  

![Commit em grupo](https://raw.githubusercontent.com/wiki/fga-gpp-mds/00-Disciplina/img/commitGrupo.png) 

Na primeira linha insira um **Título** para o commit.  
Na segunda linha **descreva** um pouco melhor as alterações.  
Para adicionar os **coautores**, basta copiar a linha, ``Signed-off-by`` e colar na linha abiaxo mudando os dados necessários.  
    
Feito isso basta salvar o arquivo e seu commit será efetuado com sucesso.  

# Enviar commits para um repositório

Para enviar os commits feitos para o repositório desejado, utiliza-se o comando `push`. Este comando tem a seguinte assinatura: __`git push local_remote_name remote_branch_name`__, onde __`local_remote_name`__ indica o nome do repositório local em que o repositório git se encontra e __`remote_branch_name`__ indica o nome da branch em que deve ser enviado o conjunto de commits.

# Trabalhando com branches

É importante saber utilizar da melhor maneira possível as branches do git. Branches servem para você trabalhar em uma determinada funcionalidade, dependendo da política de configuração implementada no seu projeto. O ideal de trabalhar com branches é que você possa trabalhar sem interferir em funcionalidades que já estão implementadas. 

É sugerido que no seu projeto seja definida uma branch que contenha todo o conteúdo devidamente testado e aprovado conforme os critérios de aceitação. Essa branch é criada a partir do `merge` de outras e compõe o produto mais atualizado nesse repositório. 

### Situação
Após vários merges e `rebases` de outras branchs a branch `dev` é a mais atual do projeto. Ainda faltam o caso de uso X para que o produto possa ser devidamente entregue, os desenvolvedores precisam trabalhar em paralelo para implementar todas as funcionalidades desse caso de uso. Sabendo que a `dev` está atualizada os desenvolvedores tomam a seguinte decisão: 
 * Todos, de seus computadores, mudam para `dev`: `git checkout dev`
 * A partir da `dev` criam novas branches com nomes significativos das funcionalidades que implementarão: `git checkout -b funcionalidade_x`
 
A partir de agora os desenvolvedores podem trabalhar separadamente na implementação das funcionalidades de casos de uso sem problemas, de forma que minimizem os riscos de conflitos durante o projeto, pois as novas branches tem uma origem em comum. 
# O comando Git Stash
Caso você esteja trabalhando em uma parte do seu projeto que não está fluindo muito bem e não deseja fazer um commit disso para trabalhar em outra branch por um tempo, o que fazer? Dá para resolver isso com um comando bem útil: `git stash`. Com esse comando os arquivos monitorados que foram modificados serão salvos em uma pilha de modificação não finalizadas que você pode recuperar e finalizar depois. Você pode criar uma lista de stashes e visualizá-los depois com o comando `git stash list`. 
Você pode aplicar novamente o stash feito com o comando `git stash apply`. Porém com esse comando o Git identifica apenas o útimo stash feito, para selecionar um stash específico utilize o comando : `git stash apply stash@{número do stash}`
# Merge e Rebase

### Situação 
Terminado o trabalho de implementação das funcionalidades do Caso de Uso X os desenvolvedores desejam juntar suas alterações para, finalmente, terminarem o caso de uso. Como foi dito acima as branches das funcionalidades tem uma origem em comum, `dev`, o que torna a mescla mais fácil. 

## Merge 
O merge é a mescla do conteúdo de duas branches. Para realizar tal operação tenha em mente que:

 * Você vai _fazer o merge_ da branch passada como parâmetro na sua branch **ATUAL** 

### Exemplo: 

Os desenvolvedores resolveram _fazer o merge_ a branch `funcionalidade_a` na `funcionalidade_b`, para tal eles:

* Mudaram para a branch `funcionalidade_b`. `git checkout funcionalidade_b`;
* `On branch funcionalidade_b`
* Realizaram o merge de a --> b. `git merge funcionalidade_a`

Isso gerou um commit de merge. Isso pode gerar um pouco de poluição no log de commits. 

## Rebase 
O rebase é uma alternativa ao merge. Também mesclando o conteúdo de duas branches, mas o rebase insere os commits de modo cronológico no histórico de commits. O rebase também não deixa uma mensagem de commit, uma das vantagens de usar-se o rebase. 

No uso do rebase você adicionará os commits da branch `funcionalidade_a` na `funcionalidade_b` da seguinte maneira: 
* Vá para a branch `funcionalidade_a`
* execute: `git rebase funcionalidade_b`

isso adicionara os commits que estão em `a` mas não estão em `b` em `funcionalidade_b` de forma que você poderá realizar um `fast-forward merge` em `b`

* `git checkout funcionalidade_b`
* `git merge funcionalidade_a`



# Plataforma de Exemplo

Para aprender mais sobre git e exercitar, acesse o [Codecademy](https://www.codecademy.com/pt-BR/learn/learn-git).

Para exercitar e fixar os conhecimentos de Git, utilize a plataforma [Learn Git Branching](http://learngitbranching.js.org/)

Para treinar Git de maneira interativa, um otimo estilo de jogo [Aprenda Git](http://aprenda.vidageek.net/aprenda/git)
ou
[Git Real Code School](http://gitreal.codeschool.com/)

# Referências

* [Controlando versões com Git e GitHub - Casa do Código](https://github.com/brunoipjg/myEbooks/blob/master/Controlando%20vers%C3%B5es%20com%20Git%20e%20GitHub%20-%20Casa%20do%20Codigo.pdf)
* [Ferramentas do Git - Fazendo Stash](https://git-scm.com/book/pt-br/v1/Ferramentas-do-Git-Fazendo-Stash)