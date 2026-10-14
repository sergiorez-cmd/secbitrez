# Guia Básico: OWASP Top 10:2025

Este guia reúne as dez categorias de riscos de segurança de aplicações web mais críticas definidas pelo **OWASP Top 10:2025**, detalhando suas descrições, exemplos práticos de vulnerabilidades, a análise dos riscos mais críticos, além de seções dedicadas a **ferramentas de SCA / SBOM** e aos **riscos emergentes na cadeia de suprimentos de IA e LLMs**.

---

## 1. Visão Geral dos Riscos e Exemplos de Vulnerabilidades

### A01:2025 – Broken Access Control (Controle de Acesso Quebrado)
* **Descrição:** Ocorre quando as restrições sobre o que os usuários autenticados podem fazer não são devidamente aplicadas, permitindo que atuem fora de suas permissões pretendidas.
* **Exemplos de Vulnerabilidades:**
  * **IDOR (Insecure Direct Object Reference):** Alterar IDs na URL (ex: `/api/pedidos/1001` para `/api/pedidos/1002`) para acessar dados de outros usuários.
  * **Evasão de Controle de Acesso:** Acesso direto a URLs administrativas ou funções privilegiadas sem autenticação adequada.
  * **SSRF (Server-Side Request Forgery):** Redirecionamento indevido de requisições do servidor para recursos internos protegidos (categoria incorporada ao A01 em 2025).

### A02:2025 – Security Misconfiguration (Configuração Incorreta de Segurança)
* **Descrição:** Configurações de segurança deficientes, incompletas ou mantidas em padrões inseguros no sistema, servidores, contêineres ou ambiente em nuvem.
* **Exemplos de Vulnerabilidades:**
  * **Credenciais Padrão:** Manutenção de senhas ou chaves padrão ativas em componentes de software ou bancos de dados.
  * **Mensagens de Erro Verborrágicas:** Exibição de *stack traces* completos e detalhes internos do servidor em mensagens de erro enviadas ao usuário.
  * **Serviços Desnecessários Expostos:** Portas, serviços, páginas de exemplo ou recursos de teste mantidos ativos em ambiente de produção.

### A03:2025 – Software Supply Chain Failures (Falhas na Cadeia de Suprimentos de Software)
* **Descrição:** Fraquezas e comprometimentos em todo o ecossistema de software, incluindo aquisição de dependências, sistemas de *build* (CI/CD) e canais de distribuição.
* **Exemplos de Vulnerabilidades:**
  * **Dependências Vulneráveis ou Inseguras:** Uso de bibliotecas de terceiros desatualizadas ou sem manutenção.
  * **Ataques de Injeção de Pacotes Maliciosos:** Práticas de *typosquatting* ou *dependency confusion* em repositórios públicos (ex: npm, PyPI).
  * **Comprometimento do Pipeline de CI/CD:** Alteração não autorizada de código-fonte ou artefatos durante o processo automatizado de compilação.

### A04:2025 – Cryptographic Failures (Falhas Criptográficas)
* **Descrição:** Exposição de dados sensíveis (senhas, dados financeiros, PII) devido à ausência, fraco uso ou má gestão de criptografia.
* **Exemplos de Vulnerabilidades:**
  * **Tráfego em Texto Claro:** Transmissão de informações sensíveis via HTTP sem TLS/HTTPS.
  * **Algoritmos Obsoletos:** Uso de funções de hash ou criptografia fracas (ex: MD5, SHA-1, DES).
  * **Chaves Hardcoded:** Armazenamento de chaves criptográficas ou segredos diretamente no código-fonte.

### A05:2025 – Injection (Injeção)
* **Descrição:** Inclusão de dados não confiáveis que são interpretados pelo sistema como comandos ou consultas executáveis.
* **Exemplos de Vulnerabilidades:**
  * **SQL Injection (SQLi):** Concatenação de entradas de usuário em consultas SQL, permitindo leitura ou alteração indevida do banco de dados.
  * **Command Injection:** Execução de comandos do sistema operacional a partir de parâmetros fornecidos pelo usuário.
  * **Cross-Site Scripting (XSS):** Injeção de scripts maliciosos no navegador de outros usuários.

### A06:2025 – Insecure Design (Design Inseguro)
* **Descrição:** Falhas conceituais e estruturais na arquitetura do software e na lógica de negócios, originadas antes mesmo da escrita do código.
* **Exemplos de Vulnerabilidades:**
  * **Ausência de Rate Limiting:** Lógica de negócios que permite chamadas ilimitadas (ex: automação de compras ou consultas em massa).
  * **Recuperação de Senha Insegura:** Processo de redefinição de credenciais baseado em perguntas secretas previsíveis sem validação robusta.

### A07:2025 – Authentication Failures (Falhas de Autenticação)
* **Descrição:** Deficiências na confirmação da identidade do usuário, gerenciamento de sessões ou proteção contra automação.
* **Exemplos de Vulnerabilidades:**
  * **Ataques de Força Bruta / Credential Stuffing:** Ausência de bloqueio de conta ou CAPTCHA após múltiplas tentativas de login.
  * **Gestão Inadequada de Sessão:** Tokens de sessão válidos por tempo indeterminado ou que não expiram após o *logout*.

### A08:2025 – Software or Data Integrity Failures (Falhas de Integridade de Software ou Dados)
* **Descrição:** Aplicações que confiam em código, atualizações ou objetos serializados sem validar sua procedência e integridade.
* **Exemplos de Vulnerabilidades:**
  * **Desserialização Insegura:** Processamento de objetos serializados não confiáveis que levam à execução remota de código (RCE).
  * **Atualizações sem Assinatura:** Mecanismos de atualização automática que baixam e executam arquivos sem verificação de assinatura digital.

### A09:2025 – Security Logging and Alerting Failures (Falhas no Registro e Alerta de Segurança)
* **Descrição:** Ausência de registros (*logs*) de eventos relevantes de segurança ou falha em gerar alertas em tempo real para ações suspeitas.
* **Exemplos de Vulnerabilidades:**
  * **Falta de Logs Auditáveis:** Tentativas repetidas de acesso indevido ou falhas de autenticação que não são registradas.
  * **Ausência de Alerta Ativo:** Coleta de logs sem integração com sistemas de monitoramento (SIEM) para identificação e resposta a incidentes.

### A10:2025 – Mishandling of Exceptional Conditions (Tratamento Inadequado de Condições Excepcionais)
* **Descrição:** Nova categoria focada na incapacidade do sistema de lidar de forma segura com erros, exceções não tratadas ou estados anômalos.
* **Exemplos de Vulnerabilidades:**
  * **Falha do tipo *Fail-Open*:** Sistemas que concedem acesso ou ignoram verificações de segurança quando ocorre um erro interno.
  * **Vazamento por Exceção:** Exposição de dados sensíveis da aplicação ao tratar exceções não previstas.

---

## 2. Categorias Mais Críticas do OWASP Top 10:2025

Com base na severidade, impacto e prevalência, as três categorias no topo do ranking representam o nível mais crítico de risco:

1. **A01:2025 – Broken Access Control (#1 mais crítico):** Mantém-se na primeira posição da lista devido à sua alta frequência e impacto direto na confidencialidade e integridade dos dados de usuários.
2. **A02:2025 – Security Misconfiguration (#2):** Subiu para a segunda posição, refletindo a crescente complexidade das arquiteturas modernas baseadas em nuvem, contêineres e microsserviços.
3. **A03:2025 – Software Supply Chain Failures (#3):** Nova categoria em destaque que expandiu o risco de componentes desatualizados para abranger toda a integridade da cadeia de desenvolvimento, compilação e distribuição de software.

---

## 3. Ferramentas para Testar a Cadeia de Suprimentos (SCA e SBOM)

A proteção da cadeia de suprimentos de software requer automação na análise de componentes e governança de dependências integradas ao pipeline DevSecOps.

### Análise de Composição de Software (SCA - Software Composition Analysis)
* **OWASP Dependency-Check:** Ferramenta open-source que realiza o inventário contínuo de dependências do projeto e identifica vulnerabilidades conhecidas (CVEs) em componentes de terceiros.
* **retire.js:** Solução focada na varredura de bibliotecas JavaScript desatualizadas ou com falhas de segurança conhecidas.
* **Plataformas de SCA Automatizadas (ex: Snyk, Trivy, Safeguard):** Ferramentas que analisam continuamente o código, registros de contêineres e repositórios de artefatos para mapear dependências diretas e transitivas.

### Geração e Gestão de SBOM (Software Bill of Materials)
* **Padrões Abertos (CycloneDX e SPDX):** Formatos padronizados e legíveis por máquina para documentar a lista completa de componentes, licenças e procedência do software.
* **Geradores Automatizados de SBOM:** Ferramentas integradas ao processo de *build* (CI/CD) que emitem o inventário em tempo real durante a compilação do código.
* **Monitoramento Contínuo com NVD / CVE:** Integração dos inventários de SBOM com bases públicas de vulnerabilidades (National Vulnerability Database) para emissão de alertas em tempo real.

---

## 4. Riscos na Cadeia de Suprimentos de IA e LLMs

A adoção de Inteligência Artificial e Modelos de Linguagem (LLMs) expande a cadeia de suprimentos para além do código tradicional, incluindo modelos pré-treinados, conjuntos de dados (*datasets*), *plugins* e agentes autônomos.

### Principais Ameaças Conforme o OWASP Top 10 para LLMs e Aplicações Agênticas

1. **LLM04:2026 – Supply Chain Vulnerabilities (Vulnerabilidades na Cadeia de Suprimentos de IA):**
   * Uso de modelos pré-treinados alterados ou não verificados provenientes de repositórios públicos.
   * Dependência de *plugins*, extensões de terceiros e serviços hospedados sem auditoria de segurança.

2. **LLM05:2026 – Data and Model Poisoning (Envenenamento de Dados e Modelos):**
   * Injeção de dados maliciosos ou tendenciosos durante as fases de treinamento, *fine-tuning* ou no pipeline de recuperação RAG (Retrieval-Augmented Generation).
   * Introdução de *backdoors* ou comportamentos alterados no modelo antes do seu implantação.

3. **ASI04:2026 – Agentic Supply Chain Vulnerabilities (Vulnerabilidades Agênticas):**
   * Execução autônoma de ferramentas e APIs de terceiros por agentes de IA sem validação prévia de assinatura ou atestação de integridade.

4. **ASI06:2026 – Memory & Context Poisoning (Envenenamento de Memória e Contexto):**
   * Manipulação de bases vetoriais e memórias de curto/longo prazo utilizadas por agentes inteligentes, levando a decisões e ações comprometidas.
