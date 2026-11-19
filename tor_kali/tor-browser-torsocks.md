# Tor Browser + Torsocks 
```bash
sudo apt update && sudo apt upgrade -y
```
```bash
sudo apt install -y torbrowser-launcher torsocks
```
```bash
torbrowser-launcher
```
---

## Conectar + Onionize (Configurações>Conexão>Encontrar mais Pontes)
```text
https://check.torproject.org 
```
```text
https://bgp.he.net
```
---

## Utilizando Torsocks no Shell Kali Linux
```bash
sudo systemctl start tor
```
```bash
sudo systemctl status tor
```
```bash
. torsocks on
```
```bash
curl ifconfig.so
```
```bash
curl ipinfo.io 
```
```bash
curl check.torproject.org
```
```bash
sudo nmap -sS scanme.nmap.org
```
```bash
. torsocks off
```
