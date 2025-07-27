# Hashcat

## Verficar tipo de hash

$hashid -m [hash-sequence]

## Crack hash MD5

#hashcat --help | grep MD5

$hashcat -a 0 -m 0 hash-md5.txt /usr/share/wordlists/rockyou.txt

## Crack hash SHA256

hashcat -a -m 1400 crack-hash-sha256.txt /usr/share/wordlists/rockyou.txt

## Crack hash Linux OS

$hashcat --help | grep Unix

$hashcat -a 0 -m 1800 hash-passwd-shadow.txt /usr/share/wordlists/rockyou.txt

## Crack hash Windows OS

$hashcat --help | grep NTLM

$hashcat -a 0 -m 1000 hash-md5.txt /usr/share/wordlists/rockyou.txt

## Crack HMAC-SHA1 + salt

$hashcat -a 0 -m 160 crack-hash-hmac-sha1-salt.txt /usr/share/wordlists/rockyou.txt

## Crack Hash Brute Force

hashcat -a 3 -m 0 hash-md5.txt ?l?l?l?l

* Built-in charsets:

   ?l = abcdefghijklmnopqrstuvwxyz

   ?u = ABCDEFGHIJKLMNOPQRSTUVWXYZ

   ?d = 0123456789

   ?s =  !"#$%&'()*+,-./:;<=>?@[\]^_`{|}~

   ?a = ?l?u?d?s

   ?b = 0x00 - 0xff


Crack bcrypt $2*$, Blowfish (Unix) com mascara de 4 letras minusculas
hashcat -a 3 -m 3200 crack-hash-bcrypt.txt ?l?l?l?l

Crack sha512crypt $6$, SHA512 (Unix) 2 com mascara de 4 letras minúsculas e 2 numeros
hashcat -a 3 -m 1800 crack-hash-sha512.txt ?l?l?l?l?d?d

Fonte: https://www.stationx.net/how-to-use-hashcat

Fonte: https://www.kali.org/tools/hashcat

Fonte: https://hashcat.net/wiki
