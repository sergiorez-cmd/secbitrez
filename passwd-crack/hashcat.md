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

Fonte: https://www.stationx.net/how-to-use-hashcat

Fonte: https://www.kali.org/tools/hashcat

Fonte: https://hashcat.net/wiki
