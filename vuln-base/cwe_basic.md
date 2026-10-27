# CWE Common Weakness Enumeration

CWE significa Common Weakness Enumeration (ou Enumeração de Fraquezas Comuns). É uma lista padronizada que cataloga falhas de segurança subjacentes em arquitetura, design, código ou configuração de softwares e hardwares. 
O projeto é mantido pela organização sem fins lucrativos MITRE Corporation em colaboração com a comunidade global de cibersegurança. 

### Principais características dos CWEs

• __Não são vulnerabilidades reais:__ O CWE define a causa raiz ou o tipo de fraqueza (por exemplo, um erro de lógica ou falha na validação de entrada), e não um problema específico que está atacando um produto em um momento exato. 

• __Identificação numérica:__ Cada fraqueza recebe um código único. Um exemplo clássico é o CWE-79, que representa falhas de Cross-Site Scripting (XSS). 

• __Foco preventivo:__ Ajuda programadores e equipes de DevSecOps a escreverem código seguro desde a concepção, identificando padrões de risco antes que eles virem brechas reais. 


### CWE vs. Outras Súmulas da Cibersegurança

Para entender o ecossistema de cibersegurança, é comum confundir as siglas. A diferença básica funciona assim:

• __CWE (A Fraqueza):__ A fraqueza conceitual ou o erro de programação subjacente (ex: falta de validação de dados).

• __CVE (A Vulnerabilidade):__ O registro público de uma falha real e específica descoberta em um software de um fornecedor específico (ex: uma falha em uma versão exata de um leitor de PDF). Uma CVE geralmente está associada a um ou mais CWEs.

• __CVSS (A Pontuação):__ O sistema de notas que mede a gravidade (de 0 a 10) de uma CVE.

• __CAPEC (O Ataque):__ Catálogo que descreve como um invasor tenta explorar fraquezas (os padrões de ataque). 


### Como consultar a base oficial de fraquezas da MITRE?

Para consultar a base oficial de fraquezas da MITRE, você deve acessar o site oficial do CWE. O catálogo é público, gratuito e atualizado regularmente. 

[CWE Mitre Org](https://cwe.mitre.org/) 

[CWE Mitre About](https://cwe.mitre.org/about/index.html)

A plataforma oferece três formas principais para você explorar os dados de maneira eficiente:

1. **Busca Direta (Por ID ou Palavra-chave)**

Se você já sabe o número da fraqueza ou o nome do termo que está procurando, use os mecanismos de busca rápida:

• __ID Lookup:__ No canto superior direito da página inicial, há um campo de busca por identificador. Digite o número (ex: 79 ou CWE-79) para ir direto à página explicativa. 

[CWE Mitre](https://cwe.mitre.org/)

[CWE Lookup](https://inventivehq.com/tools/security/cwe-lookup)

• __Busca por Termos:__ Acesse a página de Busca do Site do CWE para digitar palavras-chave como "SQL Injection" ou "Buffer Overflow" e encontrar as fraquezas correspondentes. 

[CWE Find](https://cwe.mitre.org/find/index.html)

2. **Navegação por "Visões" (Views)**

A MITRE organiza as centenas de fraquezas catalogadas em diferentes "perspectivas" para facilitar o estudo, acessíveis através da seção CWE List Data. As visões mais utilizadas são:

• __Software Development (Desenvolvimento de Software):__ Organiza as falhas com base em conceitos de programação e nas fases do ciclo de vida do código. 

• __Hardware Design (Design de Hardware):__ Focada em vulnerabilidades físicas de circuitos, processadores e firmwares. 

• __Research Concepts (Conceitos de Pesquisa):__ Uma visão estritamente teórica e acadêmica, estruturada por comportamentos de abstração do sistema. 

[CWE Data](https://cwe.mitre.org/data/index.html)

3. **Listas Temáticas e Mapeamentos Externos**

Se o seu objetivo é priorizar o aprendizado ou focar nos maiores riscos do mercado, você pode consultar as seleções da aba **Top-N Lists / Scoring:** 

• __CWE Top 25:__ A lista anual que reúne os 25 erros de programação mais perigosos, frequentes e fáceis de explorar no mundo.

• __Filtros por Linguagem:__ É possível filtrar as falhas que afetam especificamente ecossistemas como C, C++, Java e PHP.

• __Mapeamento OWASP:__ Cruzamento direto do catálogo com frameworks famosos, como o OWASP Top 10. 

[CWE Scoring](https://cwe.mitre.org/scoring/index.html)


### O que você encontra em cada registro?

Ao abrir a página de um CWE específico (como o CWE-89 de Injeção de SQL), a MITRE disponibiliza uma ficha técnica profunda: 

• Descrição teórica e o nível de abstração da falha.

• Exemplos de código demonstrativo (mostrando o trecho vulnerável e a sua respectiva correção).

• Métodos de detecção (como encontrar a falha via análise estática ou testes de invasão).

• Táticas de mitigação para guiar os desenvolvedores em como blindar o sistema. 
