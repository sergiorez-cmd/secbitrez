# Online

Search Google generate password hash online

# Linux mkpasswd

$mkpasswd -m help

Available methods:

yescrypt       

gost-yescrypt  

scrypt         

bcrypt         

bcrypt-a        bcrypt (obsolete $2a$ version)

sha512crypt    

sha256crypt     

sunmd5          

md5crypt       

bsdicrypt       BSDI extended DES-based crypt(3)

descrypt        standard 56 bit DES-based crypt(3)

nt              NT-Hash

$mkpasswd -m sha-512crypt <user-password>

# OpenSSL Passwd

$openssl passwd user-password
