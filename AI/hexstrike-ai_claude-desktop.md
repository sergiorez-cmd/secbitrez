
# Integrar Claude-Desktop AI + MCP Hexstrike-ai no Kali Linux

https://github.com/aaddrick/claude-desktop-debian

## Instalar Claude-Desktop + Hexstrike-ai

### Add the repo:
```
curl -fsSL https://pkg.claude-desktop-debian.dev/KEY.gpg | sudo gpg --dearmor -o /usr/share/keyrings/claude-desktop-unofficial.gpg
echo "deb [signed-by=/usr/share/keyrings/claude-desktop-unofficial.gpg arch=amd64,arm64] https://pkg.claude-desktop-debian.dev stable main" | sudo tee /etc/apt/sources.list.d/claude-desktop-unofficial.list
```
### Instalar o Claude-Desktop:
```
sudo apt update && sudo apt install claude-desktop-unofficial
```
### Instalar o MCP Hexstrike-ai:
```
sudo apt install hexstrike-ai
```

### Acesse o github oficial para copiar a configuração para integrar o Claude Desktop

https://github.com/0x4m4/hexstrike-ai

### Execute o Claude Desktop 

Procure por "Settings>Developer>Local MCP Server"

Editar as configurações no arquivo "claude_desktop_config.json"

Insira as seguintes configurações no inicio do arquivo

```
  "mcpServers": {
    "hexstrike-ai": {
      "command": "hexstrike_mcp",
      "args": [
        "--server",
        "http://localhost:8888"
      ],
      "description": "HexStrike AI v6.0 - Advanced Cybersecurity Automation Platform",
      "timeout": 300,
      "disabled": false
    }
  },
```
Reinicie o kali linux 

Execute o servidor MCP Hexstrike-ai
```
hexstrike_server
```
```
hexstrike_mcp
``` 
No terminal do Claude-Desktop digite o prompt para verificar se esta tudo OK
```
check health hexstrike mcp
```
