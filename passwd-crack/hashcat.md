# Hashcat

$hashcat --help

$hashcat -a 0 -m 0 hash.txt /dir/worlist.txt [Ataque de dicionário]

$hashcat -a 1 -m 0 hash.txt /dir/wordlist1.txt /dir/wordlist2.txt [Ataque combinado de dicionários]

$hashcat -a 3 -m 0 --increment hash.txt ?l?l?l?l [Ataque de força bruta com mascara de caracteres]

$hashcat -a 6 -m 0 hash.txt /dir/worlist.txt ?d?d?d?d [Ataque híbrido combinando wordlist+mascara]

$hashcat -a 7 -m 0  hash.txt ?d?d?d?d /dir/worlist.txt [Ataque híbrido combinando mascara+wordlist]

## Verficar tipo de hash

$hashid -m [hash-sequence]

## Crack hash MD5

$hashcat --help | grep MD5

$hashcat -a 0 -m 0 hash-md5.txt /usr/share/wordlists/rockyou.txt

$hashcat -m 0 hash.txt --show

## Crack hash SHA256

$hashcat --help | grep SHA256

hashcat -a -m 1400 hash-sha256.txt /usr/share/wordlists/rockyou.txt

$hashcat -m 1400 hash-sha256.txt --show

## Crack hash Linux OS

$hashcat --help | grep Unix

$hashcat -a 0 -m 1800 hash-passwd-shadow.txt /usr/share/wordlists/rockyou.txt

$hashcat -m 1800 hash-passwd-shadow.txt --show

## Crack hash Windows OS

$hashcat --help | grep NTLM

$hashcat -a 0 -m 1000 hash-ntlm.txt /usr/share/wordlists/rockyou.txt

$hashcat -m 0 hash-ntlm.txt --show

## Crack HMAC-SHA1 + salt

$hashcat --help | grep HMAC-SHA

$hashcat -a 0 -m 160 hash-hmac-sha1-salt.txt /usr/share/wordlists/rockyou.txt

$hashcat -m 160 hash-hmac-sha1-salt.txt --show

## Crack Hash Brute Force

$hashcat -a 3 -m 0 hash-md5.txt ?l?l?l?l

* Built-in charsets:

   ?l = abcdefghijklmnopqrstuvwxyz

   ?u = ABCDEFGHIJKLMNOPQRSTUVWXYZ

   ?d = 0123456789

   ?s =  !"#$%&'()*+,-./:;<=>?@[\]^_`{|}~

   ?a = ?l?u?d?s

   ?b = 0x00 - 0xff


## Crack bcrypt $2*$, Blowfish (Unix) com mascara de 4 letras minúsculas

$hashcat --help | grep Unix

$hashcat -a 3 -m 3200 hash-bcrypt.txt ?l?l?l?l

$hashcat -m 3200 hash-bcrypt.txt --show

## Crack sha512crypt $6$, SHA512 (Unix) com wordlist e mascara de 2 números

$hashcat --help | grep SHA512

$hashcat -a 6 -m 1800 hash-sha512.txt /dir/wordlist.txt ?d?d

$hashcat -m 1800 hash-sha512.txt --show

## Links

Fonte: https://www.stationx.net/how-to-use-hashcat

Fonte: https://www.kali.org/tools/hashcat

Fonte: https://hashcat.net/wiki
