---
tags: [python, instrucoes, expressoes, funcoes-basicas]
área: Python
status: draft
---

# ← [[Python]]

## Instruções

Uma instrução é uma ação executada pelo interpretador Python.

Exemplos:

```python
print("Olá")

x = 10

idade = int(input("Digite sua idade: "))
```

> [!NOTE]
> Instruções realizam ações, mas normalmente não produzem um valor para ser reutilizado.

---

## Expressões

Uma expressão é qualquer construção que produz um valor.

Exemplo:

```python
10 + 5
```

Resultado:

```text
15
```

Outros exemplos:

```python
2 * 3

idade + 1

10 > 5

type("Olá")
```

---

## Expressões Simples

Não possuem operadores.

### Literais

```python
10

3.14

"Olá"
```

### Variáveis

```python
idade
```

### Chamadas de Função

```python
type(10)

input()
```

---

## Expressões Aritméticas

Utilizam operadores matemáticos.

```python
10 + 5

20 - 3

4 * 8

16 / 2
```

### Operadores

|Operador|Descrição|
|---|---|
|`+`|Adição|
|`-`|Subtração|
|`*`|Multiplicação|
|`/`|Divisão|
|`//`|Divisão inteira|
|`%`|Módulo (resto)|
|`**`|Potência|

---

### Divisão x Divisão Inteira

```python
25 / 4
```

Resultado:

```text
6.25
```

```python
25 // 4
```

Resultado:

```text
6
```

```python
25 % 4
```

Resultado:

```text
1
```

---

## Precedência de Operadores

Ordem padrão de execução:

|Prioridade|Operadores|
|---|---|
|1|`()`|
|2|`**`|
|3|`*`, `/`, `//`, `%`|
|4|`+`, `-`|

Exemplo:

```python
5 + 2 * 3
```

Resultado:

```text
11
```

---

### Alterando a Prioridade

```python
(5 + 2) * 3
```

Resultado:

```text
21
```

---

## Atribuições

### Simples

```python
idade = 20
```

### Múltipla

```python
a = b = 10
```

### Sequencial

```python
x, y, z = 1, 2, 3
```

---

## Atribuições Simplificadas

```python
x += 1
x -= 1
x *= 2
x /= 2
```

Correspondem a:

```python
x = x + 1
x = x - 1
x = x * 2
x = x / 2
```

---

## None

Representa ausência de valor.

```python
valor = None
```

Exemplo:

```python
x = print("Olá")
```

Resultado:

```python
print(x)
```

```text
None
```

> [!NOTE]
> `None` não significa erro. Apenas indica que nenhum valor foi retornado.

---

## Input

Solicita entrada do usuário.

```python
nome = input("Digite seu nome: ")
```

---

### Tipo Retornado

```python
idade = input("Idade: ")

print(type(idade))
```

Resultado:

```text
<class 'str'>
```

> [!WARNING]
> `input()` sempre retorna uma string.

---

## Conversão de Tipos

### Inteiro

```python
idade = int(input("Idade: "))
```

### Decimal

```python
peso = float(input("Peso: "))
```

### Texto

```python
texto = str(100)
```

---

## Print

Exibe informações na tela.

```python
print("Olá Mundo")
```

---

### Imprimindo múltiplos valores

```python
nome = "Ana"
idade = 20

print(nome, idade)
```

Resultado:

```text
Ana 20
```

---

## Relacionados

[[Python - Variáveis e Tipos de Dados]]

[[Python - Condicionais]]