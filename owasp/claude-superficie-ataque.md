# Mapa Mental de Superfície de Ataque do Juice-Shop

__Prompt =__ ```Crie um mapa mental da superfície de ataque externa para uma empresa que usa [AWS, Express, Angular, Node.js, SQLite]. Liste vetores de ataque prováveis, desde o CDN até o banco de dados, identificando pontos de falha comuns em cada camada.```

Usei o stack do seu exemplo (AWS, Express, Angular, Node.js). Se o real for diferente, me diga e eu adapto.

## Mapa mental: superfície de ataque externa

```
EMPRESA (superfície externa)
│
├── 1. DNS e DOMÍNIOS (Route 53)
│   ├── Subdomain takeover (CNAME apontando para recurso removido: S3, CloudFront, Elastic Beanstalk)
│   ├── Zonas com registros esquecidos (staging, dev, admin, VPN)
│   ├── Domínio expirado ou sem lock / registrar sem MFA
│   └── SPF/DKIM/DMARC fracos → spoofing de e-mail e phishing
│
├── 2. CDN e BORDA (CloudFront)
│   ├── Origem exposta: ALB/EC2/S3 acessível direto, contornando CDN e WAF
│   ├── Cache poisoning / cache deception (headers não incluídos na cache key)
│   ├── Bucket S3 de origem público ou com política permissiva
│   ├── Falta de HSTS, TLS antigo, certificados mal gerenciados
│   └── Signed URLs/cookies com validade longa ou sem escopo
│
├── 3. WAF e BALANCEADOR (AWS WAF, ALB/NLB)
│   ├── Regras em modo "count" e nunca promovidas a "block"
│   ├── Bypass por diferenças de parsing (encoding, content-type, HTTP smuggling)
│   ├── Security groups abertos (0.0.0.0/0) em portas administrativas
│   ├── Listeners HTTP sem redirecionamento / headers internos confiados
│   └── Sem rate limiting → brute force, scraping, DoS de camada 7
│
├── 4. FRONTEND (Angular / SPA)
│   ├── Segredos e chaves no bundle JS (API keys, endpoints internos, flags)
│   ├── XSS via bypassSecurityTrust*, innerHTML, bibliotecas de terceiros
│   ├── Tokens em localStorage (roubáveis via XSS)
│   ├── Source maps publicados em produção
│   ├── Controle de acesso só no cliente (route guards ≠ autorização)
│   └── CSP ausente/permissiva, scripts de terceiros sem SRI
│
├── 5. API (Express / Node.js)
│   ├── Autenticação e autorização
│   │   ├── BOLA/IDOR (acessar objetos de outros usuários pelo ID)
│   │   ├── BFLA (funções administrativas acessíveis a usuários comuns)
│   │   ├── JWT mal validado (alg none, segredo fraco, sem expiração/revogação)
│   │   └── Mass assignment (req.body direto no modelo)
│   ├── Validação de entrada
│   │   ├── Injeção NoSQL/SQL/comando (operadores $ne, $gt no Mongo; concatenação em queries)
│   │   ├── SSRF (fetch de URL fornecida pelo usuário → metadata da AWS)
│   │   ├── Path traversal e upload inseguro (tipo, tamanho, destino)
│   │   ├── Prototype pollution (merge/extend de objetos não confiáveis)
│   │   └── ReDoS e payloads gigantes (sem limite de body)
│   ├── Configuração
│   │   ├── CORS permissivo (origin refletido, credentials: true)
│   │   ├── Sem helmet/headers de segurança; x-powered-by exposto
│   │   ├── Stack traces e erros detalhados em produção
│   │   └── Endpoints esquecidos: /debug, /metrics, /swagger, /graphql introspection
│   └── Lógica de negócio: race conditions, abuso de fluxos (cupons, reset de senha, OTP sem limite)
│
├── 6. IDENTIDADE E SESSÃO (Cognito / Auth própria / OAuth)
│   ├── Credential stuffing e enumeração de usuários
│   ├── Reset de senha e MFA com fluxos contornáveis
│   ├── OAuth: redirect_uri frouxo, state ausente
│   └── Cookies sem Secure/HttpOnly/SameSite
│
├── 7. COMPUTE (EC2 / ECS / EKS / Lambda)
│   ├── Instância com IMDSv1 → roubo de credenciais via SSRF
│   ├── Imagens de container desatualizadas, rodando como root
│   ├── Portas de gestão expostas (SSH, Docker API, Kubernetes dashboard)
│   ├── Variáveis de ambiente com segredos em texto claro
│   ├── Lambda com role IAM excessiva ou event injection
│   └── Falta de patching de SO e runtime Node.js (versões EOL)
│
├── 8. CADEIA DE SUPRIMENTOS (npm e dependências)
│   ├── Pacotes vulneráveis (npm audit ignorado)
│   ├── Typosquatting e dependency confusion (pacotes internos sem escopo)
│   ├── Scripts postinstall maliciosos, mantenedores comprometidos
│   └── Lockfile ausente ou não respeitado no CI
│
├── 9. DADOS (RDS / DynamoDB / S3 / ElastiCache)
│   ├── Banco com IP público ou security group amplo
│   ├── S3 com ACL/política pública, listagem aberta, sem bloqueio de acesso público
│   ├── Credenciais do banco compartilhadas e sem rotação
│   ├── Sem criptografia em repouso/trânsito; snapshots públicos
│   ├── Redis/Memcached sem autenticação
│   └── Backups sem controle de acesso, logs com dados sensíveis (PII, tokens)
│
├── 10. PLANO DE CONTROLE AWS (IAM e contas)
│   ├── Chaves de acesso de longa duração vazadas (repositórios, front, CI)
│   ├── Roles com "*:*" e confiança cruzada excessiva
│   ├── Root sem MFA, usuários sem MFA, sem SCPs
│   ├── CloudTrail/GuardDuty desativados ou sem alertas
│   └── Escalada de privilégio (iam:PassRole, políticas editáveis)
│
├── 11. CI/CD E CÓDIGO (GitHub/GitLab, pipelines)
│   ├── Segredos em histórico do Git, em logs de build ou em variáveis expostas
│   ├── Runners com permissões amplas; PRs de forks executando workflows
│   ├── Artefatos e registries sem controle de acesso
│   └── Contas de desenvolvedores sem MFA / tokens pessoais antigos
│
└── 12. TERCEIROS E FATOR HUMANO
    ├── Webhooks sem verificação de assinatura
    ├── SaaS integrados (analytics, suporte, pagamentos) com acesso excessivo
    ├── Phishing e engenharia social contra o time e o suporte
    └── Shadow IT: ambientes de teste esquecidos na internet
```

## Onde costuma doer mais

Pela frequência em incidentes reais, eu priorizaria nesta ordem:

1. **Autorização quebrada na API** (IDOR/BOLA), o problema mais comum e de maior impacto.
2. **Segredos expostos** (chaves AWS no código, no bundle ou no CI) combinados com IAM permissivo.
3. **SSRF + IMDSv1**, que transforma uma falha de aplicação em acesso à conta AWS.
4. **Buckets e bancos com exposição pública** por configuração errada.
5. **Origem acessível sem passar por CDN/WAF**, que anula as proteções de borda.
6. **Dependências npm** desatualizadas ou comprometidas.

## Como usar isso na prática

- **Descoberta:** inventarie ativos externos (subdomínios, IPs, buckets, portas) e compare com o que você *acha* que está exposto.
- **Verificação:** use os itens como checklist de revisão de arquitetura, junto com o OWASP API Security Top 10 e o CIS Benchmark da AWS.
- **Priorização:** cruze cada item com o impacto (dados sensíveis? acesso à conta?) e a facilidade de exploração.
- **Evidência:** teste apenas ambientes que você é autorizado a avaliar.

Se quiser, posso transformar isso em um modelo STRIDE por camada, em um checklist de verificação com comandos de auditoria (AWS CLI, Prowler, ScoutSuite), ou ajustar para o seu stack real.

# Modelo STRIDE: AWS + Express + Angular + Node.js

**Legenda:** **S**poofing (falsificação de identidade) · **T**ampering (adulteração) · **R**epudiation (repúdio) · **I**nformation disclosure (vazamento) · **D**enial of service (negação de serviço) · **E**levation of privilege (elevação de privilégio)

## Fronteiras de confiança

```
[Internet] ─┬─► [DNS/CDN/WAF] ─► [ALB] ─► [Express/Node em ECS/EC2/Lambda] ─► [RDS/DynamoDB/S3]
            │         ▲                              │
[Navegador: Angular]──┘                              └─► [APIs de terceiros / IMDS / IAM]
[Dev/CI/CD] ─────────────► [Registry/Repo] ─────────► [Deploy na conta AWS]
```

Cada seta que cruza uma fronteira (Internet → borda, borda → app, app → dados, CI → produção) é um ponto onde as ameaças abaixo precisam de um controle explícito.

## 1. Borda (DNS, CloudFront, WAF, ALB)

| Cat. | Ameaça | Mitigação |
|---|---|---|
| S | Subdomain takeover; spoofing de e-mail do domínio | Auditar CNAMEs órfãos; SPF/DKIM/DMARC com `p=reject` |
| T | Cache poisoning; manipulação de headers (smuggling) | Cache key explícita; normalizar headers; ALB com `drop_invalid_header_fields` |
| R | Sem logs de acesso na borda | Logs do CloudFront, WAF e ALB em S3 com retenção e imutabilidade |
| I | Origem exposta; certificados e versões de TLS fracos | Restringir origem ao CloudFront (managed prefix list + header secreto); TLS 1.2+ |
| D | Flood L7, sem rate limit | Rate-based rules no WAF, Shield, cache agressivo |
| E | Regras do WAF em `count`; SG com `0.0.0.0/0` em portas de gestão | Promover regras para `block`; revisar security groups |

## 2. Frontend (Angular)

| Cat. | Ameaça | Mitigação |
|---|---|---|
| S | Phishing com clone do site; OAuth com `redirect_uri` frouxo | Allowlist exata de redirects; `state` e PKCE |
| T | XSS (`bypassSecurityTrust*`, `innerHTML`); script de terceiro comprometido | CSP restritiva, SRI, evitar bypass do sanitizer |
| R | Ações críticas sem confirmação ou trilha | Registrar no backend com ID do usuário e timestamp |
| I | Segredos no bundle; source maps em produção; token em `localStorage` | Nada sensível no cliente; desativar source maps; cookies `HttpOnly` |
| D | Loops/consultas pesadas disparados pelo cliente | Paginação e limites impostos no servidor |
| E | Route guards tratados como autorização | Autorização sempre reaplicada na API |

## 3. API (Express / Node.js)

| Cat. | Ameaça | Mitigação |
|---|---|---|
| S | JWT mal validado (`alg:none`, segredo fraco); confiar em `X-Forwarded-For` ou headers internos | Fixar algoritmo, validar `iss/aud/exp`, configurar `trust proxy` corretamente |
| T | Injeção SQL/NoSQL; mass assignment; prototype pollution; path traversal | Queries parametrizadas; schemas (Zod/Joi) com allowlist de campos; bloquear `__proto__` |
| R | Logs sem correlação ou que aceitam input do usuário (log injection) | Logs estruturados com request ID e identidade; sanitizar entrada |
| I | IDOR/BOLA; stack traces; CORS permissivo; `/swagger`, `/debug`, `/metrics` abertos | Checagem de propriedade por objeto; erros genéricos; CORS com allowlist; proteger ou remover endpoints internos |
| D | ReDoS; body gigante; upload sem limite; operações sem timeout | Limites de body, timeouts, rate limit por usuário/IP, validar regex |
| E | BFLA (função admin acessível); SSRF → IMDS → credenciais | RBAC/ABAC no servidor; allowlist de destinos em requests de saída; **IMDSv2 obrigatório** |

## 4. Identidade e sessão

| Cat. | Ameaça | Mitigação |
|---|---|---|
| S | Credential stuffing; sessão roubada; fluxo de reset contornável | MFA, detecção de credenciais vazadas, tokens de reset de uso único e curta duração |
| T | Fixação de sessão; alteração de claims | Rotacionar sessão no login; assinar e validar tokens |
| R | Falta de auditoria de login, reset e mudança de MFA | Eventos de autenticação imutáveis e com alerta |
| I | Enumeração de usuários por mensagens ou tempo de resposta | Respostas uniformes; limitar tentativas |
| D | Bloqueio de contas por tentativas forçadas | Lockout progressivo com CAPTCHA em vez de bloqueio rígido |
| E | Auto-registro com papel privilegiado; troca de e-mail sem reautenticar | Papéis atribuídos só no servidor; reautenticação em ações sensíveis |

## 5. Compute (ECS/EKS/EC2/Lambda)

| Cat. | Ameaça | Mitigação |
|---|---|---|
| S | Roubo de credenciais da task/instância via metadata | IMDSv2, hop limit 1, roles por serviço |
| T | Imagem adulterada ou desatualizada; Node.js em EOL | Assinatura e scan de imagens (ECR), patching, runtime suportado |
| R | Sem logs de runtime e de acesso ao host | CloudWatch/Falco, SSM Session Manager em vez de SSH |
| I | Segredos em variáveis de ambiente e imagens | Secrets Manager/SSM Parameter Store, injeção em runtime |
| D | Sem limites de CPU/memória; autoscaling sem teto | Limits/quotas, budgets e alarmes |
| E | Container como root; role com `*`; portas de gestão expostas | Usuário não-root, filesystem read-only, menor privilégio, sem portas de gestão públicas |

## 6. Dados (RDS, DynamoDB, S3, ElastiCache)

| Cat. | Ameaça | Mitigação |
|---|---|---|
| S | Uso de credenciais compartilhadas do banco | Credenciais por serviço, IAM auth, rotação automática |
| T | Alteração direta de dados; bucket com escrita ampla | Princípio do menor privilégio, versionamento e Object Lock |
| R | Sem trilha de quem leu ou alterou dados | Audit logging (pgaudit, CloudTrail data events), logs centralizados |
| I | Banco ou bucket públicos; snapshots compartilhados; PII em logs; sem criptografia | Block Public Access, subnets privadas, KMS, TLS, mascarar dados em logs |
| D | Queries pesadas, conexões esgotadas, ransomware | Pool e timeouts, backups cross-account e imutáveis |
| E | App com usuário de banco `admin` | Usuário de aplicação com permissões mínimas por schema/tabela |

## 7. Plano de controle AWS (IAM)

| Cat. | Ameaça | Mitigação |
|---|---|---|
| S | Chaves de longa duração vazadas; root sem MFA | Roles temporárias (SSO/OIDC), MFA obrigatório, sem chaves estáticas |
| T | Alteração de políticas, CloudTrail ou Config | SCPs que protegem logs e guardrails, CloudTrail com validação de integridade |
| R | Auditoria desligada ou local | CloudTrail multi-região em conta de log separada |
| I | Políticas amplas permitindo listar e ler tudo | IAM Access Analyzer, escopo por recurso e condição |
| D | Exclusão de recursos ou do KMS key | SCPs, proteção contra deleção, MFA delete, backups em outra conta |
| E | `iam:PassRole`, `iam:*`, confiança cruzada excessiva | Permission boundaries, revisão de caminhos de escalada (Prowler/PMapper) |

## 8. CI/CD e cadeia de suprimentos

| Cat. | Ameaça | Mitigação |
|---|---|---|
| S | Token pessoal vazado; PR de fork rodando workflow com segredos | OIDC para a AWS, MFA, restringir workflows de forks |
| T | Dependência maliciosa; dependency confusion; lockfile ignorado | `npm ci`, pacotes com escopo, registry privado, SCA, revisão de `postinstall` |
| R | Deploys sem rastreabilidade | Branch protection, aprovações, assinatura de commits e artefatos |
| I | Segredos no histórico do Git e nos logs de build | Secret scanning, rotação imediata ao vazar, masking nos logs |
| D | Pipeline sabotado ou runners esgotados | Runners isolados, quotas, ambientes efêmeros |
| E | Runner ou role de deploy com admin | Roles de deploy com escopo mínimo, ambientes separados por conta |

## Priorização por risco

| Prioridade | Ameaça | Por quê |
|---|---|---|
| Crítica | SSRF → IMDS → credenciais (E, I) | Uma falha na aplicação vira acesso à conta AWS |
| Crítica | Segredos expostos + IAM amplo (S, E) | Vazamento simples, impacto total |
| Alta | IDOR/BOLA e BFLA na API (I, E) | Mais comum e fácil de explorar |
| Alta | Dados públicos por má configuração (I) | Exposição massiva sem exploit |
| Alta | Origem exposta, sem CDN/WAF (D, E) | Anula as defesas de borda |
| Média | Dependências npm e CI/CD (T) | Ataque indireto, mas de grande alcance |
| Média | Falta de logs e auditoria (R) | Não causa o incidente, mas impede detectá-lo e investigá-lo |

## Próximos passos

1. Desenhe o DFD real da sua aplicação e marque as fronteiras de confiança.
2. Para cada fluxo que cruza uma fronteira, valide os seis tipos de ameaça acima.
3. Registre as ameaças com dono, controle e status (ex.: no Jira ou em uma planilha).
4. Revise o modelo a cada mudança de arquitetura.

Se quiser, posso entregar isso como planilha (.xlsx) para acompanhamento, com colunas de risco, dono e status, ou como documento. Também posso detalhar um fluxo específico, como login ou upload de arquivos, em um DFD com STRIDE por elemento.
