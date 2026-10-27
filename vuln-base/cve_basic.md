# CVE 

CVE significa Common Vulnerabilities and Exposures (Vulnerabilidades e Exposições Comuns). Trata-se de um catálogo ou glossário público que padroniza a identificação de falhas e brechas de segurança em softwares, sistemas operacionais e hardwares. 

### Como funciona um CVE

• __Identificador único:__ Quando uma falha é descoberta e validada, ela recebe um código único no formato CVE-AAAA-NNNNN (onde AAAA é o ano do registro e NNNNN é um número sequencial). Exemplo: CVE-2021-44228 (conhecida como Log4Shell). 

• __Padronização:__ Em vez de cada empresa ou pesquisador dar um nome diferente para o mesmo problema, o CVE cria uma linguagem universal para que o mercado de TI saiba exatamente de qual vulnerabilidade se está falando. 

• __Gestão:__ O programa foi criado em 1999 e é mantido pela MITRE Corporation, com o apoio de diversas autoridades de numeração (CNAs) e bases de dados como o National Vulnerability Database (NVD). 

### Para que servem?

• __Rastreamento:__ Permitem que softwares de escaneamento de segurança verifiquem se os sistemas da empresa possuem componentes desatualizados ou vulneráveis. 

• __Priorização:__ Geralmente são associados ao CVSS (Common Vulnerability Scoring System), um sistema que pontua a gravidade da falha de 0 a 10 para ajudar as equipes de tecnologia a decidirem o que corrigir primeiro. 

• __Correção (Patching):__ Facilitam a comunicação entre pesquisadores, fabricantes e administradores de sistemas para a criação e aplicação de atualizações de segurança. 

Você pode acompanhar os registros mais recentes e pesquisar falhas diretamente no Site Oficial do Programa CVE.

https://www.cve.org

CVE e CVSS são ferramentas complementares, mas com funções totalmente diferentes: enquanto o CVE serve para identificar uma falha, o CVSS serve para medir a gravidade dela.

Pense no CVE como a certidão de nascimento da vulnerabilidade e no CVSS como o boletim médico que diz a gravidade da doença.

### A diferença detalhada

| Característica	 | CVE (Common Vulnerabilities and Exposures) | CVSS (Common Vulnerability Scoring System) |

| --- | --- | --- |

| O que é? | 	Um identificador único (um nome/código).	| Um sistema de pontuação (uma nota). |

| Objetivo	| Responder: "Qual é a falha específica de que estamos falando?"	| Responder: "O quão urgente e perigosa é essa falha?" |

| Formato | Um código padrão, como CVE-2021-44228.	| Uma nota de 0.0 a 10.0 (junto com um vetor de texto). |

| Quem define?	| A MITRE Corporation e as CNAs autorizadas.	| O FIRST (Forum of Incident Response and Security Teams). |


### Como eles funcionam juntos na prática?

Quando um analista de segurança analisa a rede de uma empresa, ele usa os dois conceitos em conjunto:

• __Passo 1 (CVE):__ O scanner de segurança avisa: **"Encontrei a falha CVE-2023-XXXX no seu servidor web".**

• __Passo 2 (CVSS):__ O analista olha a nota CVSS atrelada àquele CVE. Se a nota for 9.8 (Crítica), ele para tudo o que está fazendo para corrigir o problema. Se a nota for 2.5 (Baixa), ele agenda a correção para a próxima janela de manutenção rotineira.

### As Faixas de Gravidade do CVSS

A nota do CVSS é dividida em faixas para facilitar a tomada de decisão:

• 0.0: Nenhuma (None)

• 0.1 – 3.9: Baixa (Low)

• 4.0 – 6.9: Média (Medium)

• 7.0 – 8.9: Alta (High)

• 9.0 – 10.0: Crítica (Critical)


