# Crack bcrypt via hashcat

**1°** Gerar um hash de uma senha de 8 números, copiar o hash e salvar em um arquivo txt

Ex: 12345678

[https\://bcrypt-generator.com](https://bcrypt-generator.com)


**2°** Identificar o tipo do modo para utilizar o hashcat via hashid

[https\://www\.kali.org/tools/hashid](https://www.kali.org/tools/hashid)
```
hashid -m bcrypt-hash.txt
```

**3°** Executar o hashcat para realizar um ataque de força bruta

[https\://hashcat.net/wiki](https://hashcat.net/wiki)
```
hashcat -a 3 -m 3200 bcrypt-hash.txt ?d?d?d?d?d?d?d?d
```
```
hashcat -m 3200 --show bcrypt-hash.txt
```
