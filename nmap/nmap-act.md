# NMAP Network Scanner

O comando `nmap scanme.nmap.org` executa uma **varredura padrão** (também conhecida como "default scan") contra o host especificado. Abaixo está a descrição técnica de como essa varredura é realizada, passo a passo:

### 1. Resolução do Hostname

- O NMAP primeiro resolve o nome de domínio `scanme.nmap.org` em um endereço IP (via DNS).
- Se a resolução falhar, o NMAP tenta usar o nome diretamente em protocolos que suportam resolução reversa (como em alguns casos de varredura de scripts).

### 2. Seleção de Portas Padrão

- Por padrão, o NMAP varre as **1.000 portas mais comuns** (definidas no arquivo `nmap-service-probes` ou no conjunto padrão de portas).
- Isso inclui portas TCP e UDP, mas a varredura padrão é **TCP-only** (a menos que `-sU` seja usado para UDP).

### 3. Técnica de Varredura TCP: SYN Stealth Scan (`-sS`)

- O NMAP usa a técnica **SYN scan** (também chamada de "stealth scan" ou "half-open scan").
- Em vez de estabelecer uma conexão TCP completa (como faria um `connect()`), o NMAP envia um pacote **SYN** (Synchronize) para cada porta alvo.
  - **Resposta SYN-ACK:** A porta está **aberta**.
  - **Resposta RST (Reset):** A porta está **fechada**.
  - **Sem resposta ou RST:** A porta pode estar **filtrada** (por um firewall).
- O NMAP não completa o handshake TCP (não envia ACK), o que torna a varredura menos perceptível em logs do alvo.

### 4. Varredura de Versões de Serviços (`-sV` opcional)

- Por padrão, o NMAP **não** executa a detecção de versões de serviços (`-sV`). Isso significa que ele identifica o serviço apenas com base na porta e no banner padrão, sem enviar probes personalizados para determinar a versão exata do software.
- Se `-sV` fosse adicionado, o NMAP envolveria pacotes adicionais para interrogar os serviços abertos e identificar a versão exata.

### 5. Detecção de Sistema Operacional (`-O` opcional)

- Por padrão, o NMAP **não** executa a detecção de sistema operacional (`-O`). Isso é feito apenas se a flag `-O` for incluída, onde o NMAP analisa os detalhes do IP/TCP/ICMP (como TTL, window size, options) para inferir o SO do host.

### 6. Processamento de Resultados e Filtros

__O NMAP classifica cada porta como:__
  - **open:** Porta acessível.
  - **closed:** Porta acessível, mas sem serviço ouvindo.
  - **filtered:** Firewall impede o acesso ou dropa pacotes.
  - **unfiltered:** Porta acessível, mas o NMAP não pode determinar se está aberta ou fechada (raro no modo padrão).

### 7. Saída

__O NMAP exibe um relatório no terminal com:__
  - Endereços IP e hostnames resolvidos.
  - Lista de portas abertas, fechadas ou filtradas.
  - Nomes de serviços associados às portas abertas (baseados em `services` file).
  - Resumo final (ex.: "3 open ports").

### Exemplo de Saída Típica:

```bash
Starting Nmap 7.94 ( https://nmap.org ) at 2023-10-05 12:00:00
Nmap scan report for scanme.nmap.org (45.33.32.156)
Host is up (0.00012s latency).
Not shown: 996 closed tcp ports (reset)
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
31337/tcp open insert
```

### Resumo das Flags Implícitas no Comando Padrão:
- `-sS` (SYN scan)
- `-Pn` (Não assume que o host está online; assume que está)
- `-p 1-1000` (Varre as 1.000 portas mais comuns)
- `-sV` **não** é usado por padrão
- `-O` **não** é usado por padrão

### Observações Importantes:

- **Privilegios:** O SYN scan requer privilégios de root (ou capacidades equivalentes) para criar pacotes TCP brutos. Se executado sem privilégios, o NMAP usa um `connect()` scan (`-sT`) em vez de SYN scan.

- **Firewalls:** A detecção de portas "filtered" depende de como o firewall do alvo trata pacotes SYN. Firewalls stateful podem gerar respostas RST, fazendo com que portas abertas pareçam fechadas.
