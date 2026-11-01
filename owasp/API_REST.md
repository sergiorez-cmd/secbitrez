# Guia Prático: API REST com Node.js, Express e SQLite


Uma API REST (ou API RESTful) é uma interface de programação de aplicações que segue os princípios do estilo arquitetural REST (Representational State Transfer). Ela permite a comunicação e a troca de dados entre diferentes sistemas pela internet usando o protocolo HTTP. 

__O que significa ser REST?__

Para uma API ser considerada RESTful, ela precisa seguir certas regras arquiteturais, como: 

• __Cliente-Servidor:__ Separa a interface do usuário (quem pede) da lógica e do armazenamento de dados (quem responde). 

• __Sem estado (Stateless):__ Cada requisição enviada pelo cliente deve conter todas as informações necessárias para que o servidor a compreenda e processe; o servidor não guarda o histórico de sessões anteriores. 

• __Cacheável:__ As respostas precisam informar se podem ou não ser armazenadas em cache para reduzir o tráfego e melhorar a velocidade. 

• __Interface uniforme:__ Padroniza a forma como os recursos são identificados e manipulados. 

• __Sistema em camadas:__ O cliente pode estar se comunicando com um intermediário (como um balanceador de carga ou proxy) sem precisar saber se é o servidor final. 

__Como funciona na prática?__

A comunicação acontece através de métodos (verbos) HTTP aplicados a recursos (identificados por URLs):

• __GET:__ Solicita a leitura ou busca de informações.

• __POST:__ Cria um novo recurso.

• __PUT:__ Atualiza um recurso por completo.

• __PATCH:__ Atualiza parcialmente um recurso.

• __DELETE:__ Remove um recurso. 

Os dados trocados entre o cliente e o servidor são comumente estruturados no formato JSON (JavaScript Object Notation), embora XML também possa ser usado. 

A resposta do servidor sempre inclui um código de status HTTP indicando o resultado (por exemplo, 200 para sucesso, 201 para criado, 304 para não modificado, 404 para não encontrado ou 500 para erro no servidor). 

Você pode explorar mais definições conceituais no glossário do MDN Web Docs ou entender as bases da AWS e do Google Cloud.

[MDN Web Docs](https://developer.mozilla.org/pt-BR/docs/Glossary/REST)

[What is REST API](https://cloud.google.com/discover/what-is-rest-api?hl=pt-BR)

[Restfull API](https://aws.amazon.com/pt/what-is/restful-api/)

Este documento reúne o passo a passo para a criação de uma API RESTful utilizando o ambiente de execução **Node.js**, o framework **Express** para gerenciamento de rotas HTTP, e o banco de dados **SQLite** para persistência local de dados através do padrão de Promises (`async/await`).

---

## 1. Configuração do Ambiente e Instalação

Para iniciar o projeto, crie uma pasta, abra o terminal nela e execute os seguintes comandos:

```bash
# Inicializar o gerenciador de pacotes do Node.js
npm init -y

# Instalar o Express e as bibliotecas do SQLite
npm install express sqlite3 sqlite
```

---

## 2. Código Fonte da API (`index.js`)

Crie um arquivo chamado `index.js` e insira o código estruturado abaixo:

```javascript
const express = require('express');
const sqlite3 = require('sqlite3');
const { open } = require('sqlite');

const app = express();
const PORT = 3000;

// Middleware para permitir que a API interprete corpos de requisição em JSON
app.use(express.json());

let db;

// Função assíncrona para iniciar o banco de dados e criar a tabela se não existir
async function iniciarBanco() {
    db = await open({
        filename: './database.db',
        driver: sqlite3.Database
    });

    await db.exec(`
        CREATE TABLE IF NOT EXISTS usuarios (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            nome TEXT NOT NULL
        )
    `);
    console.log('Banco de dados SQLite conectado e pronto.');
}

// Rota GET: Buscar todos os usuários cadastrados
app.get('/usuarios', async (req, res) => {
    try {
        const usuarios = await db.all('SELECT * FROM usuarios');
        res.status(200).json(usuarios);
    } catch (error) {
        res.status(500).json({ erro: 'Erro ao buscar usuários' });
    }
});

// Rota POST: Criar um novo usuário
app.post('/usuarios', async (req, res) => {
    const { nome } = req.body;
    if (!nome) {
        return res.status(400).json({ erro: 'O nome é obrigatório' });
    }

    try {
        const resultado = await db.run('INSERT INTO usuarios (nome) VALUES (?)', [nome]);
        res.status(201).json({ id: resultado.lastID, nome });
    } catch (error) {
        res.status(500).json({ erro: 'Erro ao salvar usuário' });
    }
});

// Rota DELETE: Remover um usuário pelo ID enviado na URL
app.delete('/usuarios/:id', async (req, res) => {
    const { id } = req.params;
    try {
        await db.run('DELETE FROM usuarios WHERE id = ?', [id]);
        res.status(204).send();
    } catch (error) {
        res.status(500).json({ erro: 'Erro ao deletar usuário' });
    }
});

// Inicialização segura: Garante a conexão com o banco antes de escutar na porta HTTP
iniciarBanco().then(() => {
    app.listen(PORT, () => {
        console.log(`Servidor rodando em http://localhost:${PORT}`);
    });
});
```

---

## 3. Conceitos e Boas Práticas Aplicadas

* **Persistência Real:** Diferente de arrays em memória, os dados são salvos fisicamente no arquivo `database.db`, sobrevivendo a reinicializações do servidor.
* **Async/Await:** Utilizado para gerenciar operações assíncronas de I/O do banco de dados sem travar o loop de eventos principal do Node.js.
* **Prevenção de SQL Injection:** O uso de marcadores `?` (parâmetros parametrizados) na query `WHERE id = ?` neutraliza injeções maliciosas de código SQL.
* **Códigos de Status HTTP Semânticos:** 
  * `200 OK` para consultas bem-sucedidas.
  * `201 Created` para inserções com sucesso.
  * `204 No Content` para remoções sem retorno de corpo.
  * `400 Bad Request` para erros de validação do cliente.
  * `500 Internal Server Error` para falhas inesperadas no servidor.

---

## 4. Como Executar e Testar

1. No terminal, execute o comando:
   ```bash
   node index.js
   ```
2. Utilize uma ferramenta como **Postman**, **Insomnia** ou a extensão **REST Client** do VS Code para disparar requisições para `http://localhost:3000/usuarios`.
