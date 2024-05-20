# Guia de Estudos TypeScript

Este guia de estudos abrange tópicos essenciais de TypeScript, desde conceitos básicos até funcionalidades avançadas. Utilize este guia como um mapa para sua jornada de aprendizado em TypeScript.

---

## Índice

1. [Introdução ao TypeScript](#introdução-ao-typescript)
2. [Configuração do Ambiente](#configuração-do-ambiente)
3. [Tipos Básicos](#tipos-básicos)
4. [Interfaces e Tipos](#interfaces-e-tipos)
5. [Funções](#funções)
6. [Classes](#classes)
7. [Enums](#enums)
8. [Generics](#generics)
9. [Manipulação de Módulos](#manipulação-de-módulos)
10. [Decorators](#decorators)
11. [Manipulação de Tipos Avançados](#manipulação-de-tipos-avançados)
12. [Configuração do tsconfig.json](#configuração-do-tsconfigjson)
13. [Integração com Bibliotecas JavaScript](#integração-com-bibliotecas-javascript)
14. [Boas Práticas](#boas-práticas)
15. [Ferramentas e Recursos](#ferramentas-e-recursos)

---

## Introdução ao TypeScript

TypeScript é uma linguagem de programação de código aberto desenvolvida pela Microsoft. É um superconjunto de JavaScript que adiciona tipagem estática opcional e recursos avançados de desenvolvimento.

---

## Configuração do Ambiente

### Instalação do TypeScript

```bash
npm install -g typescript
```

### Compilando Arquivos TypeScript

```bash
tsc arquivo.ts
```

### Configurando um Projeto TypeScript

```bash
tsc --init
```

---

## Tipos Básicos

### Tipos Primitivos

```typescript
let nome: string = 'João';
let idade: number = 25;
let ativo: boolean = true;
let indefinido: undefined = undefined;
let nulo: null = null;
```

### Arrays e Tuplas

```typescript
let numeros: number[] = [1, 2, 3];
let lista: Array<number> = [1, 2, 3];

let tupla: [string, number];
tupla = ['Olá', 10];
```

### Enum

```typescript
enum Cor {
  Vermelho,
  Verde,
  Azul
}

let cor: Cor = Cor.Verde;
```

### Any e Unknown

```typescript
let valor: any = 'Olá';
valor = 10;

let desconhecido: unknown = 4;
if (typeof desconhecido === "number") {
  let numero: number = desconhecido;
}
```

---

## Interfaces e Tipos

### Interfaces

```typescript
interface Pessoa {
  nome: string;
  idade: number;
}

let pessoa: Pessoa = { nome: 'João', idade: 30 };
```

### Tipos

```typescript
type Pessoa = {
  nome: string;
  idade: number;
}

let pessoa: Pessoa = { nome: 'João', idade: 30 };
```

### Diferenças entre Interface e Tipo

- Interfaces podem ser extendidas e implementadas por classes.
- Tipos podem representar tipos primitivos, uniões, interseções e tuplas.

---

## Funções

### Tipagem de Parâmetros e Retorno

```typescript
function saudacao(nome: string): string {
  return `Olá, ${nome}!`;
}
```

### Funções Anônimas

```typescript
let saudacao = function (nome: string): string {
  return `Olá, ${nome}!`;
};
```

### Arrow Functions

```typescript
let saudacao = (nome: string): string => `Olá, ${nome}!`;
```

### Parâmetros Opcionais e Padrão

```typescript
function construirNome(primeiroNome: string, ultimoNome?: string): string {
  return `${primeiroNome} ${ultimoNome || ''}`;
}
```

---

## Classes

### Declaração de Classes

```typescript
class Pessoa {
  nome: string;
  idade: number;

  constructor(nome: string, idade: number) {
    this.nome = nome;
    this.idade = idade;
  }

  saudacao(): string {
    return `Olá, meu nome é ${this.nome}`;
  }
}

let joao = new Pessoa('João', 30);
```

### Herança

```typescript
class Funcionario extends Pessoa {
  cargo: string;

  constructor(nome: string, idade: number, cargo: string) {
    super(nome, idade);
    this.cargo = cargo;
  }

  saudacao(): string {
    return `Olá, meu nome é ${this.nome} e eu sou um ${this.cargo}`;
  }
}
```

### Modificadores de Acesso

```typescript
class Pessoa {
  private nome: string;
  protected idade: number;
  public cargo: string;

  constructor(nome: string, idade: number, cargo: string) {
    this.nome = nome;
    this.idade = idade;
    this.cargo = cargo;
  }

  public saudacao(): string {
    return `Olá, meu nome é ${this.nome}`;
  }
}
```

---

## Enums

### Declaração de Enums

```typescript
enum DiaDaSemana {
  Domingo,
  Segunda,
  Terça,
  Quarta,
  Quinta,
  Sexta,
  Sábado
}

let hoje: DiaDaSemana = DiaDaSemana.Sexta;
```

### Enums de String

```typescript
enum Cor {
  Vermelho = "Vermelho",
  Verde = "Verde",
  Azul = "Azul"
}

let cor: Cor = Cor.Verde;
```

---

## Generics

### Funções Genéricas

```typescript
function identidade<T>(valor: T): T {
  return valor;
}

let numero = identidade<number>(10);
let texto = identidade<string>('Olá');
```

### Classes Genéricas

```typescript
class Caixa<T> {
  conteudo: T;

  constructor(conteudo: T) {
    this.conteudo = conteudo;
  }

  getConteudo(): T {
    return this.conteudo;
  }
}

let caixaDeString = new Caixa<string>('Texto');
let caixaDeNumero = new Caixa<number>(123);
```

---

## Manipulação de Módulos

### Exportação e Importação

#### Exportação

```typescript
// arquivo: saudacao.ts
export function saudacao(nome: string): string {
  return `Olá, ${nome}!`;
}
```

#### Importação

```typescript
// arquivo: app.ts
import { saudacao } from './saudacao';

console.log(saudacao('João'));
```

### Exportação Padrão

#### Exportação

```typescript
// arquivo: saudacao.ts
export default function saudacao(nome: string): string {
  return `Olá, ${nome}!`;
}
```

#### Importação

```typescript
// arquivo: app.ts
import saudacao from './saudacao';

console.log(saudacao('João'));
```

---

## Decorators

### Decorators de Classe

```typescript
function logarClasse(construtor: Function) {
  console.log(`Classe criada: ${construtor.name}`);
}

@logarClasse
class Pessoa {
  constructor(public nome: string) {}
}
```

### Decorators de Método

```typescript
function logarMetodo(target: any, propertyKey: string, descriptor: PropertyDescriptor) {
  const metodoOriginal = descriptor.value;
  descriptor.value = function (...args: any[]) {
    console.log(`Método ${propertyKey} chamado com argumentos: ${JSON.stringify(args)}`);
    return metodoOriginal.apply(this, args);
  };
}

class Pessoa {
  constructor(public nome: string) {}

  @logarMetodo
  saudacao(mensagem: string): string {
    return `${mensagem}, ${this.nome}`;
  }
}
```

---

## Manipulação de Tipos Avançados

### Union Types

```typescript
let id: number | string;
id = 10;
id = 'ABC123';
```

### Intersection Types

```typescript
interface Pessoa {
  nome: string;
}

interface Funcionario {
  salario: number;
}

type FuncionarioDetalhado = Pessoa & Funcionario;

let funcionario: FuncionarioDetalhado = { nome: 'João', salario: 1000 };
```

### Type Guards

```typescript
function exibirID(id: number | string) {
  if (typeof id === 'string') {
    console.log(`ID: ${id.toUpperCase()}`);
  } else {
    console.log(`ID: ${id}`);
  }
}
```

### Type Assertions

```typescript
let valor: any = 'Olá';
let tamanho: number = (valor as string).length;
```

---

## Configuração do tsconfig.json

### Exemplo Básico

```json
{
  "compilerOptions": {
    "target": "es6",
    "module": "commonjs",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true
  }
}
```

### Opções Comuns

- **target**: Define a versão do ECMAScript para a qual o código será compilado.
- **module**: Define o sistema de módulos (commonjs, es6, etc.).
- **strict**: Ativa todas as verificações de tipo estritas.
- **esModuleInterop**: Melhora a compatibilidade com módulos

 ES.
- **skipLibCheck**: Ignora a verificação de tipos em arquivos de declaração.
- **forceConsistentCasingInFileNames**: Garante a consistência de maiúsculas/minúsculas nos nomes dos arquivos.

---

## Integração com Bibliotecas JavaScript

### Instalando Tipos de Bibliotecas

```bash
npm install @types/lodash
```

### Exemplo com Lodash

```typescript
import * as _ from 'lodash';

let numeros = [1, 2, 3, 4, 5];
let soma = _.sum(numeros);
console.log(soma);
```

---

## Boas Práticas

- **Usar Tipagem Estrita**: Aproveite o máximo possível a verificação de tipos do TypeScript.
- **Escrever Código Limpo e Legível**: Mantenha o código organizado e fácil de entender.
- **Documentação e Comentários**: Use comentários para explicar partes complexas do código.
- **Usar Interfaces e Tipos**: Utilize interfaces e tipos para descrever a forma dos objetos.
- **Escrever Testes**: Garanta a funcionalidade do código através de testes automatizados.

---

## Ferramentas e Recursos

### Ferramentas

- **TypeScript**: [Site Oficial](https://www.typescriptlang.org/)
- **tslint**: Ferramenta de linting para TypeScript
- **Visual Studio Code**: Editor com excelente suporte a TypeScript

### Recursos

- **Documentação Oficial**: [TypeScript Docs](https://www.typescriptlang.org/docs/)
- **TypeScript Deep Dive**: [Livro Online](https://basarat.gitbook.io/typescript/)
- **TypeScript Handbook**: [Guia Oficial](https://www.typescriptlang.org/docs/handbook/intro.html)

---

Este guia é um ponto de partida. Explore cada tópico, pratique e aprofunde seus conhecimentos para se tornar um desenvolvedor TypeScript proficient. Boa sorte!
