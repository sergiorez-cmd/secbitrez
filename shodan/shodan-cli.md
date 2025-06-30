
# Shodan via linha de comando (CLI)

## Criar uma conta e obter uma API Key

https://account.shodan.io

## Instalar Shodan no Kali-Linux

$sudo apt install -y python3-pip

$pip3 install shodan

## Executar Shodan CLI

$shodan init [YOUR_API_KEY]

$shodan --help

$shodan search --help

$shodan myip

$shodan host example.com

$shodan domain example.com

$shodan count port:3389 os:"Windows 10 Home 19041"

$shodan count Apache 2.4

$shodan count vuln:cve-2021-40449

$shodan stats --facets vuln country:BR

$shodan search '230 login successful port:21'

$shodan search 'product:MySQL'    

$shodan search --fields ip_str,port,org,hostnames microsoft iis 6.0

$shodan search --fields ip_str,port,org,hostnames Apache 2.4

$shodan search --fields ip_str,org,hostnames port:8291 product:mikrotik

$shodan search --fields ip_str,org,hostnames port:8080 product:nginx

$shodan download apache-2.4 Apache 2.4

$shodan parse --fields ip_str,port,org --separator , apache-2.4.json.gz

$shodan search --fields ip_str,port,org,hostnames 'asn:<ASN_Number> vuln:cve-2021-40449'

$shodan stats --facets ssl.version asn:<ASN_Number> has_ssl:true http

$shodan domain -D scanme.nmap.com -S

$shodan honeyscore  [Target_IP]

$shodan scan submit [Target_IP]

$nmap -sn -Pn -n --script shodan-api --script-args shodan-api.apikey=<ShodanAPI_KEY> scanme.nmap.org

## Lista de palavras chaves para search

Geral: all, asn, city, country, cpe, device, geo, has_ipv6, has_screenshot, screenshot.label, has_ssl, has_vuln, hash hostname, ip, isp, link, net, org, os, port, postal, product, region, scan, shodan.module, state, version

HTTP: http.component, http.component_category, http.favicon.hash, http.html, http.html_hash, http.robots_hash, http.securitytxt, http.status, http.title, http.waf

BITCOIN: bitcoin.ip, bitcoin.ip_count, bitcoin.port, bitcoin.version

SNMP: snmp.contact, snmp.location, snmp.name

SSL: ssl, ssl.alpn, ssl.cert.alg, ssl.cert.expired, ssl.cert.extension, ssl.cert.fingerprint, ssl.cert.issuer.cn, ssl.cert.pubkey.bits, ssl.cert.pubkey.type, ssl.cert.serial, ssl.cert.subject.cn, ssl.chain_count, ssl.cipher.bits, ssl.cipher.name, ssl.cipher.version, ssl.version

NTP: ntp.ip, ntp.ip_count, ntp.more, ntp.port

TELNET: telnet.do, telnet.dont, telnet.option, telnet.will, telnet.wont

SSH: ssh.hassh, ssh.type

https://cli.shodan.io/

https://help.shodan.io/command-line-interface/0-installation
