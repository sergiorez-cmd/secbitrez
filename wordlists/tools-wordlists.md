# WordlistCTL

https://github.com/BlackArch/wordlistctl

# CeWL

https://github.com/digininja/CeWL

# Mentalist

https://github.com/sc0tfree/mentalist/releases/tag/v1.0

# TTPassGen

https://github.com/tp7309/TTPassGen

$ python3 -m venv my_venv 

$ source my_venv/bin/activate

$ (my_venv)─(kali㉿kali)-[~]

$ python -m pip install ttpassgen

$ ttpassgen --rule '[?d]{4:4:*}' pin.txt

$ ttpassgen --rule '[?l]{1:3:*}' abc.txt

$ ttpassgen --dictlist 'pin.txt,abc.txt' --rule '$0[-]{1}$1' combination.txt

# Dir Wordlists Kali

$ wordlists

/usr/share/wordlists/

# Criar Worlists Personalizadas

Exemplo para criar wordlist de letras e números min=4 max=8

$ crunch 4 8 abcdef1234567890 -o hex-wordlist.txt

Exemplo para criar wordlist parte fixa * e números % ramdômicos min=16 max=16

$ crunch 16 16 -t password*%%%%%%%% -o custom-wordlist.txt

Exemplo para criar uma wordlist de palavras com comprimento de 8 caracteres via GREP

$ grep -oE '\b\w{8}\b' /usr/share/wordlists/rockyou.txt > custom-wordlist.txt

$ wc -l custom-wordlist.txt

## Links

https://github.com/danielmiessler/SecLists

https://weakpass.com

