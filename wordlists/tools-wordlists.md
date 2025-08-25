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

Exemplo criar wordlist de letras e números via Crunch min=4 max=8

$ crunch 4 8 abcdef1234567890 -o wordlist.txt

Exemplo para criar uma wordlist de palavras com comprimento de 8 caracteres via GREP

$ grep -oE '\b\w{8}\b' /usr/share/wordlists/rockyou.txt > passwd-8lt.txt

$ wc -l passwd-8lt.txt

## Links

https://github.com/danielmiessler/SecLists

https://weakpass.com

