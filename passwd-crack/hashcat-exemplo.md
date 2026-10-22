# Exemplo Crack bcrypt via hashcat

1° Gerar um hash de uma senha, copiar o hash e salvar em um arquivo txt

https://bcrypt-generator.com

Ex: 12345678 (somente números)

Ex: Password123456 (Palavra fixa + números)



2° Identificar o tipo do modo para utilizar o hashcat

https://www.kali.org/tools/hashid
```
hashid -m bcrypt-hash.txt
```


3° Executar o hashcat para realizar um ataque de força bruta

https://hashcat.net/wiki
``` 
hashcat -a 3 -m 3200 bcrypt-hash.txt ?d?d?d?d?d?d?d?d
```
```
hashcat -a 3 -m 3200 bcrypt-hash.txt Password?d?d?d?d?d?d
```
