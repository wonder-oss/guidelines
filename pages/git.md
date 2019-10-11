## 1. Git

![Git](/images/pages/git.png)

Sumário

- [1.1 Fluxo de Commits](#1.1)
- [1.2 Porque evitar `git merge` diretamente](#1.2)

### 1.1 Fluxo de Commits <a name="1.1"></a>

Nós usamos [branch por funcionalidade](https://www.atlassian.com/git/tutorials/comparing-workflows#feature-branch-workflow) com [rebasing interativo](https://www.atlassian.com/git/tutorials/merging-vs-rebasing#the-golden-rule-of-rebasing) e usamos um branch master que é o branch de desenvolvimento. Os passos básicos são os seguintes:

* Criar um novo branch com uma nova funcionalidade/correção
    ```
    git checkout -b <nome_do_branch>
    ```
* Adicionar as mudanças
    ```
    git add
    git commit -m "Descrição das mudanças"
    ```
* Sincronizar o branch master local com o git, pois possivelmente terá mudanças
    ```
    git checkout master
    git pull
    ```
* Enviar o seu branch com as últimas mudanças do branch master usando rebase interativo ([Leia Mais](https://www.atlassian.com/git/tutorials/merging-vs-rebasing#the-golden-rule-of-rebasing))
    ```
    git checkout <nome_do_branch>
    git rebase -i master
    ```
* Se não houver conflitos de arquivo, pule este passo. Se houver, [resolva-os](https://help.github.com/articles/resolving-a-merge-conflict-using-the-command-line/)  e continue o rebasing
    ```
	git add <arquivo1> <arquivo2> ...
    git rebase --continue
    ```
* Faça push do seu branch. O rebase vai alterar o histórico, logo você deve usar a opção `-f` para forçar as mudanças no branch remoto. Se houver outra pessoa trabalhando no mesmo branch, use a opção `--force-with-lease` ([Entenda o porque](https://developer.atlassian.com/blog/2015/04/force-with-lease/)).
    ```
    git push -f
    ```
* Faça um pull request
* Remova o seu branch local
    ```
    git branch -D <nome_do_branch>
    ```

### 1.2 Porque evitar `git merge` diretamente <a name="1.2"></a>

O comando `git merge` cria um novo commit acima das suas mudanças, isso quer dizer que ao fazer revisão de código, este foi mesclado com o branch de origem, e possui código que já foi revisado e quem revisa tem o trabalho de passar pelo mesmo código múltiplas vezes.

Em algumas situações é OK usar merge, como por exemplo quando uma branch já tem muito tempo, e fazer rebase originaria um trabalho extra de passar commit por commit e resolver conflitos.

Merges periódicos são ruins pois criam a mesma situação do merge (código antigo sobre o código novo) só que repetidamente, ou seja mais código vai ser revisado em duplicidade além de demonstrar que a branch está aberta por muito tempo, o que já indica um padrão ruim de agilidade no desenvolvimento.

Recapitulando:

 - Branch + Rebase = Perfeição
 - Branch + Merge = OK
 - Branch + Merges Periódicos = Ruim
