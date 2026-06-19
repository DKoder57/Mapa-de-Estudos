---

tags: [python, oo, erros, exceções, try-except]

área: Python

status: draft

---
# Python - Tratamento de Erros

> [!NOTE] Fonte: _Programação Intermediária com Python — Módulos 1 e 2_ — Prof. Camila Laranjeira / UFMG / SEBRAE (Módulo 2)

## Por que tratar erros?

Erros no sistema precisam ser tratados — seja uma entrada incorreta do usuário, um arquivo inexistente ou uma falha de rede. Tratar nem sempre significa resolver: às vezes é só informar o usuário do que aconteceu.

---

## Tipos de Erro

|Tipo|Descrição|Como tratar|
|---|---|---|
|**Erro de sintaxe** (`SyntaxError`)|Código mal-escrito — o interpretador aponta a linha|Reescrever o trecho|
|**Erro semântico** (exceção em runtime)|Código sintaticamente correto, mas que falha ao executar|Capturar com `try-except`|

---

## LBYL vs EAFP

Dois estilos de lidar com erros potenciais:

```python
data = {'nome': 'Alice', 'idade': 25}

# LBYL — Look Before You Leap (verificar antes)
if 'nome' in data:
    print(data['nome'])

# EAFP — Easier to Ask Forgiveness than Permission (tentar e capturar)
try:
    print(data['nome'])
except KeyError:
    print("Chave não encontrada.")
```

> [!TIP] Python favorece o estilo **EAFP** — é mais idiomático e geralmente mais legível para casos com múltiplos caminhos de erro.

---

## `try-except` Básico

```python
try:
    resultado = 10 / int(input("Divisor: "))
except ZeroDivisionError as e:
    print(f"Erro: divisão por zero — {e}")
except ValueError as e:
    print(f"Erro: entrada inválida — {e}")
```

- O tipo do erro na cláusula `except` é opcional, mas recomendado para tratamentos específicos
- Múltiplas cláusulas `except` devem estar ordenadas da **mais específica para a mais genérica**

---

## Hierarquia de Exceções

Exceções são classes organizadas em hierarquia de herança. Capturar uma exceção pai captura todas as filhas:

```
BaseException
└── Exception
    ├── ArithmeticError
    │   └── ZeroDivisionError
    ├── AttributeError
    ├── OSError
    │   ├── FileNotFoundError
    │   ├── PermissionError
    │   └── ConnectionError
    ├── TypeError
    ├── ValueError
    └── KeyError
```

```python
try:
    fp = open('arquivo.txt', 'r')
except OSError:                       # captura FileNotFoundError também
    print("Erro de sistema operacional")
except FileNotFoundError:             # ⚠️ nunca executará — OSError vem antes
    print("Isso nunca vai executar")
```

> [!NOTE] Para capturar qualquer exceção sem especificar, use `except:` (implicitamente `BaseException`). Use com cautela — pode mascarar erros inesperados.

---

## Estrutura Completa: `try-except-else-finally`

```python
try:
    fp = open('dados.txt', 'r')
    conteudo = fp.read()
except FileNotFoundError:
    print("Arquivo não encontrado!")
except PermissionError:
    print("Sem permissão para ler o arquivo!")
else:
    # executa SOMENTE se nenhuma exceção ocorreu
    print(f"Lido com sucesso: {len(conteudo)} caracteres")
finally:
    # executa SEMPRE — com ou sem exceção
    print("Encerrando operação de leitura")
    # bom lugar para fechar recursos
```

|Bloco|Quando executa|
|---|---|
|`try`|Sempre (código que pode falhar)|
|`except`|Somente se a exceção correspondente for lançada|
|`else`|Somente se **nenhuma** exceção ocorreu|
|`finally`|**Sempre** — ideal para liberar recursos|

---

## `raise` — Lançando Exceções

```python
def dividir(a, b):
    if b == 0:
        raise ValueError("O divisor não pode ser zero!")
    return a / b

try:
    dividir(10, 0)
except ValueError as e:
    print(e)
```

---

## Criando Exceções Customizadas

Basta criar uma subclasse do tipo de exceção que deseja especializar:

```python
class SaldoInsuficienteError(ValueError):
    def __init__(self, saldo, valor):
        self.saldo = saldo
        self.valor = valor
        super().__init__(
            f"Saldo insuficiente: tem R${saldo:.2f}, tentou sacar R${valor:.2f}"
        )

class ContaBancaria:
    def __init__(self, saldo):
        self.saldo = saldo

    def sacar(self, valor):
        if valor > self.saldo:
            raise SaldoInsuficienteError(self.saldo, valor)
        self.saldo -= valor

conta = ContaBancaria(100)
try:
    conta.sacar(200)
except SaldoInsuficienteError as e:
    print(e)
    print(f"Saldo atual: R${e.saldo:.2f}")
```

---

## Links Relacionados

- [[Python - Classes e Atributos]]
- [[Python - Pilares da OO]]
- [[Python - Herança e Polimorfismo]]
- [[Python - Pydantic e Validação de Dados]]