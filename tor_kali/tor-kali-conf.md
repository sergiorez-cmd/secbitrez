# TOR+Proxychains

## 1° Instalar os pacotes necessários: 

$sudo apt install -y tor proxychains

## 2° Editar o arquivo de configuração do proxychains: 

$sudo vim /etc/proxychains.conf

    • Descomente a linha: dynamic_chain
    • Comente a linha: strict_chain
    • Acrescente no final do arquivo a linha: socks5  127.0.0.1 9050

## 3° Inicializar o serviço tor: 

#sudo service tor [status,start,stop]

$sudo systemctl [status,start,stop] tor

$systemctl status tor

## 4° Verificar endereçamento IP da máquina

$curl ifconfig.so (seu_ip_publico_REAL)

$proxychains curl ifconfig.so (seu_ip_via_TOR)

## 5° Testar a rede tor com firefox 

“$proxychains firefox”

https://check.torproject.org
https://bgp.he.net
https://ifconfig.me
https://ipinfo.io
https://en.utrace.me
https://dnsleaktest.com

## Exemplos de comandos úteis para reconhecimento ativo de alvos

$tor-resolve example.com (pesquisa dns query via rede tor)

$sudo proxychains nmap -sS [IP_Alvo] (mapeamento de portas disponíveis em hosts)

$sudo proxychains nmap -Pn -p 80 [IP_Alvo] (mapeamento de porta específica em hosts)

$sudo proxychains whatweb https://example.com (verificar tecnologias do site)

$sudo proxychains wpscan --url https://example.com (verificar vulnerabilidades wordpress)

$sudo proxychains dirb https://example.com /usr/share/wordlists/dirb/common.txt (visualizar diretórios do webserver)
