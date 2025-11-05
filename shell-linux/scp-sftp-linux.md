## SCP e SFTP usam a conexão segura do SSH para transferir dados criptografados entre seu computador e o servidor. 

## Usando SCP (Secure Copy)

Abra o terminal no Linux.

Use o comando scp: com a seguinte sintaxe para enviar um arquivo para o servidor remoto:

scp /caminho/do/arquivo/local usuario@ip_do_servidor:/caminho/de/destino/no/servidor

Exemplo: 
```
scp /home/user/doc.txt ssh_user@192.168.1.100:/home/ssh_user
```

## Usando SFTP (SSH File Transfer Protocol)

Abra o terminal no Linux.

Conecte-se ao servidor: com sftp:

sftp usuario@ip_do_servidor

Exemplo:
```
sftp usuario@192.168.1.100
```

Use comandos locais: para navegar no seu computador:

Para ver arquivos no diretório local:
```
!ls
```
Use comandos SFTP: para gerenciar arquivos no servidor remoto:

put /caminho/do/arquivo/local para fazer o upload de um arquivo
```
put /home/kali/script.sh
```

get /caminho/do/arquivo/remoto para baixar um arquivo
```
get /home/user/file.txt
```

Para listar arquivos no servidor remoto
```
ls
```
