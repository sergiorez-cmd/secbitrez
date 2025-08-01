# Online

Search Google generate password hash online

# Linux mkpasswd

$mkpasswd -m help

Available methods:

yescrypt        Yescrypt

gost-yescrypt   GOST Yescrypt

scrypt          scrypt

bcrypt          bcrypt

bcrypt-a        bcrypt (obsolete $2a$ version)

sha512crypt     SHA-512

sha256crypt     SHA-256

sunmd5          SunMD5

md5crypt        MD5

bsdicrypt       BSDI extended DES-based crypt(3)

descrypt        standard 56 bit DES-based crypt(3)

nt              NT-Hash

$mkpasswd -m sha-512 user-password

$openssl passwd user-password
