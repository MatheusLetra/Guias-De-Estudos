# Guia de Estudos React.js

Este guia de estudos abrange tópicos essenciais de React.js, desde conceitos básicos até funcionalidades avançadas. Utilize este guia como um mapa para sua jornada de aprendizado em React.js.

---

## Índice

1. [Introdução ao React.js](#introdução-ao-reactjs)
2. [Configuração do Ambiente](#configuração-do-ambiente)
3. [Componentes](#componentes)
4. [JSX](#jsx)
5. [Props e State](#props-e-state)
6. [Ciclo de Vida dos Componentes](#ciclo-de-vida-dos-componentes)
7. [Eventos](#eventos)
8. [Formulários](#formulários)
9. [Estilização](#estilização)
10. [React Router](#react-router)
11. [Hooks](#hooks)
12. [Context API](#context-api)
13. [Gerenciamento de Estado](#gerenciamento-de-estado)
14. [Boas Práticas](#boas-práticas)
15. [Ferramentas e Recursos](#ferramentas-e-recursos)

---

## Introdução ao React.js

React.js é uma biblioteca JavaScript para construir interfaces de usuário, mantida pelo Facebook e por uma comunidade de desenvolvedores. React permite a criação de componentes reutilizáveis e de fácil manutenção.

---

## Configuração do Ambiente

### Instalação do Create React App

```bash
npx create-react-app meu-app
cd meu-app
npm start
```

### Estrutura do Projeto

```plaintext
meu-app/
├── node_modules/
├── public/
├── src/
│   ├── App.css
│   ├── App.js
│   ├── App.test.js
│   ├── index.css
│   ├── index.js
│   ├── logo.svg
│   └── serviceWorker.js
├── .gitignore
├── package.json
├── README.md
└── yarn.lock
```

---

## Componentes

### Componente Funcional

```javascript
import React from 'react';

function Saudacao(props) {
  return <h1>Olá, {props.nome}</h1>;
}

export default Saudacao;
```

### Componente de Classe

```javascript
import React, { Component } from 'react';

class Saudacao extends Component {
  render() {
    return <h1>Olá, {this.props.nome}</h1>;
  }
}

export default Saudacao;
```

---

## JSX

### Sintaxe Básica

```javascript
const elemento = <h1>Olá, Mundo!</h1>;
```

### Expressões em JSX

```javascript
const nome = 'João';
const elemento = <h1>Olá, {nome}!</h1>;
```

### Atributos em JSX

```javascript
const elemento = <img src="logo.png" alt="Logo" />;
```

---

## Props e State

### Props

```javascript
function Saudacao(props) {
  return <h1>Olá, {props.nome}</h1>;
}

<Saudacao nome="João" />;
```

### State

```javascript
class Contador extends React.Component {
  constructor(props) {
    super(props);
    this.state = { contador: 0 };
  }

  incrementar = () => {
    this.setState({ contador: this.state.contador + 1 });
  };

  render() {
    return (
      <div>
        <p>{this.state.contador}</p>
        <button onClick={this.incrementar}>Incrementar</button>
      </div>
    );
  }
}
```

---

## Ciclo de Vida dos Componentes

### Métodos de Ciclo de Vida

- **componentDidMount**: Chamado após o componente ser montado no DOM.
- **componentDidUpdate**: Chamado após o componente ser atualizado.
- **componentWillUnmount**: Chamado antes do componente ser desmontado e destruído.

```javascript
class ExemploCicloDeVida extends React.Component {
  componentDidMount() {
    console.log('Componente montado');
  }

  componentDidUpdate() {
    console.log('Componente atualizado');
  }

  componentWillUnmount() {
    console.log('Componente será desmontado');
  }

  render() {
    return <div>Veja o console para os métodos de ciclo de vida</div>;
  }
}
```

---

## Eventos

### Manipulação de Eventos

```javascript
function Botao() {
  function handleClick() {
    alert('Botão clicado!');
  }

  return <button onClick={handleClick}>Clique em mim</button>;
}
```

### Eventos em Componentes de Classe

```javascript
class Botao extends React.Component {
  handleClick = () => {
    alert('Botão clicado!');
  };

  render() {
    return <button onClick={this.handleClick}>Clique em mim</button>;
  }
}
```

---

## Formulários

### Manipulação de Formulários

```javascript
class Formulario extends React.Component {
  constructor(props) {
    super(props);
    this.state = { valor: '' };
  }

  handleChange = (event) => {
    this.setState({ valor: event.target.value });
  };

  handleSubmit = (event) => {
    alert('Um nome foi enviado: ' + this.state.valor);
    event.preventDefault();
  };

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Nome:
          <input type="text" value={this.state.valor} onChange={this.handleChange} />
        </label>
        <button type="submit">Enviar</button>
      </form>
    );
  }
}
```

---

## Estilização

### CSS

```css
/* App.css */
.titulo {
  color: blue;
  font-size: 24px;
}
```

```javascript
import './App.css';

function App() {
  return <h1 className="titulo">Olá, Mundo!</h1>;
}
```

### Styled Components

```bash
npm install styled-components
```

```javascript
import styled from 'styled-components';

const Titulo = styled.h1`
  color: blue;
  font-size: 24px;
`;

function App() {
  return <Titulo>Olá, Mundo!</Titulo>;
}
```

---

## React Router

### Instalação

```bash
npm install react-router-dom
```

### Configuração Básica

```javascript
import React from 'react';
import { BrowserRouter as Router, Route, Switch, Link } from 'react-router-dom';

function Home() {
  return <h2>Home</h2>;
}

function Sobre() {
  return <h2>Sobre</h2>;
}

function App() {
  return (
    <Router>
      <div>
        <nav>
          <ul>
            <li>
              <Link to="/">Home</Link>
            </li>
            <li>
              <Link to="/sobre">Sobre</Link>
            </li>
          </ul>
        </nav>

        <Switch>
          <Route path="/sobre">
            <Sobre />
          </Route>
          <Route path="/">
            <Home />
          </Route>
        </Switch>
      </div>
    </Router>
  );
}

export default App;
```

---

## Hooks

### useState

```javascript
import React, { useState } from 'react';

function Contador() {
  const [contador, setContador] = useState(0);

  return (
    <div>
      <p>{contador}</p>
      <button onClick={() => setContador(contador + 1)}>Incrementar</button>
    </div>
  );
}
```

### useEffect

```javascript
import React, { useState, useEffect } from 'react';

function Exemplo() {
  const [contador, setContador] = useState(0);

  useEffect(() => {
    document.title = `Você clicou ${contador} vezes`;
  }, [contador]);

  return (
    <div>
      <p>Você clicou {contador} vezes</p>
      <button onClick={() => setContador(contador + 1)}>Clique em mim</button>
    </div>
  );
}
```

### useContext

```javascript
import React, { useContext } from 'react';

const TemaContext = React.createContext('claro');

function Titulo() {
  const tema = useContext(TemaContext);
  return <h1 style={{ color: tema === 'claro' ? '#000' : '#fff' }}>Tema Atual: {tema}</h1>;
}

function App() {
  return (
    <TemaContext.Provider value="escuro">
      <Titulo />
    </TemaContext.Provider>
  );
}
```

---

## Context API

### Criando e Usando um Contexto

```javascript
const UsuarioContext = React.createContext();

function UsuarioProvider({ children }) {
  const [usuario, setUsuario] = useState({ nome: 'João' });

  return (
    <UsuarioContext.Provider value={usuario}>
      {children}
    </UsuarioContext.Provider>
  );
}

function MostrarUsuario() {
  const usuario = useContext(UsuarioContext);
  return <p>Nome do usuário: {usuario.nome}</p>;
}

function App() {
  return (
    <UsuarioProvider>
      <MostrarUsuario />
    </UsuarioProvider>
  );
}
```

---

## Gerenciamento de Estado

### Redux

#### Instalação

```bash
npm install redux react-redux
```

#### Configuração Básica

```javascript
import {

 createStore } from 'redux';
import { Provider } from 'react-redux';

const estadoInicial = { contador: 0 };

function contadorReducer(state = estadoInicial, action) {
  switch (action.type) {
    case 'INCREMENTAR':
      return { contador: state.contador + 1 };
    default:
      return state;
  }
}

const store = createStore(contadorReducer);

function App() {
  return (
    <Provider store={store}>
      <Contador />
    </Provider>
  );
}

export default App;
```

#### Usando Redux com Hooks

```javascript
import React from 'react';
import { useSelector, useDispatch } from 'react-redux';

function Contador() {
  const contador = useSelector((state) => state.contador);
  const dispatch = useDispatch();

  return (
    <div>
      <p>{contador}</p>
      <button onClick={() => dispatch({ type: 'INCREMENTAR' })}>Incrementar</button>
    </div>
  );
}
```

---

## Boas Práticas

- **Componentização**: Divida a interface em componentes reutilizáveis.
- **Imutabilidade**: Nunca modifique o state diretamente.
- **Uso de Hooks**: Prefira hooks ao invés de componentes de classe.
- **Escreva Testes**: Garanta a funcionalidade do seu código com testes.
- **Linting**: Utilize ferramentas de linting para manter o código limpo e consistente.
- **Documentação**: Mantenha seu código bem documentado para facilitar a manutenção.

---

## Ferramentas e Recursos

### Ferramentas

- **React.js**: [Site Oficial](https://reactjs.org/)
- **Create React App**: [Documentação](https://create-react-app.dev/)
- **React Router**: [Documentação](https://reactrouter.com/)
- **Redux**: [Documentação](https://redux.js.org/)
- **Styled Components**: [Documentação](https://styled-components.com/)

### Recursos

- **React Docs**: [Documentação Oficial](https://reactjs.org/docs/getting-started.html)
- **Egghead.io**: [Tutoriais de React](https://egghead.io/technologies/react)
- **freeCodeCamp**: [Curso de React](https://www.freecodecamp.org/learn/front-end-libraries/react/)
- **MDN Web Docs**: [Guia de React](https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/React_getting_started)

---

Este guia é um ponto de partida. Explore cada tópico, pratique e aprofunde seus conhecimentos para se tornar um desenvolvedor React.js proficient. Boa sorte!
