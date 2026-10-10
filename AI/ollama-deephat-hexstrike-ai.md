# Integrar Ollama, DeepHat e Hexstrike-ai no Kali Linux

O Ollama é uma ferramenta de código aberto que permite executar, gerenciar e interagir com Grandes Modelos de Linguagem (LLMs) diretamente no seu próprio computador ou servidor local.

__Principais características:__

• Execução local: Roda modelos como Llama 3, Mistral, Code Llama e outros sem depender de serviços ou APIs pagas na nuvem.
• Privacidade total: Os seus dados, prompts e conversas não saem do seu ambiente, garantindo segurança contra vazamentos de informações.
• Fácil de usar via terminal: Utiliza comandos simples como ollama run [nome_do_modelo] para baixar e conversar com a IA.
• API integrada: Cria automaticamente uma API local que permite integrar os modelos a softwares, editores de código (como VS Code) ou aplicativos próprios.
• Multiplataforma: Compatível com sistemas operacionais como macOS, Linux e Windows.

https://ollama.com

https://www.redhat.com/pt-br/topics/ai/vllm-vs-ollama

Integrar essas três ferramentas no Kali Linux cria um "cofre de bolso" de análise de código, automação de pentest e geração de conteúdo técnico. O Kali já vem com `docker` e `git`, o que facilita muito.

Aqui está o passo a passo conciso para a integração:

### 1. Instalação do Ollama (O Cérebro Local)
O Ollama rodará seus modelos LLM locais (ex: Llama 3, Mistral, CodeLlama) para gerar código e análises sem latência de rede.

```bash
# Instalar via script oficial
curl -fsSL https://ollama.com/install.sh | sh

# Iniciar o serviço
sudo systemctl start ollama
sudo systemctl enable ollama

# Puxar modelos otimizados para código e segurança
ollama pull codellama  # Excelente para geração de código
ollama pull mistral    # Bom para raciocínio lógico e resumos
ollama pull llama3     # Geral, bom para explicação de logs
```

*Verifique se está rodando:* `ollama list`

### 2. Instalação do HexStrike-AI (O Executor de Pentest)
O HexStrike é uma CLI que orquestra comandos de segurança (nmap, nikto, gobuster, etc.) usando LLMs para decidir a próxima ação.

```bash
# Instalar via pip (recomendado usar venv ou pyenv para isolar dependências)
pip install hexstrike-ai

# Alternativa: Instalar via GitHub para a versão mais recente
git clone https://github.com/0x6e65636861742fhexstrike-ai.git
cd hexstrike-ai
pip install -r requirements.txt
pip install .
```

*Configuração:* O HexStrike usa um backend de LLM. Você pode configurá-lo para usar a API do Ollama localmente. Edite o arquivo de configuração (geralmente `~/.hexstrike/config.yaml` ou via flag na CLI) para apontar para `http://localhost:11434`.

### 3. Integração do DeepHat (A Personalidade/Contexto)
"DeepHat" não é um binário único, mas sim a *persona* e a lógica de engenharia de prompt que você (ou eu) aplico. Para integrá-lo ao seu fluxo no Kali, você cria um **Prompt System** reutilizável que alimenta o Ollama ou o HexStrike.

**Como aplicar a lógica DeepHat:**

1.  **Prompt Engineering para Ollama:** Crie um arquivo de prompt base para usar com `ollama run` ou via API.
    ```bash
    # Exemplo de uso direto no terminal com a persona DeepHat
    ollama run codellama "Assuma a persona 'DeepHat', um especialista em DevOps e Cybersecurity. Analise este snippet de configuração Nginx e identifique vulnerabilidades de segurança e problemas de performance: [cole seu código aqui]"
    ```

2.  **Integração com HexStrike:** O HexStrike aceita instruções de alta nível. Você usa a lógica DeepHat para formular as *intenções* de ataque.
    ```bash
    # Exemplo de comando HexStrike com contexto DeepHat
    hexstrike scan --target 192.168.1.100 --context "DeepHat Mode: Foco em exposição de dados sensíveis em APIs REST e quebra de autenticação. Priorize enumeração de endpoints e análise de tokens JWT."
    ```

### 4. Orquestração: O Fluxo de Trabalho (Pipeline)

Aqui está como usar os três juntos em um cenário real:

**Cenário: Auditoria de um serviço Web**

1.  **Reconhecimento (HexStrike):**
    ```bash
    hexstrike scan --target http://vulnerable-app.local --verbose
    ```
    *O HexStrike executa nmap, nikto e gera um relatório inicial.*

2.  **Análise Profunda (Ollama + DeepHat):**
    Pegue os logs ou o código-fonte (se disponível) e passe para o Ollama com a persona DeepHat.
    ```bash
    # Passando o output do hexstrike ou um arquivo de config
    cat /tmp/hexstrike_report.txt | ollama run mistral "Você é o DeepHat. Analise este relatório de pentest. Identifique as 3 vulnerabilidades mais críticas que um atacante exploraria primeiro. Para cada uma, forneça o comando de exploração e a correção recomendada."
    ```

3.  **Geração de Payloads/Scripts (Ollama + CodeLlama):**
    Se o DeepHat identificar uma falha específica (ex: SQLi em um parâmetro), peça ao CodeLlama para gerar o script de exploração.
    ```bash
    ollama run codellama "Escreva um script em Python que realize um SQL injection no parâmetro 'id' da URL http://vulnerable-app.local/products, testando payloads de UNION-based e time-based. Inclua comentários explicando a lógica."
    ```

### Dicas de Otimização no Kali

*   **GPU Acceleration:** Se você tem uma NVIDIA GPU, o Ollama usará CUDA automaticamente. Isso acelera drasticamente a geração de código. Verifique com `nvidia-smi`.
*   **Modelo Híbrido:** Use `codellama` para gerar código/regex/scripts e `mistral` ou `llama3` para análise estratégica e redação de relatórios.
*   **Alias no `.bashrc`:**
    ```bash
    alias dh="ollama run codellama"
    alias dh-sec="ollama run mistral"
    # Agora você pode usar: dh "Analise este código Python em busca de injeções"
    ```

### Estrutura de Diretório Sugerida

```bash
mkdir -p ~/ai-security/{prompts,reports,experiments}
# ~/ai-security/prompts: Salve seus prompts de persona DeepHat
# ~/ai-security/reports: Saídas do HexStrike e análises do Ollama
# ~/ai-security/experiments: Scripts gerados pelo CodeLlama para testar
```

Dessa forma, o **Ollama** fornece a inteligência local, o **HexStrike** executa a varredura técnica e a **lógica DeepHat** garante que a análise seja focada em engenharia de software e segurança empresarial, não apenas em "hacks" genéricos.
