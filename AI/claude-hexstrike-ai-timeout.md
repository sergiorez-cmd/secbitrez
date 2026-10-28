# Guia de Resolução de Timeout: HexStrike-AI & Nmap/Nuclei Kali Linux

Este guia consolida as configurações necessárias para ajustar e otimizar os limites de tempo (*timeout*) tanto no servidor e cliente do HexStrike-AI quanto nas varreduras do Nmap e Nuclei.

---

## Part 1: Ajustando o Timeout no HexStrike-AI

Se os seus escaneamentos longos estão caindo, você precisa aumentar o limite de tempo em até três frentes distintas:

### 1. Na Configuração do Cliente MCP (Claude Desktop, Cursor, etc.)

Por padrão, a integração MCP limita as requisições em 300 segundos. 

Edite o arquivo de configuração do seu cliente (ex: `claude_desktop_config.json` ou `hexstrike-ai-mcp.json`) e adicione ou altere o campo `"timeout"`:

```json
  "mcpServers": {
    "hexstrike-ai": {
      "command": "hexstrike_mcp",
      "args": [
        "--server",
        "http://localhost:8888",
        "--timeout",
        "600"
      ],
      "description": "HexStrike AI v6.0 - Advanced Cybersecurity Automation Platform",
      "timeout": 600,
      "disabled": false
    }
  },
```
*(No exemplo acima, o valor foi elevado para `600` segundos / 10 minutos).*

### 2. Parâmetros na Linha de Comando (`hexstrike_mcp.py`)

Se você estiver iniciando a ponte do cliente MCP manualmente ou via scripts SSH/customizados, passe explicitamente a flag `--timeout` seguida do valor em segundos:

```bash
hexstrike_mcp --server http://127.0.0.1:8888 --timeout 600
```

### 3. No Servidor Principal (`hexstrike_server.py`)

O servidor possui um limite interno padrão para a execução de ferramentas (`⏱️ Command Timeout: 300s`). Caso o comando ultrapasse o limite interno da aplicação, você deve alterá-lo diretamente no código-fonte:

1. Abra o arquivo `hexstrike_server.py` no seu editor de texto.
```bash
sudo -H mousepad /usr/share/hexstrike-ai/hexstrike_server.py
```
2. Procure pela constante ou variável de configuração de tempo limite (geralmente nomeada como `COMMAND_TIMEOUT`).

3. Modifique o valor de `300` para o tempo desejado (por exemplo, `600` ou `3600` se precisar de até 1 hora).

4. Reinicie o processo do servidor no terminal para aplicar as mudanças.

---

## Part 2: Otimizando o Scanner Nmap para Evitar Timeout

Para resolver o timeout excessivo no scanner Nmap (especialmente em varreduras de muitas portas ou IPs lentos), ajuste os argumentos de temporização do próprio binário do Nmap ou altere a chamada no servidor.

### 1. Passando Parâmetros de Otimização na Requisição

Ao invés de rodar um escaneamento genérico, adicione as flags de desempenho do Nmap (`-T4` ou `-T5`) e configure limites de timeout para os pacotes (`--host-timeout` ou `--max-rtt-timeout`).

* **Para varreduras rápidas (Aumenta a velocidade geral):**
  ```bash
  nmap -T4 -F 192.168.1.1
  ```
  *(O `-T4` acelera os timers e o `-F` varre apenas as 100 portas mais comuns).*

* **Para limitar o tempo máximo por Host (Recomendado para redes grandes):**
  ```bash
  nmap -T4 --host-timeout 5m 192.168.1.0/24
  ```
  *(Força o Nmap a desistir de qualquer IP que demore mais de 5 minutos).*

* **Para evitar travar em portas filtradas (Firewalls):**
  ```bash
  nmap -T4 --max-rtt-timeout 100ms --max-retries 1 192.168.1.1
  ```
