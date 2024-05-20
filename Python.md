# Guia de Estudos Python

Este guia de estudos abrange tópicos essenciais de Python, desde conceitos básicos até funcionalidades avançadas. Utilize este guia como um mapa para sua jornada de aprendizado em Python.

---

## Índice

1. [Introdução ao Python](#introdução-ao-python)
2. [Configuração do Ambiente](#configuração-do-ambiente)
3. [Sintaxe Básica](#sintaxe-básica)
4. [Estruturas de Dados](#estruturas-de-dados)
5. [Funções](#funções)
6. [Programação Orientada a Objetos](#programação-orientada-a-objetos)
7. [Módulos e Pacotes](#módulos-e-pacotes)
8. [Manipulação de Arquivos](#manipulação-de-arquivos)
9. [Exceções](#exceções)
10. [Bibliotecas Populares](#bibliotecas-populares)
11. [Testes](#testes)
12. [Boas Práticas](#boas-práticas)
13. [Ferramentas e Recursos](#ferramentas-e-recursos)

---

## Introdução ao Python

Python é uma linguagem de programação de alto nível, interpretada e de propósito geral, conhecida por sua sintaxe clara e legibilidade. É amplamente utilizada em diversos campos, incluindo desenvolvimento web, análise de dados, inteligência artificial e automação de tarefas.

---

## Configuração do Ambiente

### Instalação do Python

1. Baixe e instale o Python a partir do [site oficial](https://www.python.org/).
2. Verifique a instalação:

```bash
python --version
```

### Configuração de um Ambiente Virtual

```bash
python -m venv meuambiente
source meuambiente/bin/activate  # No Windows: meuambiente\Scripts\activate
```

### Instalando Pacotes com pip

```bash
pip install requests
```

---

## Sintaxe Básica

### Variáveis e Tipos de Dados

```python
nome = "João"
idade = 30
altura = 1.75
is_programador = True
```

### Operadores

```python
# Aritméticos
soma = 5 + 3
subtracao = 10 - 2
multiplicacao = 4 * 7
divisao = 15 / 3
modulo = 10 % 3

# Comparação
maior = 5 > 3
igual = 5 == 5

# Lógicos
e = True and False
ou = True or False
```

### Estruturas de Controle

```python
# Condicionais
if idade > 18:
    print("Maior de idade")
else:
    print("Menor de idade")

# Laços de Repetição
for i in range(5):
    print(i)

while idade < 18:
    idade += 1
```

### Funções

```python
def saudacao(nome):
    return f"Olá, {nome}!"

print(saudacao("João"))
```

---

## Estruturas de Dados

### Listas

```python
numeros = [1, 2, 3, 4, 5]
numeros.append(6)
print(numeros[2])  # Acessando o terceiro elemento
```

### Tuplas

```python
cores = ("vermelho", "verde", "azul")
print(cores[1])
```

### Dicionários

```python
pessoa = {"nome": "João", "idade": 30}
print(pessoa["nome"])
pessoa["altura"] = 1.75
```

### Conjuntos

```python
numeros = {1, 2, 3, 4, 5}
numeros.add(6)
```

---

## Funções

### Funções com Argumentos e Retorno

```python
def somar(a, b):
    return a + b

resultado = somar(5, 3)
```

### Argumentos Padrão

```python
def saudacao(nome="visitante"):
    return f"Olá, {nome}!"

print(saudacao())
```

### Funções Lambda

```python
dobro = lambda x: x * 2
print(dobro(5))
```

### Funções Aninhadas

```python
def pai():
    print("Dentro da função pai")

    def filho():
        print("Dentro da função filho")

    filho()

pai()
```

---

## Programação Orientada a Objetos

### Classes e Objetos

```python
class Pessoa:
    def __init__(self, nome, idade):
        self.nome = nome
        self.idade = idade

    def saudacao(self):
        return f"Olá, meu nome é {self.nome} e eu tenho {self.idade} anos."

p1 = Pessoa("João", 30)
print(p1.saudacao())
```

### Herança

```python
class Estudante(Pessoa):
    def __init__(self, nome, idade, matricula):
        super().__init__(nome, idade)
        self.matricula = matricula

    def saudacao(self):
        return f"Olá, meu nome é {self.nome}, tenho {self.idade} anos e minha matrícula é {self.matricula}."

e1 = Estudante("Maria", 20, "12345")
print(e1.saudacao())
```

---

## Módulos e Pacotes

### Criando e Importando Módulos

#### saudacao.py

```python
def saudacao(nome):
    return f"Olá, {nome}!"
```

#### app.py

```python
from saudacao import saudacao

print(saudacao("João"))
```

### Pacotes

#### Estrutura de Diretórios

```plaintext
meu_pacote/
├── __init__.py
├── modulo1.py
└── modulo2.py
```

#### __init__.py

```python
from .modulo1 import func1
from .modulo2 import func2
```

#### Usando o Pacote

```python
from meu_pacote import func1, func2
```

---

## Manipulação de Arquivos

### Leitura de Arquivos

```python
with open('arquivo.txt', 'r') as file:
    conteudo = file.read()
    print(conteudo)
```

### Escrita em Arquivos

```python
with open('arquivo.txt', 'w') as file:
    file.write('Olá, Mundo!')
```

### Apêndice em Arquivos

```python
with open('arquivo.txt', 'a') as file:
    file.write(' Mais texto.')
```

---

## Exceções

### Tratamento de Exceções

```python
try:
    resultado = 10 / 0
except ZeroDivisionError:
    print("Erro: Divisão por zero")
except Exception as e:
    print(f"Erro: {e}")
finally:
    print("Bloco finally executado")
```

### Lançando Exceções

```python
def divide(a, b):
    if b == 0:
        raise ValueError("O divisor não pode ser zero")
    return a / b
```

---

## Bibliotecas Populares

### requests

```bash
pip install requests
```

```python
import requests

response = requests.get('https://api.github.com')
print(response.json())
```

### numpy

```bash
pip install numpy
```

```python
import numpy as np

arr = np.array([1, 2, 3, 4, 5])
print(arr.mean())
```

### pandas

```bash
pip install pandas
```

```python
import pandas as pd

df = pd.DataFrame({'Nome': ['João', 'Maria'], 'Idade': [30, 25]})
print(df)
```

### matplotlib

```bash
pip install matplotlib
```

```python
import matplotlib.pyplot as plt

plt.plot([1, 2, 3, 4], [1, 4, 9, 16])
plt.show()
```

---

## Testes

### unittest

```python
import unittest

def soma(a, b):
    return a + b

class TestSoma(unittest.TestCase):
    def test_soma(self):
        self.assertEqual(soma(1, 2), 3)

if __name__ == '__main__':
    unittest.main()
```

### pytest

```bash
pip install pytest
```

```python
# test_soma.py
from app import soma

def test_soma():
    assert soma(1, 2) == 3
```

```bash
pytest
```

---

## Boas Práticas

- **Escreva Código Legível**: Use nomes de variáveis e funções descritivas.
- **Documente seu Código**: Utilize docstrings para documentar funções e classes.
- **Escreva Testes**: Garanta que seu código funcione como esperado.
- **Siga PEP 8**: Adote o guia de estilo oficial do Python.
- **Use Gerenciamento de Dependências**: Utilize ambientes virtuais e o arquivo `requirements.txt`.

---

## Ferramentas e Recursos

### Ferramentas

- **Python**: [Site Oficial](https://www.python.org/)
- **pip**: [Documentação](https://pip.pypa.io/en/stable/)
- **virtualenv**: [Documentação](https://virtualenv.pypa)
