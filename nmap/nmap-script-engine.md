### Nmap Scripting Engine Categories

The most common Nmap scripting engine categories:
- auth: Utilize credentials or bypass authentication on target hosts.
- broadcast: Discover hosts not included on command line by broadcasting on local network.
- brute: Attempt to guess passwords on target systems, for a variety of protocols, including http, SNMP, IAX, MySQL, VNC, etc.
- default: Scripts run automatically when -sC or -A are used.
- discovery: Try to learn more information about target hosts through public sources of information, SNMP, directory services, and more.
- dos: May cause denial of service conditions in target hosts.
- exploit: Attempt to exploit target systems.
- external: Interact with third-party systems not included in target list.
- fuzzer: Send unexpected input in network protocol fields.
- intrusive: May crash target, consume excessive resources, or otherwise impact target machines in a malicious fashion.
- malware: Look for signs of malware infection on the target hosts.
- safe: Designed not to impact target in a negative fashion.
- version: Measure the version of software or protocols on the target hosts.
- vul: Measure whether target systems have a known vulnerability.

## Search Scripts

$grep "ftp" /usr/share/nmap/scripts/script.db

$grep "safe" /usr/share/nmap/scripts/script.db

## Common Examples

$sudo bash

#sha256sum $(which nmap)

#nmap -sn [Target_IP_Range] -oN scan_network.txt

#nmap -sS -sV -p1-1024 [Target_IP] -oN port_scan.txt

#nmap --script-updatedb

#nmap --script-help vuln

#nmap -sC -Pn [Target_IP]

#nmap -Pn --script=default [Target_IP]

#nmap -Pn --script vuln [Target_IP]

#nmap -Pn -sV --script banner [Target_IP]

#nmap -Pn -p 80 --script http-enum [Target_IP]

#nmap -Pn -p 80 --script http-vuln-* [Target_IP] -d

#nmap -Pn --script http-robots.txt [Target_IP]

#nmap -Pn -p 21 --script ftp-anon [Target_IP]

#nmap -Pn -p 445 --script smb-os-discovery [Target_IP]

#nmap -Pn -p 445 --script smb-enum-shares,smb-enum-users [Target_IP]

#nmap -Pn -p 445 --script smb-brute [Target_IP]

#nmap -Pn -p 25 --script smtp-enum-users [Target_IP]

#nmap -Pn --script dns-brute [Target_IP]

#nmap -Pn -p 53 --script dns-zone-transfer [Target_IP]

#nmap -Pn --script snmp-brute [Target_IP]

## Links
---------------------------------------------------------------------------------
Fonte: https://www.stationx.net/nmap-scripts

Fonte: https://nmap.org/book/man-nse.html

Fonte: https://nmap.org/nsedoc/categories/vuln.html
