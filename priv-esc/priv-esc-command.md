# Search Priv-Esc

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

