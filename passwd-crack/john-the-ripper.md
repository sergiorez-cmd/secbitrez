# JohnTheRipper

## Crack Linux PASSWD/SHADOW

$unshadow passwd shadow > crack-passwd.txt

$john --wordlist=/usr/share/wordlists/rockyou.txt --format=crypt crack-passwd.txt

## Crack SSH ID_RSA

$ssh2john id_rsa > crack-idrsa.txt

$john --wordlist=/usr/share/wordlists/rockyou.txt --format=SSH crack-idrsa.txt

$john --show crack-idrsa.txt

## Crack Windows NT

meterpreter>hashdump

$john --wordlist=/usr/share/wordlists/rockyou.txt --format=NT hashdmp-blue.txt

$john --show hashdmp-blue.txt
