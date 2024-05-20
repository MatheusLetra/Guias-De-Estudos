# Guia de Estudos Node.js

Este guia de estudos abrange tópicos essenciais de Node.js, desde conceitos básicos até funcionalidades avançadas. Utilize este guia como um mapa para sua jornada de aprendizado em Node.js.

---

## Índice

1. [Introdução ao Node.js](#introdução-ao-nodejs)
2. [Configuração do Ambiente](#configuração-do-ambiente)
3. [Módulos Node.js](#módulos-nodejs)
4. [Manipulação de Arquivos](#manipulação-de-arquivos)
5. [Eventos](#eventos)
6. [Streams](#streams)
7. [Trabalhando com HTTP](#trabalhando-com-http)
8. [Express.js](#expressjs)
9. [Banco de Dados](#banco-de-dados)
10. [Autenticação e Autorização](#autenticação-e-autorização)
11. [Testes](#testes)
12. [Boas Práticas](#boas-práticas)
13. [Ferramentas e Recursos](#ferramentas-e-recursos)

---

## Introdução ao Node.js

Node.js é uma plataforma construída sobre o motor JavaScript V8 do Google Chrome, utilizada para construir aplicações de rede rápidas e escaláveis. Node.js utiliza um modelo de I/O não bloqueante e orientado a eventos, tornando-o leve e eficiente.

---

## Configuração do Ambiente

### Instalação do Node.js

1. Baixe e instale o Node.js a partir do [site oficial](https://nodejs.org/).
2. Verifique a instalação:

```bash
node -v
npm -v
```

### Iniciando um Projeto Node.js

```bash
mkdir meu-projeto
cd meu-projeto
npm init -y
```

### Instalando Dependências

```bash
npm install express
```

---

## Módulos Node.js

### Importando e Exportando Módulos

#### Exportação

```javascript
// arquivo: saudacao.js
module.exports = function(nome) {
  return `Olá, ${nome}!`;
};
```

#### Importação

```javascript
// arquivo: app.js
const saudacao = require('./saudacao');
console.log(saudacao('João'));
```

### Módulos Nativos

```javascript
const fs = require('fs');
const path = require('path');
```

---

## Manipulação de Arquivos

### Lendo Arquivos

```javascript
const fs = require('fs');

fs.readFile('arquivo.txt', 'utf8', (err, data) => {
  if (err) {
    console.error(err);
    return;
  }
  console.log(data);
});
```

### Escrevendo Arquivos

```javascript
fs.writeFile('arquivo.txt', 'Olá, Mundo!', err => {
  if (err) {
    console.error(err);
    return;
  }
  console.log('Arquivo escrito com sucesso!');
});
```

### Apêndice em Arquivos

```javascript
fs.appendFile('arquivo.txt', ' Mais texto.', err => {
  if (err) {
    console.error(err);
    return;
  }
  console.log('Texto adicionado com sucesso!');
});
```

---

## Eventos

### Emissor de Eventos

```javascript
const EventEmitter = require('events');
class MeuEmissor extends EventEmitter {}

const meuEmissor = new MeuEmissor();
meuEmissor.on('evento', () => {
  console.log('Evento disparado!');
});

meuEmissor.emit('evento');
```

---

## Streams

### Leitura de Streams

```javascript
const fs = require('fs');
const stream = fs.createReadStream('arquivo.txt', 'utf8');

stream.on('data', chunk => {
  console.log(`Chunk recebido: ${chunk}`);
});
```

### Escrita em Streams

```javascript
const fs = require('fs');
const stream = fs.createWriteStream('arquivo.txt');

stream.write('Olá, ');
stream.write('Mundo!');
stream.end();
```

---

## Trabalhando com HTTP

### Servidor HTTP Básico

```javascript
const http = require('http');

const servidor = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Olá, Mundo!\n');
});

servidor.listen(3000, '127.0.0.1', () => {
  console.log('Servidor rodando em http://127.0.0.1:3000/');
});
```

---

## Express.js

### Configuração Básica

```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.send('Olá, Mundo!');
});

app.listen(3000, () => {
  console.log('Servidor rodando na porta 3000');
});
```

### Middleware

```javascript
app.use((req, res, next) => {
  console.log(`${req.method} ${req.url}`);
  next();
});
```

### Rotas

```javascript
app.get('/usuarios', (req, res) => {
  res.json([{ nome: 'João' }, { nome: 'Maria' }]);
});
```

---

## Banco de Dados

### MongoDB com Mongoose

#### Instalação

```bash
npm install mongoose
```

#### Conexão e Modelos

```javascript
const mongoose = require('mongoose');

mongoose.connect('mongodb://localhost/meu_banco', { useNewUrlParser: true, useUnifiedTopology: true });

const Usuario = mongoose.model('Usuario', { nome: String });

const novoUsuario = new Usuario({ nome: 'João' });
novoUsuario.save().then(() => console.log('Usuário salvo'));
```

---

## Autenticação e Autorização

### JSON Web Tokens (JWT)

#### Instalação

```bash
npm install jsonwebtoken
```

#### Geração e Verificação de Token

```javascript
const jwt = require('jsonwebtoken');
const segredo = 'meu_segredo';

const token = jwt.sign({ id: 123 }, segredo, { expiresIn: '1h' });

jwt.verify(token, segredo, (err, decoded) => {
  if (err) {
    console.error('Token inválido');
    return;
  }
  console.log('Token válido:', decoded);
});
```

### Middleware de Autenticação

```javascript
app.use((req, res, next) => {
  const token = req.headers['authorization'];
  if (!token) {
    return res.status(401).send('Acesso negado');
  }

  jwt.verify(token, segredo, (err, decoded) => {
    if (err) {
      return res.status(401).send('Token inválido');
    }
    req.user = decoded;
    next();
  });
});
```

---

## Testes

### Mocha e Chai

#### Instalação

```bash
npm install mocha chai
```

#### Exemplo de Teste

```javascript
const chai = require('chai');
const expect = chai.expect;

describe('Teste de exemplo', () => {
  it('deve retornar verdadeiro', () => {
    expect(true).to.be.true;
  });
});
```

### Supertest para Testes de API

#### Instalação

```bash
npm install supertest
```

#### Exemplo de Teste de API

```javascript
const request = require('supertest');
const express = require('express');
const app = express();

app.get('/usuarios', (req, res) => {
  res.json([{ nome: 'João' }]);
});

describe('GET /usuarios', () => {
  it('deve responder com JSON', (done) => {
    request(app)
      .get('/usuarios')
      .expect('Content-Type', /json/)
      .expect(200, done);
  });
});
```

---

## Boas Práticas

- **Modularize seu código**: Separe funcionalidades em módulos distintos.
- **Escreva testes**: Garanta que seu código funcione como esperado.
- **Use ferramentas de linting**: Mantenha seu código limpo e consistente.
- **Gerencie variáveis de ambiente**: Utilize arquivos `.env` para configurações sensíveis.
- **Documente seu código**: Facilite a manutenção e o entendimento do código.

---

## Ferramentas e Recursos

### Ferramentas

- **Node.js**: [Site Oficial](https://nodejs.org/)
- **Express.js**: [Documentação Oficial](https://expressjs.com/)
- **MongoDB**: [Site Oficial](https://www.mongodb.com/)
- **Mongoose**: [Documentação Oficial](https://mongoosejs.com/)

### Recursos

- **Node.js Docs**: [Documentação Oficial](https://nodejs.org/en/docs/)
- **NPM**: [Site Oficial](https://www.npmjs.com/)
- **MDN Web Docs**: [Node.js Guia](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Node_server_without_framework)
- **Egghead.io**: [Tutoriais de Node.js](https://egghead.io/technologies/node)

---

Este guia é um ponto de partida. Explore cada tópico, pratique e aprofunde seus conhecimentos para se tornar um desenvolvedor Node.js proficient. Boa sorte!
