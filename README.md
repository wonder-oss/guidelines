
![Wonder Sistemas Logo](./logo.png)

# Diretrizes de Projetos Ruby
> Aqui está presente uma lista de diretrizes que nós achamos, escrevemos ou reunimos e que achamos que funcionam bem com os projetos de Ruby on Rails da [Wonder Sistemas](http://www.wonder.com.br).

- [Git](#git)
- [Documentações](#documentation)
- [Ambientes de Sistema](#environments)
- [Testes](#testing)
- [Estrutura de Projeto](#structure-and-naming)
- [Estilo de Código](#code-style)
- [API Design](#api-design)

## 1. Git <a name="git"></a>

### 1.1 Fluxo do Git
Nós usamos o fluxo de [branch por funcionalidade](./branch_workflow.md) com [rebasing interativo](https://www.atlassian.com/git/tutorials/merging-vs-rebasing#the-golden-rule-of-rebasing) e usamos um branch master que é o branch de desenvolvimento. Os passos básicos são os seguintes:

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

### 1.2 Algumas regras adicionais

* Faça todo o trabalho no branch criado.
* Faça pull requests para o branch `master`.
* Nunca faça push diretamente para o branch `master`.
* Atualize seu branch `master` e faça um rebase interativo antes de fazer push e criar uma PR.
* Resolva conflitos potenciais enquanto fizer rebase e antes de fazer um PR.
* Exclua o branch local e remoto depois de fazer merge.
* Antes de fazer um PR, assegure-se de que seu branch pode ser compilado e que passe nos testes automatizados.
* Utilize [esse arquivo de .gitignore](./.gitignore).
* Comentários de commit devem estar em português.
