# 1° Scan Nmap 

$sudo nmap -A [Target_IP] -oN report-nmap.txt

$sudo nmap -Pn -sV -O [Target_IP] -oN report-nmap.txt

$sudo nmap -Pn --script vuln [Target_IP]

$sudo nmap -Pn -p 80 --script http-enum [Target_IP]

$sudo nmap -Pn --script http-robots.txt [Target_IP]

$sudo nmap -Pn -p 21 --script ftp-anon [Target_IP]

# 2° Scan Dirb/Gobuster

$dirb http://example.com -o dirb-report.txt

$gobuster -u http://example.com -w /usr/share/dirb/wordlists/big.txt dir

# 3° Gain Access

http://example.com/login

http://example/upload

http://example.com/hiden/dir

http://robots.txt

$ftp Target_IP

$ssh user@Target_IP

$ssh -i id_rsa user@Target_IP

$ssh -oHostKeyAlgorithms=+ssh-rsa user@Target_IP

$sudo mount -o rw <Target_IP>:/tmp /tmp/dir-target

$sudo mount -t cifs -o username=user_name //server_name/share_name /mnt/dir-target

# 4° Search Priv-Esc

$cat /etc/proc/version

$cat /etc/issue

$cat /etc/passwd

$cat /etc/crontab

$cat /etc/exports

$cat ~/.*history | less

$id

$ls -la /

$ls -la /home

$sudo -l

$getcap -r / 2>/dev/null

$find / -perm -o w -type d 2>/dev/null

$find / -perm -u=s -type f 2>/dev/null

$find / -name perl* python* gcc* 2>/dev/nul

$find /home -name flag*.txt

