# Deep-Hat Claude-Desktop

### Prompts para Enumerar Vetores de Ataque e Recomendações de Hardening
```text
Crie um mapa mental da superfície de ataque externa para uma empresa que usa [AWS, Express, Angular, Node.js, SQLite]. Liste vetores de ataque prováveis, desde o CDN até o banco de dados, identificando pontos de falha comuns em cada camada.
```
```text
Gere um checklist de hardening para uma instância EC2 rodando [Ubuntu 22.04 LTS] com [HTTPS, FTP, SSH]. Foque em: 1) Segurança de Rede (Security Groups, NACLs), 2) Gestão de Identidade e Acesso (IAM), 3) Monitoramento e Logs, e 4) Criptografia de dados em repouso e em trânsito.
```
### Prompts para Gerar Payloads SQLi. XSS e Shell Reverso
```text
Crie 3 variações de payloads para testar uma vulnerabilidade de SQL Injection em um campo de login que usa [BANCO_DE_DADOS SQLite]. Inclua técnicas de Boolean-blind, Time-based e Out-of-band, considerando que a aplicação filtra os caracteres 'OR' e 'AND'.
```
```text
Crie um documento Markdown completo e profissional, pronto para ser copiado para um Wiki, GitHub ou relatório.
Ele deve incluir:

    1-Título e Metadados
    2-Contexto (SQLite, filtros OR/AND)
    3-As 3 técnicas com payloads e explicações
    4-Tabela resumo
    5-Notas de implementação
    6-Gere o arquivo final limpo, pronto para salvar
```
```text
Crie 5 possíveis payloads para um ataque Cross-Site Scripting (XSS) DOM-based em uma aplicação que usa [FRAMEWORK, AngularJS]. O ataque deve ser capaz de exfiltrar cookies e tokens de sessão para um endpoint controlado pelo atacante, contornando filtros de HTML sanitizers comuns.
```
```text
Crie 3 variações de shell reverso para testar vulnerabilidade de execução de comando em servidores Linux. Inclua as seguintes linguagens de script [PHP, Python 3, Java].
```
