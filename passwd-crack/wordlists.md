## Dir Wordlists Kali

$ wordlists

/usr/share/wordlists/

## Criar Worlists Personalizadas 

Exemplo para criar uma wordlist de palavras com comprimento de 8 caracteres

Exemplo criar wordlist de letras e números via Crunch min=4 max=8

$ crunch 4 8 abcdef1234567890 -o hex-wordlist.txt

$ grep -oE '\b\w{8}\b' /usr/share/wordlists/rockyou.txt > passwd-8lt.txt

$ wc -l passwd-8lt.txt

## Links

https://github.com/danielmiessler/SecLists

https://weakpass.com
