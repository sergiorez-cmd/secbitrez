# Filtrar Texto Terminal Linux

Comando
Função
`$cut -d ',' -f 1,3 arquivo.txt`
Filtrar delimitado por vírgula 1° e 2° coluna
`$awk '{print $1, $3}' arquivo.txt`
Filtrar 1° e 3° coluna separado por espaço
`$sort -d arquivo.txt`
Ordenar em ordem alfabética
`$uniq arquivo.txt`
Remove linhas duplicadas
`$uniq -c arquivo.txt`
Mostra número de linhas duplicadas
`$uniq -d arquivo.txt`
Mostra somente linhas únicas
`$uniq -u arquivo.txt`
Mostra somente linhas duplicadas
`$wc -l` 
Conta linhas de um arquivo
`$cat arquivo.txt | tr a-z A-Z`
Converter para letras maiúsculas
`$cat arquivo.txt | tr A-Z a-z`
Converter para letras minúsculas
`$grep -i port /etc/ssh/sshd_config`
Filtrar por palavras 
`$grep '^....$' arquivo.txt`
Filtrar palavras de 4 caracteres
`$grep -oE '\b\w{5}\b' arquivo.txt`
Filtrar palavras de 5 caracteres
`$grep -v '^$' arquivo.txt`
Remover linhas em branco
`$sed -i '/^$/d' arquivo.txt`
Remover linhas em branco e subscrever
`$sed -i 's/"//g' arquivo.txt`
Remover aspas duplas e subscrever
`$sed -i 's/[[:space:]]//g' arquivo.txt`
Remover todos espaços em branco
`$sed -i 's/\.//g' arquivo.txt`
Remover todos pontos e subscrever
`$sed -i 's/\(.\)/\L\1/' arquivo.txt`
Alterar 1° letra para minúscula
`$sed -i 's/\(.\)/\u\1/' arquivo.txt`
Alterar 1° letra para maiúscula
`$sed -i 's/192.168.1.1/10.0.0.1/' config.txt`
Alterar parâmetros de um arquivo
`$sed -i 's/word1/word2/g'  arquivo.txt`
Alterar todas palavras de um arquivo
`$paste -d ‘@’ names.txt mail.txt`
Concatena palavras de 2 arquivos
`$cat arquivo1 arquivo2 > arquivo3`
Concatena 2 arquivos


Ex; cat log.txt | grep "error" | awk '{print $2, $3}' | sort | uniq
