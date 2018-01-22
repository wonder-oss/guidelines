
![Wonder Sistemas Logo](/images/logo.png)

# Diretrizes de Projetos Ruby
> Lista de diretrizes que nós achamos, escrevemos ou reunimos e que achamos que funcionam bem com os projetos Ruby on Rails da [Wonder Sistemas](http://www.wonder.com.br).

- [Git](#git)
- [Documentação](#documentation)
- [Ambientes de Sistema](#environments)
- [Testes](#tests)
- [Estilo de Código](#code-style)
- [API](#api)

## 1. Git <a name="git"></a>
![Git](/images/git.png)

### 1.1 Fluxo do Git
Nós usamos o fluxo de [branch por funcionalidade](https://www.atlassian.com/git/tutorials/comparing-workflows#feature-branch-workflow) com [rebasing interativo](https://www.atlassian.com/git/tutorials/merging-vs-rebasing#the-golden-rule-of-rebasing) e usamos um branch master que é o branch de desenvolvimento. Os passos básicos são os seguintes:

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

## 2. Documentação <a name="documentation"></a>
![Documentação](/images/documentation.png)

* Use esse [template](./README.sample.md) para o `README.md` do projeto.
* Para projetos com mais de um repositório direcionar para os seus arquivos de `README.md`.
* Manter o `README.md` atualizado à medida que o projeto evolui.
* Comentar pequenas porções de código quando achar que o código não é autoexplicativo.
* Comentar o código quando pertencer a uma biblioteca de funções que pode ser utilizada por múltiplos projetos.
* Manter os comentários de código atualizados à medida que o código evolui.

## 3. Ambientes de Sistema <a name="environments"></a>
![Ambientes de Sistema](/images/environment.png)

## 4. Testes <a name="tests"></a>
![Testes](/images/testing.png)

## 5. Estilo de Código <a name="code-style"></a>
![Estilo de Código](/images/code-style.png)

- É recomendado utilizar algum plugin de análise automática para seu editor de texto para forçar as boas práticas em tempo de código.
- Reforçar o mesmo estilo de código nas aplicações para que todo o time siga as mesmas métricas.

### 5.1. Ruby

Utilize as métricas de código da gem [Wonder-Ruby-Style](https://github.com/wondersistemas/wonder-ruby-style).

### 5.2. Javascript/Ecmascript/Typescript

Utilize eslint/tslint para reforçar métricas comuns da comunidade.
Utilize identação de 2 espaços para cada nível.

### 5.3. CSS/SCSS/LESS

Utilize csslint para reforçar métricas comuns da comunidade.
Utilize identação de 2 espaços para cada nível.
Utilize [CSS orientado à objetos](http://thesassway.com/intermediate/using-object-oriented-css-with-sass) como padrão de arquitetura.

## 6. API <a name="api"></a>
![API](/images/api.png)

### 6.1. Versionamento

O padrão de versionamento de API deve seguir os modelos abaixo e estar prefixado com `v` (ex: v1, v2) e deve estar no escopo mais alto da URL, esta forma facilita a manutenibilidade das versões e mudanças na API incompatíveis com clientes que ainda utilizam versões mais antigas.

`www.site.com/api/v1/users`
`api.site.com/v1/users`

### 6.2. API Design

Url's devem conter nomes no plural quando se trata de coleções de dados.

`/api/v1/usuarios`
`/api/v1/oportunidades`

Use *snake_case* para palavras compostas ou combinações de palavras.

`/api/v1/sessoes_usuario`
`/api/v1/anexos?nao_enviados=1`

Nunca crie url's que apontam diretamente para uma propriedade de uma coleção.

`/api/v1/anexos/10/descricao`

Use verbos quando url's não tem objetivo de operar com coleções, mas que executam alguma operação.

`/api/v1/emails/enviar`

Não utilize '/update_user' ou '/add_user', ao invés disso disponha das funcionalidades CRUD utilizando métodos HTTP.

> **GET**: Retorna uma representação de uma coleção ou recurso

> **POST**: Cria um recurso ou sub-recurso

> **PUT**: Atualiza recursos existentes

> **PATCH**: Atualiza recursos existentes. Apenas atualiza campos que foram inseridos, deixando os outros como estão

> **DELETE**:	Exclui recursos existentes

Utilizar código de status http para respostas da api.

> [`200`](https://httpstatuses.com/200) OK - Resposta para um GET, PUT, PATCH ou DELETE que foi bem sucedido. Serve para POST que não resultou em uma criação de um objeto novo.

> [`201`](https://httpstatuses.com/201) Created - Resposta para um POST bem sucedido que resultou em um objeto criado. Deve ser acompanhado por um header contendo a url do novo objeto criado.

> [`204`](https://httpstatuses.com/204) No Content - Reposta para uma requisição bem sucedida que não retorna informação no body.

> [`304`](https://httpstatuses.com/304) Not Modified - Usado quando o cache entrou em ação e não houve necessidade do servidor enviar uma resposta que já é valida pelo cliente, equivalente ao 200 em que o retorno foi feito pelo cache.

> [`400`](https://httpstatuses.com/400) Bad Request - A requisição está mal formada, por exemplo: se o conteúdo do body não pode ser interpretado.

> [`401`](https://httpstatuses.com/401) Unauthorized - Quando a autenticação de usuário falhou ou não havia dados de autenticação.

> [`403`](https://httpstatuses.com/403) Forbidden - Quanto a antenticação foi bem sucedida mas o usuário autenticado não possui  acesso ao recurso.

> [`404`](https://httpstatuses.com/404) Not Found - Quando a requisição não encontra o recurso.

> [`405`](https://httpstatuses.com/405) Method Not Allowed - Quando um usuário não possui acesso ao método HTTP que está sendo usado.

> [`410`](https://httpstatuses.com/410) Gone - Indica que o recurso nesse endpoint não está mais disponível. Útil como resposta de endpoints que já foram depreciados.

> [`415`](https://httpstatuses.com/415) Unsupported Media Type - Se o content-type informado na request for incorreto

> [`422`](https://httpstatuses.com/422) Unprocessable Entity - Quando ocorre um erro de validação do objeto.

> [`429`](https://httpstatuses.com/429) Too Many Requests - Quando uma request é rejeitada porque a quantidade de requests atingiu o limite.

---
Estas diretrizes foram baseadas em [wearehive/project-guidelines](https://github.com/wearehive/project-guidelines).
