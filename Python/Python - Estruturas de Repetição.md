---
tags: [python, repeticao, loops, for, while]
área: Python
status: draft
---

# ← [[Python]]

## Estruturas de Repetição

Permitem executar um bloco de código várias vezes.

---

## while

Executa enquanto a condição for verdadeira.

```python
contador = 0

while contador < 5:
    print(contador)
    contador += 1
```

Resultado:

```text
0
1
2
3
4
```

---

> [!WARNING]
> Se a condição nunca se tornar falsa, ocorre um loop infinito.

Exemplo:

```python
while True:
    print("Loop infinito")
```

---

## for

Percorre uma sequência de valores.

```python
for numero in range(5):
    print(numero)
```

Resultado:

```text
0
1
2
3
4
```

---

## range()

Gera sequências numéricas.

### Apenas limite

```python
range(5)
```

Resultado:

```text
0 1 2 3 4
```

---

### Início e fim

```python
range(2, 6)
```

Resultado:

```text
2 3 4 5
```

---

### Passo

```python
range(0, 10, 2)
```

Resultado:

```text
0 2 4 6 8
```

---

## Iterando Listas

```python
frutas = ["Maçã", "Banana", "Laranja"]

for fruta in frutas:
    print(fruta)
```

---

## break

Interrompe imediatamente o laço.

```python
for numero in range(10):

    if numero == 5:
        break

    print(numero)
```

Resultado:

```text
0
1
2
3
4
```

---

## continue

Pula para a próxima iteração.

```python
for numero in range(5):

    if numero == 2:
        continue

    print(numero)
```

Resultado:

```text
0
1
3
4
```

---

## else em Loops

Executado apenas se o loop terminar normalmente.

```python
for numero in range(5):
    print(numero)
else:
    print("Fim do loop")
```

---

> [!NOTE]
> O bloco `else` não executa quando o loop é interrompido por `break`.

---

## Comparativo

|Estrutura|Quando usar|
|---|---|
|`for`|Quantidade conhecida de repetições|
|`while`|Condição controla a repetição|
|`break`|Interromper imediatamente|
|`continue`|Pular uma iteração|

---

## Relacionados

[[Python - Condicionais]]

[[Python - Escopo e Funções]]