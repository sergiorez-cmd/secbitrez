# TOR+Proxychains

## 1° Instalar os pacotes necessários: 
```bash
sudo apt update && sudo apt upgrade -y
```
```bash
sudo apt install tor proxychains -y
```
---

## 2° Editar o arquivo de configuração do proxychains: 
```bash
$ sudo nano /etc/proxychains.conf
```
  • Descomente a linha: __dynamic_chain__
  
  • Comente a linha: __strict_chain__
  
  • Acrescente no final do arquivo a linha: __socks5  127.0.0.1 9050__

---

## 3° Inicializar o serviço tor: [status,start,stop]
```bash
sudo service tor start
```
```bash
sudo systemctl start tor
```
```bash
sudo systemctl status tor
```
---

## 4° Verificar endereçamento IP da máquina

* (seu_ip_publico_REAL)
```bash
curl ifconfig.so 
```
* (seu_ip_via_TOR)
```bash
proxychains curl ifconfig.so 
```
---

## 5° Testar a rede tor com firefox 
```bash
proxychains firefox
```
```text
https://check.torproject.org
```
```text
https://bgp.he.net
```
```text
https://ifconfig.me
```
```text
https://ipinfo.io/what-is-my-ip
```
```text
https://en.utrace.me
```
```text
https://dnsleaktest.com
```
---

## Exemplos de comandos úteis para reconhecimento ativo de alvos

`$ tor-resolve example.com (pesquisa dns query via rede tor)`

`$ sudo proxychains nmap -sS [IP_Alvo] (mapeamento de portas disponíveis em hosts)`

`$ sudo proxychains nmap -Pn -p 80 [IP_Alvo] (mapeamento de porta específica em hosts)`

`$ sudo proxychains whatweb https://example.com (verificar tecnologias do site)`

`$ sudo proxychains wpscan --url https://example.com (verificar vulnerabilidades wordpress)`

`$ sudo proxychains dirb https://example.com /usr/share/wordlists/dirb/common.txt (visualizar conteúdo do webserver)`
