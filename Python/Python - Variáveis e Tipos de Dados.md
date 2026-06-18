---
tags: [python, variaveis, tipos-dados]
área: Python
status: draft
---

# ← [[Python]]

## Variáveis

Variáveis armazenam referências para valores.

```python
idade = 20
nome = "Danilo"
```

---

## Operador de Atribuição

```python
=
```

Exemplos:

```python
x = 10

y = 5 + 3

z = x * y
```

---

## Tipagem Dinâmica

Python define o tipo automaticamente.

```python
x = 10

print(type(x))
```

Resultado:

```text
<class 'int'>
```

Alterando o valor:

```python
x = "Olá"
```

Agora:

```text
<class 'str'>
```

> [!NOTE]
> Uma variável pode mudar de tipo durante a execução.

---

## Tipos Básicos

### int

Números inteiros.

```python
idade = 25
saldo = -100
```

---

### float

Números decimais.

```python
pi = 3.14

peso = 72.5
```

---

### str

Textos.

```python
nome = "Maria"

mensagem = 'Olá'
```

---

## Verificando Tipos

```python
type(valor)
```

Exemplo:

```python
print(type(3.14))
```

Resultado:

```text
<class 'float'>
```

---

## Conversão de Tipos

### Para inteiro

```python
int("10")
```

### Para decimal

```python
float("10.5")
```

### Para texto

```python
str(100)
```

---

## Boas Práticas

### Bons nomes

```python
raio = 10

diametro = raio * 2

salario_mensal = 5000
```

### Nomes ruins

```python
x = 10

abc = 20

teste123 = 30
```

---

## Regras para Nomes

Pode:

```python
nome

idade2

_velocidade
```

Não pode:

```python
2idade

valor-total

for
```

---

## Erros Comuns

### SyntaxError

```python
2 = x
```

---

### TypeError

```python
idade = "20"

print(2025 - idade)
```

---

### IndentationError

```python
x = 10
 print(x)
```

---

> [!TIP]
> Se receber um TypeError, verifique primeiro os tipos usando `type()`.

---

## Literais

Valores escritos diretamente no código.

```python
10

3.14

"Olá"
```

Exemplo:

```python
idade = 20
```

- `idade` → variável
- `20` → literal

---

## Relacionados

[[Python - Ferramentas e Ambiente (Google Colab)]]

[[Python - Instruções, Expressões e Funções Básicas]]