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

$sudo bash

#sha256sum $(which nmap)

#nmap --script-updatedb

#nmap --script-help vuln

#nmap -sC -Pn [Target_IP]

#nmap --script=default -Pn [Target_IP]

#nmap --script vuln -Pn [Target_IP]

#nmap --script banner -Pn -sV [Target_IP]

#nmap --script http-enum -Pn -p 80 [Target_IP]

#nmap --script http-vuln-* -Pn -p 80 [Target_IP] -d

#nmap --script http-robots.txt [Target_IP]

#nmap --script ftp-anon -Pn -p 21 [Target_IP]

#nmap --script smb-os-discovery -Pn -p 445 [Target_IP]

#nmap --script smb-enum-shares -Pn -p 445 [Target_IP]

#nmap --script smtp-enum-users -Pn -p 25 [Target_IP]

#nmap --script dns-brute -Pn [Target_IP]

#nmap --script dns-zone-transfer -Pn -p 53 [Target_IP]

#nmap --script snmp-brute -Pn [Target_IP]

---------------------------------------------------------------------------------
Fonte: https://www.stationx.net/nmap-scripts

Fonte: https://nmap.org/book/man-nse.html
