# JohnTheRipper

## Crack Linux PASSWD/SHADOW

$unshadow passwd shadow > crack-passwd.txt

$john --wordlist=/usr/share/wordlists/rockyou.txt --format=crypt crack-passwd.txt

## Crack SSH ID_RSA

$ssh2john id_rsa > crack-idrsa.txt

$john --wordlist=/usr/share/wordlists/rockyou.txt --format=SSH crack-idrsa.txt

$john --show crack-idrsa.txt

## Crack Windows LM/NTLM

meterpreter>hashdump

$john --wordlist=/usr/share/wordlists/rockyou.txt --format=NT hashdmp-blue.txt

$john --wordlist=/usr/share/wordlists/rockyou.txt --format=LM hashdmp-blue.txt

$john --show hashdmp-blue.txt

## Crack ZIP files

$zip2john file.zip > zip.hashes

$john --wordlist=/usr/share/wordlists/rockyou.txt zip.hashes

## Dir Kali Passwords Wordlists

/usr/share/wordlists/rockyou.txt

/usr/share/wordlists/fasttrack.txt

/usr/share/wordlists/john.lst

/usr/share/wordlists/nmap.lst

/usr/share/wordlists/legion

## Links

Fonte: https://www.stationx.net/how-to-use-john-the-ripper

Fonte: https://www.openwall.com/john/doc

Fonte: https://www.kali.org/tools/john
