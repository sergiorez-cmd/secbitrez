# Guia de Uso: Spiders no OWASP ZAP (Zed Attack Proxy)

Este documento resume o funcionamento do **AJAX Spider** e do **Client Spider** no OWASP ZAP, além de fornecer um guia prático para configuração de autenticação e fluxo de trabalho ideal.

---

## 1. Diferença entre AJAX Spider e Client Spider

No OWASP ZAP, a principal diferença entre os dois spiders está na forma como eles controlam o navegador e inspecionam a aplicação web para descobrir links e rotas:

### AJAX Spider

* **Como funciona:** Controla navegadores "por fora" (geralmente usando Selenium ou ferramentas externas como CrawlJacks) para abrir páginas, executar JavaScript e simular cliques em elementos e formulários.
* **Inspeção:** Analisa o DOM resultante de forma externa e envia requisições para mapear os endpoints.
* **Características:**
  * É mais antigo e depende de componentes externos ao núcleo do ZAP.
  * Oferece menos visibilidade em tempo real do que o navegador está fazendo.
  * É mais lento e tende a ser menos eficaz em aplicações modernas do que o substituto mais recente.

### Client Spider (introduzido na versão 2.16)

* **Como funciona:** Faz parte do complemento *Client Side Integration* e injeta uma extensão própria no navegador que o ZAP inicializa.
* **Inspeção:** A extensão emite eventos diretamente do navegador para o ZAP, permitindo construir a **Client Map** (um mapa estrutural em tempo real de tudo o que está visível no DOM e na aplicação).
* **Características:**
  * Tem acesso direto a links, controles e estados profundos do DOM.
  * É mais rápido, mais eficiente e encontra mais endpoints em aplicações modernas (Single Page Applications em React, Vue, Angular).
  * Oferece abas de detalhes visuais (*Client Details* e *Client Map*) para acompanhar o rastreamento.
  * Foi desenvolvido para substituir gradualmente o AJAX Spider tradicional.

---

## 2. Como configurar Autenticação no Client Spider

Para que o Client Spider consiga mapear áreas logadas, utilize o método moderno **Browser-Based Authentication**:

1. **Defina o Contexto:** No painel esquerdo do ZAP (*Sites*), clique com o botão direito na URL do seu alvo e selecione **Include in Context -> Default Context**.
2. **Configure a Autenticação:** Nas propriedades do contexto, vá em **Authentication** e mude o método para **Browser-Based Authentication**.
3. **Selecione o Navegador:** Escolha o navegador (ex: *Firefox headless* ou *Chrome headless*).
4. **Indique a URL de Login:** Preencha o campo *Login Page URL* com o endereço exato da página de login.
5. **Adicione as Credenciais:** Na aba **Users** (dentro do mesmo Contexto), adicione um novo usuário com o usuário e senha corretos.
6. **Defina os Indicadores (Verificação):** Na aba *Authentication*, configure como o ZAP sabe se está logado ou não (usando expressões regulares para termos como "Sair" ou "Logout" que aparecem apenas na área logada).

> **Dica:** Uma vez configurado o Contexto, ao iniciar o Client Spider, certifique-se de selecionar o usuário criado no campo *User* para que ele abra o navegador já autenticado.

---

## 3. O Fluxo de Trabalho Ideal (Combinando os Spiders)

Em aplicações modernas, use as ferramentas de rastreamento de forma sequencial, do mais simples ao mais avançado:

1. **Spider Tradicional:** Varre o HTML puro de forma extremamente rápida. Encontra links estáticos, arquivos estáticos (CSS/JS) e a estrutura básica do site em segundos.
2. **Client Spider:** Entra em cena logo em seguida para interagir com o JavaScript, renderizar o DOM, clicar em botões dinâmicos e mapear páginas em React/Vue/Angular que o Spider Tradicional não conseguiu ler.
3. **Active Scan (Opcional):** Deve ser executado depois que os dois spiders criarem uma árvore de sites (*Sites Tree*) robusta e completa, garantindo que o ZAP teste vulnerabilidades em todas as rotas possíveis.
