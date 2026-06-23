---
tags: [python, funcoes, escopo, return]
área: Python
status: draft
---

# ← [[Python]]

## Funções

Funções são blocos reutilizáveis de código que executam uma tarefa específica.

Benefícios:

- Evitam repetição de código
- Facilitam manutenção
- Melhoram organização
- Tornam programas mais legíveis

---

## Definindo uma Função

```python
def saudacao():
    print("Olá!")
```

A função só será executada quando chamada.

```python
saudacao()
```

Resultado:

```text
Olá!
```

---

## Parâmetros

Permitem enviar informações para a função.

```python
def saudacao(nome):
    print(f"Olá, {nome}")
```

Uso:

```python
saudacao("Ana")
```

Resultado:

```text
Olá, Ana
```

---

## Múltiplos Parâmetros

```python
def soma(a, b):
    print(a + b)
```

```python
soma(10, 20)
```

Resultado:

```text
30
```

---

## Return

Retorna um valor para quem chamou a função.

```python
def soma(a, b):
    return a + b
```

```python
resultado = soma(10, 20)

print(resultado)
```

Resultado:

```text
30
```

---

> [!NOTE]
> Sem `return`, a função retorna automaticamente `None`.

Exemplo:

```python
def teste():
    print("Olá")
```

```python
print(teste())
```

Resultado:

```text
Olá
None
```

---

## Funções com Valor Padrão

```python
def saudacao(nome="Visitante"):
    print(f"Olá, {nome}")
```

```python
saudacao()
```

Resultado:

```text
Olá, Visitante
```

---

## Escopo

Define onde uma variável pode ser acessada.

---

## Escopo Local

Criado dentro da função.

```python
def exemplo():
    mensagem = "Olá"
    print(mensagem)
```

A variável existe apenas dentro da função.

---

## Escopo Global

Criado fora das funções.

```python
nome = "Ana"

def mostrar():
    print(nome)
```

---

## Variáveis Locais x Globais

```python
x = 10

def teste():
    x = 20
    print(x)

teste()

print(x)
```

Resultado:

```text
20
10
```

---

> [!WARNING]
> Evite depender excessivamente de variáveis globais. Elas dificultam manutenção e testes.

---

## Lambda

Funções anônimas e simples.

```python
dobro = lambda x: x * 2

print(dobro(5))
```

Resultado:

```text
10
```

---

## Boas Práticas

✅ Funções pequenas

✅ Um único objetivo

✅ Nomes descritivos

```python
def calcular_media():
```

❌

```python
def calc():
```

---

## Relacionados

[[Python - Estruturas de Repetição]]

[[Python - Listas]]