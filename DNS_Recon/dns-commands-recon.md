# Comandos para Recon de DNS

## Enumeração básica de subdomínios
```bash
dnsrecon -d example.com
```
## Enumeração com dicionário de subdomínios
```bash
dnsrecon -d example.com -t std -D /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt
```
## Enumeração com zone transfer
```bash
dnsrecon -d example.com -t axfr
```
## Enumeração com reverse lookup
```bash
dnsrecon -d example.com -t r
```
## Coleta de informações via motores de busca e fontes públicas
```bash
theHarvester -d example.com -b crtsh
```
## Enumeração passiva de subdomínios
```bash
amass enumerate -passive -d example.com
```
## Enumeração ativa de subdomínios
```bash
amass enumerate -active -d example.com
```
## Enumeração com dicionário
```bash
amass enumerate -passive -d example.com -wordlists /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt
```
## Usar nmap para scan de DNS (se disponível)
```bash
nmap --script dns-brute example.com
```
## Usar nmap para zone transfer
```bash
nmap --script dns-service-discovery example.com
```
## Usar fping para verificar hosts ativos em subdomínios
```bash
fping -g 192.0.2.0/24
```
## Verificar registro DNSKEY
```bash
dig example.com DNSKEY
```
## Verificar registro RRSIG
```bash
dig example.com RRSIG
```
## Verificar registro DS
```bash
dig example.com DS
```
## Tentar zone transfer com dig
```bash
dig axfr @ns1.example.com example.com
```
## Tentar zone transfer com dnsrecon
```bash
dnsrecon -d example.com -t axfr
```
## Tentar zone transfer com host
```bash
host -l example.com
```
