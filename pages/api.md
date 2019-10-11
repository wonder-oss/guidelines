## 6. API

![API](/images/pages/api.png)

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
