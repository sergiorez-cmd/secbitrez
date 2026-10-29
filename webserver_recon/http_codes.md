# Referência Completa de Códigos de Status HTTP

Os códigos de status HTTP são respostas padronizadas emitidas pelos servidores web para indicar o resultado do processamento de uma requisição feita pelo cliente. Essas respostas estruturam a comunicação na web e são categorizadas em cinco classes principais indicadas pelo primeiro dígito do código (1xx a 5xx).

---

## 1. Visão Geral das Classes de Status HTTP

A tabela a seguir apresenta as cinco famílias fundamentais de códigos de status HTTP e seu propósito geral na arquitetura da web:

| Classe | Categoria | Descrição Geral |
| :--- | :--- | :--- |
| **1xx** | Informacional | Indica que a requisição foi recebida e o processo continua em andamento. |
| **2xx** | Sucesso | Indica que a ação solicitada pelo cliente foi recebida, compreendida e aceita com êxito. |
| **3xx** | Redirecionamento | Indica que ações adicionais precisam ser tomadas pelo cliente para concluir a requisição. |
| **4xx** | Erro do Cliente | Indica que a requisição contém sintaxe incorreta ou não pode ser processada pelo servidor. |
| **5xx** | Erro do Servidor | Indica que o servidor falhou ao tentar processar uma requisição aparentemente válida. |

---

## 2. Tabela Consolidada de Códigos de Status HTTP

A tabela abaixo compila todos os códigos de status HTTP disponibilizados na referência, organizados em ordem numérica:

| Código | Nome Original | Categoria | Descrição |
| :--- | :--- | :--- | :--- |
| **100** | Continue | 1xx Informacional | O servidor recebeu os cabeçalhos da requisição e o cliente deve prosseguir com o envio do corpo da mensagem. |
| **101** | Switching Protocols | 1xx Informacional | O servidor aceitou a solicitação do cliente para trocar o protocolo de comunicação. |
| **102** | Processing | 1xx Informacional | O servidor recebeu e está processando a requisição, mas ainda não há resposta disponível (WebDAV). |
| **103** | Early Hints | 1xx Informacional | Utilizado para retornar alguns cabeçalhos de resposta antes da resposta final completa. |
| **200** | OK | 2xx Sucesso | A requisição foi bem-sucedida e o servidor retornou os dados solicitados. |
| **201** | Created | 2xx Sucesso | A requisição foi concluída com êxito e um novo recurso foi criado no servidor. |
| **202** | Accepted | 2xx Sucesso | A requisição foi aceita para processamento, mas o processamento ainda não foi concluído. |
| **203** | Non-Authoritative Information | 2xx Sucesso | A requisição foi bem-sucedida, mas as informações retornadas derivam de uma cópia em cache. |
| **204** | No Content | 2xx Sucesso | A requisição foi processada com sucesso, mas não há conteúdo a ser retornado no corpo da resposta. |
| **205** | Reset Content | 2xx Sucesso | O servidor processou a requisição e solicita que o cliente redefina a visualização do documento. |
| **206** | Partial Content | 2xx Sucesso | O servidor está entregando apenas parte do recurso devido a um cabeçalho de intervalo (*range request*) enviado pelo cliente. |
| **207** | Multi-Status | 2xx Sucesso | Transmite informações sobre múltiplos recursos em situações onde várias operações podem ter ocorrido (WebDAV). |
| **208** | Already Reported | 2xx Sucesso | Os membros de uma listagem WebDAV já foram enumerados em uma resposta anterior. |
| **300** | Multiple Choices | 3xx Redirecionamento | A requisição possui mais de uma resposta possível e o cliente deve escolher uma delas. |
| **301** | Moved Permanently | 3xx Redirecionamento | O recurso solicitado foi movido permanentemente para uma nova URL. |
| **302** | Found | 3xx Redirecionamento | O recurso solicitado reside temporariamente sob uma URL diferente. |
| **303** | See Other | 3xx Redirecionamento | A resposta para a requisição pode ser encontrada em outra URL utilizando o método GET. |
| **304** | Not Modified | 3xx Redirecionamento | O recurso não foi modificado desde a última requisição, permitindo o uso da versão em cache. |
| **307** | Temporary Redirect | 3xx Redirecionamento | A requisição deve ser repetida em outra URL mantendo o mesmo método HTTP original. |
| **308** | Permanent Redirect | 3xx Redirecionamento | O recurso foi movido permanentemente para outra URL, exigindo a manutenção do mesmo método HTTP. |
| **400** | Bad Request | 4xx Erro do Cliente | O servidor não pode processar a requisição devido a um erro do cliente (sintaxe inválida, etc.). |
| **401** | Unauthorized | 4xx Erro do Cliente | A autenticação é necessária e falhou ou não foi fornecida pelo cliente. |
| **402** | Payment Required | 4xx Erro do Cliente | Código reservado para uso futuro relacionado a pagamentos digitais. |
| **403** | Forbidden | 4xx Erro do Cliente | O servidor entendeu a requisição, mas se recusa a autorizar o acesso ao recurso. |
| **404** | Not Found | 4xx Erro do Cliente | O recurso solicitado não pôde ser encontrado no servidor. |
| **405** | Method Not Allowed | 4xx Erro do Cliente | O método de requisição utilizado não é suportado pelo recurso solicitado. |
| **406** | Not Acceptable | 4xx Erro do Cliente | O recurso não consegue gerar conteúdo compatível com os cabeçalhos de aceitação (*Accept*) enviados. |
| **407** | Proxy Authentication Required | 4xx Erro do Cliente | O cliente deve se autenticar previamente junto a um proxy de rede. |
| **408** | Request Timeout | 4xx Erro do Cliente | O servidor esgotou o tempo de espera pelo envio da requisição por parte do cliente. |
| **409** | Conflict | 4xx Erro do Cliente | A requisição não pôde ser concluída devido a um conflito com o estado atual do recurso. |
| **410** | Gone | 4xx Erro do Cliente | O recurso solicitado não está mais disponível e não voltará a estar disponível novamente. |
| **411** | Length Required | 4xx Erro do Cliente | O servidor exige a especificação do cabeçalho *Content-Length* para processar a requisição. |
| **412** | Precondition Failed | 4xx Erro do Cliente | Uma ou mais pré-condições presentes nos cabeçalhos da requisição foram avaliadas como falsas. |
| **413** | Payload Too Large | 4xx Erro do Cliente | A entidade da requisição é maior do que os limites que o servidor está disposto a processar. |
| **414** | URI Too Long | 4xx Erro do Cliente | A URI fornecida na requisição é mais longa do que o servidor consegue interpretar. |
| **415** | Unsupported Media Type | 4xx Erro do Cliente | O formato de mídia dos dados enviados na requisição não é suportado pelo servidor. |
| **416** | Range Not Satisfiable | 4xx Erro do Cliente | O intervalo especificado no cabeçalho *Range* não pode ser satisfeito pelo recurso. |
| **417** | Expectation Failed | 4xx Erro do Cliente | A expectativa indicada no cabeçalho *Expect* não pôde ser cumprida pelo servidor. |
| **418** | I'm a Teapot | 4xx Erro do Cliente | O servidor se recusa a passar café porque é um bule de chá (definido na RFC 2324). |
| **422** | Unprocessable Entity | 4xx Erro do Cliente | A requisição estava bem formatada, mas continha erros semânticos (WebDAV). |
| **425** | Too Early | 4xx Erro do Cliente | O servidor não está disposto a arriscar o processamento de uma requisição que possa ser repetida. |
| **426** | Upgrade Required | 4xx Erro do Cliente | O servidor se recusa a processar a requisição com o protocolo atual e exige uma atualização (*upgrade*). |
| **428** | Precondition Required | 4xx Erro do Cliente | O servidor exige que a requisição seja condicional para evitar conflitos de atualização. |
| **429** | Too Many Requests | 4xx Erro do Cliente | O cliente enviou muitas requisições em um determinado período de tempo (*rate limiting*). |
| **431** | Request Header Fields Too Large | 4xx Erro do Cliente | O servidor se recusa a processar a requisição porque os campos de cabeçalho são muito grandes. |
| **451** | Unavailable For Legal Reasons | 4xx Erro do Cliente | O acesso ao recurso foi bloqueado por motivos legais ou regulatórios. |
| **500** | Internal Server Error | 5xx Erro do Servidor | O servidor encontrou uma condição inesperada que o impediu de atender à requisição. |
| **501** | Not Implemented | 5xx Erro do Servidor | O servidor não suporta a funcionalidade necessária para concluir a requisição. |
| **502** | Bad Gateway | 5xx Erro do Servidor | O servidor, atuando como gateway ou proxy, recebeu uma resposta inválida do servidor upstream. |
| **503** | Service Unavailable | 5xx Erro do Servidor | O servidor está temporariamente indisponível (sobrecarregado ou em manutenção). |
| **504** | Gateway Timeout | 5xx Erro do Servidor | O servidor, atuando como gateway ou proxy, não recebeu uma resposta a tempo do servidor upstream. |
| **505** | HTTP Version Not Supported | 5xx Erro do Servidor | O servidor não suporta a versão do protocolo HTTP utilizada na requisição. |
| **507** | Insufficient Storage | 5xx Erro do Servidor | O servidor não possui espaço de armazenamento suficiente para concluir a requisição (WebDAV). |
| **508** | Loop Detected | 5xx Erro do Servidor | O servidor detectou um loop infinito ao processar a requisição (WebDAV). |
| **511** | Network Authentication Required | 5xx Erro do Servidor | O cliente precisa se autenticar para obter acesso à rede antes de enviar a requisição. |

---

## 3. Detalhamento por Categoria

### 3.1 Respostas Informacionais (1xx)

As respostas informacionais indicam uma transferência provisória de estado antes de a resposta definitiva ser enviada.

| Código | Nome Original | Descrição Resumida |
| :--- | :--- | :--- |
| **100** | Continue | Cliente autorizado a continuar o envio do corpo da requisição. |
| **101** | Switching Protocols | Mudança de protocolo aprovada pelo servidor. |
| **102** | Processing | Requisição WebDAV sendo processada. |
| **103** | Early Hints | Pré-carregamento de cabeçalhos de resposta. |

### 3.2 Respostas de Sucesso (2xx)

Códigos da classe 2xx confirmam que a operação solicitada foi realizada conforme o esperado.

| Código | Nome Original | Descrição Resumida |
| :--- | :--- | :--- |
| **200** | OK | Requisição executada com sucesso. |
| **201** | Created | Novo recurso criado com sucesso. |
| **202** | Accepted | Requisição aceita para processamento assíncrono. |
| **203** | Non-Authoritative Information | Resposta retornada a partir de fonte em cache. |
| **204** | No Content | Operação concluída sem corpo de resposta. |
| **205** | Reset Content | Solicitado o reajuste da interface do usuário. |
| **206** | Partial Content | Entrega parcial de conteúdo por faixa de bytes. |
| **207** | Multi-Status | Status de múltiplas operações (WebDAV). |
| **208** | Already Reported | Elementos repetidos já reportados em WebDAV. |

### 3.3 Respostas de Redirecionamento (3xx)

Indicam que o cliente deve realizar novas requisições para acessar o recurso desejado.

| Código | Nome Original | Descrição Resumida |
| :--- | :--- | :--- |
| **300** | Multiple Choices | Diversas opções de resposta disponíveis. |
| **301** | Moved Permanently | Recurso movido permanentemente para outro local. |
| **302** | Found | Recurso encontrado temporariamente em outra URL. |
| **303** | See Other | Redirecionamento utilizando método GET. |
| **304** | Not Modified | Conteúdo inalterado; utilizar versão em cache. |
| **307** | Temporary Redirect | Redirecionamento temporário mantendo método HTTP. |
| **308** | Permanent Redirect | Redirecionamento permanente mantendo método HTTP. |

### 3.4 Respostas de Erro do Cliente (4xx)

Sinalizam que o problema na requisição originou-se do lado do cliente.

| Código | Nome Original | Descrição Resumida |
| :--- | :--- | :--- |
| **400** | Bad Request | Erro de sintaxe ou estrutura da requisição. |
| **401** | Unauthorized | Credenciais de autenticação ausentes ou inválidas. |
| **402** | Payment Required | Reservado para sistemas de pagamento futuro. |
| **403** | Forbidden | Acesso negado mesmo com autenticação. |
| **404** | Not Found | Recurso não localizado no servidor. |
| **405** | Method Not Allowed | Método HTTP não suportado pelo endpoint. |
| **406** | Not Acceptable | Formato de resposta incompatível com o cliente. |
| **407** | Proxy Authentication Required | Autenticação necessária no proxy intermediário. |
| **408** | Request Timeout | Tempo limite de requisição excedido pelo cliente. |
| **409** | Conflict | Conflito com o estado atual do recurso. |
| **410** | Gone | Recurso permanentemente removido. |
| **411** | Length Required | Cabeçalho Content-Length obrigatório ausente. |
| **412** | Precondition Failed | Falha em pré-condição declarada nos cabeçalhos. |
| **413** | Payload Too Large | Corpo da requisição excede o limite aceito. |
| **414** | URI Too Long | URL excede o tamanho máximo suportado. |
| **415** | Unsupported Media Type | Tipo de mídia enviada não suportado. |
| **416** | Range Not Satisfiable | Intervalo de bytes solicitado fora do limite do arquivo. |
| **417** | Expectation Failed | Servidor incapaz de cumprir o cabeçalho Expect. |
| **418** | I'm a Teapot | Servidor é um bule de chá (RFC 2324). |
| **422** | Unprocessable Entity | Erro semântico na requisição (WebDAV). |
| **425** | Too Early | Risco de replay attack no processamento. |
| **426** | Upgrade Required | Protocolo atual rejeitado; atualização exigida. |
| **428** | Precondition Required | Requisição condicional obrigatória. |
| **429** | Too Many Requests | Excesso de requisições enviadas (Rate limit). |
| **431** | Request Header Fields Too Large | Cabeçalhos HTTP excedem limite do servidor. |
| **451** | Unavailable For Legal Reasons | Conteúdo bloqueado devido a restrições legais. |

### 3.5 Respostas de Erro do Servidor (5xx)

Sinalizam falhas internas do próprio servidor ao tentar processar requisições válidas.

| Código | Nome Original | Descrição Resumida |
| :--- | :--- | :--- |
| **500** | Internal Server Error | Falha genérica interna no servidor. |
| **501** | Not Implemented | Recurso ou método não implementado. |
| **502** | Bad Gateway | Resposta inválida recebida de gateway/proxy upstream. |
| **503** | Service Unavailable | Servidor temporariamente inoperante ou sobrecarregado. |
| **504** | Gateway Timeout | Tempo limite esgotado ao aguardar servidor upstream. |
| **505** | HTTP Version Not Supported | Versão do protocolo HTTP não suportada. |
| **507** | Insufficient Storage | Espaço em disco insuficiente no servidor (WebDAV). |
| **508** | Loop Detected | Loop infinito identificado no servidor (WebDAV). |
| **511** | Network Authentication Required | Autenticação na rede exigida antes de acessar o recurso. |
