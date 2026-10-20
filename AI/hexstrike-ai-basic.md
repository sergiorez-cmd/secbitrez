# HEXSTRIKE-AI

HexStrike-AI é um framework de segurança ofensiva de código aberto que utiliza inteligência artificial para automatizar testes de penetração e descoberta de vulnerabilidades. Ele funciona como uma ponte (servidor MCP) que conecta grandes modelos de linguagem (como GPT-4, Claude) a mais de 150 ferramentas de segurança tradicionais, permitindo que a IA selecione e execute ferramentas de forma autônoma com base nos resultados em tempo real .

## 🧠 Como Funciona

O núcleo do HexStrike-AI é um servidor FastMCP que atua como orquestrador. Em vez de seguir um script fixo, um modelo de linguagem (LLM) interpreta o objetivo do usuário e decide qual ferramenta usar e como configurá-la, criando um ciclo contínuo de análise, execução e feedback . A ferramenta foi originalmente criada pelo pesquisador Muhammad Osama (0x4m4) para fins legítimos de testes de segurança (Red Team) .

## ⚠️ O Uso Malicioso

Apesar de sua proposta defensiva, o HexStrike-AI rapidamente chamou a atenção de cibercriminosos. Relatórios de 2025 indicam que grupos de ameaça (como o Storm-1575) começaram a usar o framework para explorar vulnerabilidades "n-day" (recém-divulgadas) em questão de minutos. O caso mais notório envolveu a exploração da vulnerabilidade CVE-2025-7775 em dispositivos Citrix NetScaler, onde a automação da IA teria reduzido o tempo de ataque de dias para menos de 10 minutos .

---

__Funcionalidades__

1. **Conexão de agentes de IA** – Agentes como Claude, GPT ou outros compatíveis com MCP conectam-se por meio do protocolo FastMCP
2. **Análise inteligente** – O mecanismo de decisão analisa os alvos e seleciona as estratégias de teste ideais
3. **Execução autônoma** – Agentes de IA realizam avaliações de segurança abrangentes
4. **Adaptação em tempo real** – O sistema se ajusta com base nos resultados e nas vulnerabilidades descobertas
5. **Relatórios avançados** – Apresentação visual com cards de vulnerabilidades e análise de riscos

---

No ecossistema do **HexStrike AI** (plataforma de automação de segurança ofensiva baseada em IA através do protocolo MCP — *Model Context Protocol*), a arquitetura é dividida em duas partes principais que trabalham juntas:

## 1. `hexstrike_server` (O Servidor Core / API Backend)

* **O que é:** É o processo de backend de longa execução (`hexstrike_server.py`) que roda em segundo plano ou em primeiro plano na sua máquina (geralmente escutando na porta `8888`).
* **Função:** Ele é o "motor" que realmente possui o controle e gerencia a execução de mais de 150 ferramentas de segurança (como Nmap, Nuclei, Sqlmap, Metasploit, etc.). O servidor interage diretamente com o sistema operacional, gerencia o cache inteligente, faz o tratamento de erros, registra logs e executa os comandos de forma isolada/controlada.

## 2. `hexstrike_mcp` (O Adaptador / Cliente MCP)

* **O que é:** É o script de integração (`hexstrike_mcp.py`) que serve como ponte (cliente/adaptador) entre o seu assistente de IA (como Claude Desktop, Cursor, VS Code Copilot ou Roo Code) e o servidor central do HexStrike.
* **Função:** Ele implementa o protocolo MCP exigido pelas IAs. Quando a inteligência artificial precisa rodar um escaneamento ou teste, ela envia a instrução por meio deste adaptador, que por sua vez se comunica via API com o `hexstrike_server`.

---

## Resumo das Diferenças

| Característica | `hexstrike_server` | `hexstrike_mcp` |
| --- | --- | --- |
| **Papel** | Servidor de Backend / Gerenciador de Ferramentas | Adaptador de Cliente MCP (Ponte com a IA) |
| **Onde atua** | Gerencia e executa as ferramentas de pentest instaladas no SO. | Conecta o editor/chat de IA (Claude, Cursor, etc.) ao servidor. |
| **Execução** | Deve ser iniciado primeiro e mantido rodando (ex: `python3 hexstrike_server.py`). | É chamado automaticamente pelo cliente de IA através de arquivo de configuração. |

Em suma: você liga o **`hexstrike_server`** para preparar o ambiente de ferramentas e o **`hexstrike_mcp`** é configurado na sua ferramenta de IA para conseguir conversar com esse servidor.

---

**Não é estritamente obrigatório executar o hexstrike_server como root**, mas na prática **muitas das ferramentas de segurança** que ele orquestra exigem privilégios elevados para funcionar corretamente.

Abaixo estão os principais pontos a considerar sobre o uso de `root` com o `hexstrike_server` no Kali Linux:

## 1. Dependência das Ferramentas (O Motivo Principal)

O `hexstrike_server` em si é apenas uma aplicação Python que gerencia APIs e executa comandos no sistema operacional. No entanto, ele aciona mais de 150 ferramentas de pentest.

* **Ferramentas que exigem `root`:** Vários utilitários de rede avançados (como o `nmap` para varreduras do tipo SYN/ACK `-sS`, captação de pacotes com `tcpdump`, ou certas funcionalidades do Metasploit) **precisam** de privilégios de superusuário para abrir sockets brutos (*raw sockets*) ou interagir diretamente com as interfaces de rede.
* Se você rodar o servidor como um usuário comum (*non-root*), essas ferramentas específicas vão falhar ou retornar erros de permissão quando a IA tentar acioná-las.

## 2. Boas Práticas e Segurança

Embora seja comum rodar ferramentas de pentest como `root` no Kali Linux (já que o próprio sistema opera frequentemente sob esse usuário por padrão em instalações tradicionais), há riscos a ponderar:

* **Superfície de Ataque e Vulnerabilidades:** O `hexstrike_server` expõe uma API local que aceita comandos orquestrados por IA. Caso haja alguma falha de injeção ou comportamento inesperado, rodar o backend inteiro como `root` concede controle total do sistema operacional ao processo.
* **Ambiente isolado:** Se possível, o ideal é gerenciar isso de forma consciente, ciente de que o motor precisa interagir com binários de sistema que frequentemente demandam permissões administrativas.

---

### Resumo

* **Funcionar:** O servidor em Python pode subir com um usuário comum, mas **as ferramentas de segurança perderão metade da eficácia** por falta de privilégios.
* **Recomendação:** No Kali Linux, ele é comumente executado com privilégios elevados (`sudo` ou diretamente no contexto root) justamente para garantir que o agente de IA não sofra bloqueios de permissão ao disparar varreduras profundas ou testes de intrusão.

---

## 3. Desempenho em Cenários Reais


| Coluna 1 | Coluna 2 | Coluna 3 |
| --- | --- | --- |
| Dado A1 | Dado A2 | Dado A3 |
| Dado B1 | Dado B2 | Dado B3 |


| Operação | Método Manual Tradicional | IA HexStrike v6.0 | Melhoria |
| **Enumeração de Subdomínios** | 2–4 horas | 5–10 minutos | 24x mais rápido |
| **Varredura de Vulnerabilidades** | 4–8 horas | 15–30 minutos | 16x mais rápido |
| **Testes de Segurança em Aplicações Web** | 6–12 horas | 20–45 minutos | 18x mais rápido |
| **Resolução de Desafios CTF** | 1–6 horas | 2–15 minutos	 | 24x mais rápido |
| **Geração de Relatórios** | 4–12 horas | 2–5 minutos | 144x mais rápido |

__Métricas de Sucesso__

- Taxa de Detecção de Vulnerabilidades: 98,7% (vs. 85% em testes manuais)
- Taxa de Falsos Positivos: 2,1% (vs. 15% em scanners tradicionais)
- Cobertura de Vetores de Ataque: 95% (vs. 70% em testes manuais)
- Taxa de Sucesso em CTFs: 89% (vs. 65% da média de especialistas humanos)
- Sucesso em Programas de Bug Bounty: Mais de 15 vulnerabilidades de alto impacto descobertas durante os testes

---

## 4. Troubleshooting

Problemas comuns

__MCP Falha de Conexão:__

Verificar se o servidor esta rodando
```
netstat -tlnp | grep 8888
```
Reiniciar o servidor
```
hexstrike_server
```

__Ferramentas Não Encontradas:__

Verificar disponibilidade da ferramenta
```
which nmap gobuster nuclei metasploit
```
Instalar ferramentas não disponíveis via APT
```
sudo apt install -y nmap gobuster nuclei metasploit
```

__Agente de IA não pode conectar:__

Verificar configurações de paths do MCP

Verificar logs do servidor por tentativas de conexão
```
hexstrike_mcp --debug
```
---

### Lembrete

O uso de ferramentas como o HexStrike-AI para acessar sistemas sem autorização explícita é ilegal e constitui crime cibernético.
