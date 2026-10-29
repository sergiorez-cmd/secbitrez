# Guia de Ferramentas de Segurança de Aplicações para JavaScript

SAST (Static Application Security Testing) e DAST (Dynamic Application Security Testing) são métodos essenciais de teste de segurança de software usados no ciclo de desenvolvimento para encontrar vulnerabilidades e proteger aplicações.

Este guia reúne as principais informações sobre métodos e ferramentas de **SAST**, **DAST** e **SCA** específicas para o ecossistema JavaScript (Node.js, React, Angular, Vue, etc.).

---

## 📌 Resumo Rápido: SAST vs DAST

| Característica | SAST | DAST |
| :--- | :--- | :--- |
| **Abordagem** | Caixa branca (vê o interior do código) | Caixa preta (vê de fora, como usuário/atacante) |
| **Acesso ao código**| Obrigatório | Não necessário (pode testar sistemas fechados) |
| **Momento no ciclo**| Cedo (durante a codificação) | Tarde (após a aplicação estar rodando) |
| **Foco principal** | Falhas de sintaxe, código inseguro e credenciais expostas | Erros de configuração, autenticação e sessão em tempo real |

---

## ⚙️ Ferramentas SAST (Análise de Código Estático)

Analisam o código-fonte, bytecode ou binários **sem executar** a aplicação.

*   **Semgrep**: A ferramenta mais rápida e moderna para JavaScript/TypeScript. Analisa o código em segundos no pipeline de CI/CD e possui regras excelentes para frameworks web modernos (como Express, React e Node.js).
*   **SonarQube**: Excelente para monitorar a qualidade e a segurança do código a longo prazo. Cria painéis visuais integrados ao Git para apontar vulnerabilidades e *code smells* em JavaScript/TypeScript.
*   **ESLint (com plugins de segurança)**: Ferramenta que você provavelmente já usa. Ao adicionar plugins como `eslint-plugin-security` ou `eslint-plugin-sonarjs`, ela se transforma em um SAST leve que avisa sobre falhas diretamente no editor de código (IDE).
*   **GitHub Advanced Security (CodeQL)**: Se o seu repositório está no GitHub, essa ferramenta nativa analisa o fluxo de dados do seu código JavaScript para encontrar falhas complexas como injeção de código ou XSS.

---

## 🌐 Ferramentas DAST (Análise Dinâmica em Execução)

Testam a aplicação **em execução**, simulando ataques externos (como um hacker) para ver se ela falha ou vaza informações.

*   **OWASP ZAP**: A melhor escolha gratuita para JavaScript. Como aplicações modernas em JS (Single Page Applications ou SPAs) dependem muito de chamadas de API (REST/GraphQL), o ZAP consegue mapear e testar esses endpoints em execução de forma automatizada.
*   **Burp Suite Professional**: Ferramenta indispensável se você precisar simular ataques manuais mais profundos na sua aplicação web em JS, analisando como o front-end manipula tokens, sessões e requisições assíncronas.
*   **Acunetix**: Ótima opção paga corporativa que possui excelente suporte para renderizar e varrer Single Page Applications (SPAs) complexas construídas em React, Angular ou Vue.

---

## 💡 Dica Bônus para JavaScript: SCA (Software Composition Analysis)

No ecossistema JavaScript (npm), a maioria das vulnerabilidades vem de **bibliotecas de terceiros** (pastas `node_modules`). Para isso, adicione essas ferramentas à sua rotina:

*   **npm audit**: Comando nativo, gratuito e instantâneo para checar falhas em dependências.
*   **Snyk Open Source**: Identifica e cria pull requests automaticamente para corrigir pacotes vulneráveis no seu projeto JavaScript.
