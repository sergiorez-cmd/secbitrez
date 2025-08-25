## Dir Wordlists Kali

$ wordlists

/usr/share/wordlists/

## Criar Worlists Personalizadas 

Exemplo para criar wordlist de letras e números min=4 max=8

$ crunch 4 8 abcdef1234567890 -o hex-wordlist.txt

Exemplo para criar wordlist parte fixa * e números % ramdômicos min=16 max=16

$ crunch 16 16 -t password*%%%%%%%% -o custom-wordlist.txt

Exemplo para criar uma wordlist de palavras com comprimento de 8 caracteres

$ grep -oE '\b\w{8}\b' /usr/share/wordlists/rockyou.txt > custom-worlist.txt

$ wc -l custom-worlist.txt

## Links

https://github.com/danielmiessler/SecLists

https://weakpass.com
