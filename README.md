# AULA 01 - GITHUB E OPENSOURCE

## INTRODUÇÃO

Nesse curso, aprenderemos sobre o que é o _open source_, como lidar com _issues_, _pull requests_ e as melhores práticas ao contribuirmos com projetos _open source_.

Além disso, veremos técnicas avançadas de resolução de conflitos, estratégias de _branching_ e etc.

## OPEN SOURCE

O GitHub é muito utilizado pela comunidade _open source_.

Quando criamos um projeto de código aberto, estamos criando um projeto em que outras pessoas podem nos ajudar, através da implementação de melhorias, resolução de conflitos e etc.

## ISSUES

Dentro das `issues`, podemos realizar pedidos de melhoria, correções de funcionalidades e etc.

Podemos criar `issues` em qualquer repositório. Podemos sugerir uma nova alteração ou funcionalidade através de uma `issue`, ou até realizar uma pergunta sobre o projeto para o desenvolvedor.

Uma `issue` aceita o formato `Markdown`.

Podemos fechar uma `issue` se tivermos a permissão no repositório, assim, se resolvermos um determinado problema, podemos fechar essa `issue`.

## PULL REQUESTS

Para contribuirmos com um projeto open source, primeiramente, devemos realizar um `fork`. Um `fork` é uma **cópia de um repositório**, assim, através de um repositório remoto, podemos criar esse `fork`.

Dessa forma, podemos criar o `fork`, criarmos o repositório remoto desse `fork`, através do comando `git remote add nome-do-repositorio-remoto link-do-repositorio-remoto-que-fizemos-o-fork`, e, depois disso, utilizarmos o comando `git pull nome-do-repositorio-remoto nome-da-branch`.

Até o momento, temos o **repositório local sincronizado com o repositório remoto do** `fork`.

Agora, basta realizarmos as alterações desejadas, utilizarmos os comandos `git add .` e `git commit` para commitarmos as alterações.

Agora, basta utilizarmos o comando `git push nome-do-repositorio-remoto nome-da-branch` para enviarmos as informações ao `fork` remoto.

Para enviarmos as modificações para o repositório original do repositório em que realizamos o `fork`, temos que abrir um `pull request`. Para isso, devemos abrir o nosso `fork` no GitHub e clicarmos no botão `Create Pull Request`, assim, basta inserirmos um título e uma mensagem ao `pull request`, e ele será enviado para o dono do repositório.

Dessa forma, basta o dono do repositório apenas aprovar o `pull request`, clicando no botão `Merge Pull Request`.

Após isso, basta o dono do repositório clicar na aba `issues` e fechar uma `issue` que foi resolvida pelo `pull request` anterior, comentando, nessa `issue`, uma mensagem, como: `Fechado pelo PR #id-do-PR`, e fechando essa `issue` através do comando `Close and Comment`.

## UNINDO COMMITS

Para unirmos três commits em apenas um, podemos utilizar o comando `git rebase -i HEAD~3`, assim, de forma interativa, podemos alterar a linha do tempo dos três primeiros commits, começando pelo commit atual.

Se desejarmos, podemos utilizar o comando `git rebase -i HEAD~hash-do-ultimo-commit`, assim, o comando `git rebase` poderá ser executado em todos os `commits`, do `commit` que estamos atualmente até o `commit` que foi definido pelo `hash-do-ultimo-commit`. Esse comando **não inclui o último** `commit`.

Após isso, teremos a lista dos commits que queremos analisar.

Basta, dentro da tela interativa do comando `git rebase`, trocarmos o `pick` pelo `s`, representando que queremos unir esse `commit` ao `commit` anterior.

Se tivermos três commits, devemos trocar o `pick` pelo `s` nos dois últimos, e deixarmos apenas o `pick` como o primeiro `commit`. Abaixo, veremos uma representação visual do arquivo final do comando `git rebase`.

```
pick 971dba0 Trocando UL por DL.
s 3db095f Separando os títulos
s af37cf6 Quebras de linha
```

Após isso, basta salvarmos o arquivo do `git rebase` e fornecermos uma **nova mensagem para esse commit de** `rebase`, assim, se digitarmos o comando `git log`, veremos que os últimos três commits foram excluídos da linha do tempo e que foi realizado **apenas um commit**.

## ALTERNATIVAS AO GITHUB

Existem várias alternativas ao [GitHub](https://github.com), como o [BitBucket](https://bitbucket.org) e o [GitLab](https://about.gitlab.com).

# AULA 02 - CONTROLE AVANÇADO DE CONFLITOS

## PEGANDO UM COMMIT

O comando `git cherry-pick hash-do-commit` permite que obtenhamos **apenas o código do** `commit` selecionado para o `branch` que estamos atualmente, assim, todas as outras mudanças de outros commits **não serão obtidas**, e sim **apenas as mudanças de um commit específico**.

Essa funcionalidade pode ser utilizada, por exemplo, para trazermos para a `branch` atual uma solução de um bug que **já foi corrigido em outra** `branch` e que **está afetando a** `branch` **atual**.

## ENCONTRANDO BUGS

Podemos utilizar o comando `git bisect start` para que o Git realize uma busca pelos commits de uma determinada `branch`.

Primeiramente, devemos informar qual é o `commit` em que temos algo que **não queremos**, assim, devemos digitar o comando `git bisect bad HEAD`, assim, informaremos que, no `commit` atual, temos um código que não está certo.

Após isso, temos que inserir o hash de um commit em que, possivelmente, uma linha do arquivo estará boa, através do comando `git bisect good c17076a`, assim, se verificarmos a alteração que o Git sugeriu e ela estiver certa, podemos utilizar novamente o comando `git bisect good`, e, depois disso, verificarmos a próxima mudança sugerida pelo Git. Se ela não estiver certa, devemos utilizar, novamente, o comando `git bisect bad`, dessa forma, o Git, através de diversas utilizações dos comandos `git bisect good` e `git bisect bad`, o Git fará o filtro dos commits até, possivelmente, indicar o `commit` específico que introduziu um bug na aplicação.

Assim, após encontrarmos o `commit` responsável por introduzir um bug na aplicação, podemos desfazer, analisar ou efetuar diversas outras ações com esse determinado `commit`.

Para visualizarmos todas as alterações de um `commit`, podemos utilizar o comando `git show hash-do-commit`, assim, será exibida todas as alterações que foram realizadas nesse determinado `commit`.

## ENCONTRANDO O CULPADO

Podemos utilizar o comando `git blame index.html`, veremos todos os responsáveis por cada uma das linhas de um determinado `commit` no arquivo `index.html`.

# AULA 03 - ESTRATÉGIAS DE BRANCHING

## MASTER E PRODUÇÃO

O branch `master` é onde teremos todo o código que vai para a produção, ou seja, em que todo o código que está pronto para o uso será inserido.

O comando `git log --graph` exibirá uma representação mais gráfica do log de commits.

## MAIS BRANCHES

Para removermos um `branch`, podemos utilizar o comando `git branch -d nome-do-branch`, ou, se existisse algum conflito no `branch` que queremos excluir, como ele estiver à frente do `branch` atual, podemos utilizar o comando `git branch -D nome-do-branch`, pois a remoção desse `branch` será **forçada**.

## GIT FLOW

O **_Git Flow_** é uma metodologia de organização das branches, **facilitando o desenvolvimento e a correção de bugs**.

No GitFlow, a branch `master` deverá ter apenas o código que está **pronto para ir para a produção**.

A branch `develop` deverá ser a `branch` em que **o código estará sendo desenvolvido**. Ao criarmos uma `branch` para uma funcionalidade específica, devemos criar essa `branch` através da branch `develop`, essa `branch` para o desenvolvimento de uma nova funcionalidade será chamada de `feature`, e será um **galho para a** `branch` de `develop`.

Quando acumularmos várias features desenvolvidas na branch `develop`, deveremos criar uma nova `branch` de `release`, que é quando **começamos o processo de lançarmos uma nova versão da aplicação**.

Dentro da branch `release`, devemos **apenas corrigir os bugs dessa** `release` **específica**. Sempre que um bug for corrigido na `branch` de `release`, devemos retornar esse código para a branch `develop`, pois outras features podem aproveitar a correção desse bug.

No final, quando tudo for corrigido, devemos enviar a versão da branch `release` para a branch `master`, e criarmos uma `tag` com uma nova versão da aplicação.

Se encontrarmos um bug na branch `master`, ou seja, um bug em produção, devemos criar um `branch` de `hotfix` a partir da branch `master`, corrigir esse bug e enviarmos a correção desse bug tanto para a branch `master`, através de uma nova `tag`, quanto pra branch `develop`.

O fluxo acima foi representado na imagem abaixo.

![[Pasted image 20230122100248.png]]

# AULA 04 - FERRAMENTAS VISUAIS

## GIT COLA

Essa foi uma das primeiras ferramentas que surgiram para manipularmos o Git através de uma GUI.

Ele não é a ferramenta mais completa, dessa forma, existem outras ferramentas mais atuais que possuem mais funcionalidades.

## GITHUB DESKTOP

É a ferramenta oficial do GitHub para manipularmos o Git através de uma GUI.

## GIT KRAKEN

Essa é a ferramenta mais complexa e completa para trabalharmos com o Git. Ele possui integração com vários provedores de nuvem, como o GitHub, o BitBucket e etc.

O GitKraken facilita a utilização do Git Flow.

# AULA 05 - HOOKS E DEPLOYS COM GIT

## EVENTOS NO GIT

Os **_Git Hooks_** servem para executarmos uma determinada ação quando determinados eventos do Git forem acionados.

Dentro do diretório `.git/hooks`, temos comandos que podem executados quando um determinado evento acontecer, que são os exemplos com o `.sample`.

Podemos criar um Shell Script para executarmos quando um determinado evento acontecer, por exemplo:

```shell
#!/bin/bash

#Arquivo "pre-commit".
echo "Você está prestes a commitar."
```

Após isso, se estivermos no Linux ou no Mac, basta executarmos o comando `chmod u+x ./pre-commit`, para fornecermos a permissão de execução para esse arquivo.

Após isso, sempre que realizarmos um determinado commit, **esse Shell Script** será executado.

Podemos, por exemplo, inserir os scripts que executam testes na aplicação antes de commitarmos um arquivo.

O nome do arquivo **sempre deverá representar o seu evento**.

## DEPLOY COM GIT

Podemos criar, na pasta `.git/hooks`, o arquivo `post-receive`. Depois que recebermos um `push`, esse script será executado. O código desse script será inserido abaixo.

```shell
#!/bin/bash

git --git-dir="C:\Users\ALURA\Documents\git-e-github\servidor" --work-tree="C:\Users\ALURA\Documents\git-e-github\web" checkout -f
```

No script acima, quando executarmos o comando `git push`, o arquivo em que o `push` foi realizado será inserido no diretório `C:\Users\ALURA\Documents\git-e-github\web`.

O diretório `C:\Users\ALURA\Documents\git-e-github\servidor` representará o **servidor remoto da aplicação**.

Após isso, temos que executar o comando `chmod u+x ./post-receive`, para fornecermos a permissão de execução para esse script.
