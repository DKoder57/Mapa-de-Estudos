---
tags: [python, condicionais, if, elif, else]
área: Python
status: draft
---

# ← [[Python]]

## Condicionais

Permitem executar diferentes blocos de código dependendo de uma condição.

---

## if

Executa um bloco quando a condição é verdadeira.

```python
idade = 18

if idade >= 18:
    print("Maior de idade")
```

---

## if / else

Executa um bloco se a condição for verdadeira e outro se for falsa.

```python
idade = 16

if idade >= 18:
    print("Maior")
else:
    print("Menor")
```

---

## if / elif / else

Utilizado para múltiplas decisões.

```python
nota = 75

if nota >= 90:
    print("A")
elif nota >= 70:
    print("B")
elif nota >= 50:
    print("C")
else:
    print("Reprovado")
```

---

## Operadores Relacionais

|Operador|Descrição|
|---|---|
|`==`|Igual|
|`!=`|Diferente|
|`>`|Maior|
|`<`|Menor|
|`>=`|Maior ou igual|
|`<=`|Menor ou igual|

---

## Operadores Lógicos

### and

Todas as condições devem ser verdadeiras.

```python
idade = 20
tem_carteira = True

if idade >= 18 and tem_carteira:
    print("Pode dirigir")
```

---

### or

Pelo menos uma condição deve ser verdadeira.

```python
if idade >= 60 or possui_deficiencia:
    print("Atendimento prioritário")
```

---

### not

Inverte o resultado.

```python
ativo = False

if not ativo:
    print("Usuário inativo")
```

---

## Condições Aninhadas

```python
idade = 20

if idade >= 18:
    if idade >= 60:
        print("Idoso")
    else:
        print("Adulto")
```

---

> [!TIP]
> Evite muitos níveis de indentação. Geralmente é possível simplificar a lógica.

---

## Valores Booleanos

```python
True
False
```

Resultado de comparações:

```python
10 > 5
```

```text
True
```

```python
10 == 5
```

```text
False
```

---

## Relacionados

[[Python - Instruções, Expressões e Funções Básicas]]

[[Python - Estruturas de Repetição]]