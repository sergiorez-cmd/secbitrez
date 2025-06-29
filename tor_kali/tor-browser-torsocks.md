# Tor Browser + Torsocks 

$sudo apt update

$sudo apt -y upgrade

$sudo apt install -y torbrowser-launcher torsocks

$torbrowser-launcher

## Conectar + Onionize (Configurações>Conexão>Encontrar mais Pontes)

https://check.torproject.org, https://bgp.he.net

## Utilizando Torsocks no Shell Kali Linux

$sudo systemctl start tor

$sudo systemctl status tor

$ . torsocks on

$curl ifconfig.so

$curl ipinfo.io 

$curl check.torproject.org

$sudo nmap -sS scanme.nmap.org

$ . torsocks off
