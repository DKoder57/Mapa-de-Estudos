---
tags: [python, listas, arrays]
área: Python
status: draft
---

# ← [[Python]]

## Listas

Listas armazenam múltiplos valores em uma única variável.

Características:

- Ordenadas
- Mutáveis
- Permitem valores repetidos

```python
frutas = ["Maçã", "Banana", "Laranja"]
```

---

## Índices

Cada elemento possui uma posição.

```python
frutas = ["Maçã", "Banana", "Laranja"]
```

|Índice|Valor|
|---|---|
|0|Maçã|
|1|Banana|
|2|Laranja|

---

## Acessando Elementos

```python
print(frutas[0])
```

Resultado:

```text
Maçã
```

---

## Índices Negativos

```python
print(frutas[-1])
```

Resultado:

```text
Laranja
```

---

## Alterando Valores

```python
frutas[1] = "Uva"
```

Resultado:

```python
["Maçã", "Uva", "Laranja"]
```

---

## Adicionando Elementos

### append()

```python
frutas.append("Manga")
```

---

### insert()

```python
frutas.insert(1, "Abacaxi")
```

---

## Removendo Elementos

### remove()

```python
frutas.remove("Banana")
```

---

### pop()

```python
frutas.pop()
```

Remove o último elemento.

---

## Tamanho da Lista

```python
len(frutas)
```

---

## Percorrendo Listas

```python
for fruta in frutas:
    print(fruta)
```

---

## Fatiamento

### Intervalo

```python
frutas[1:3]
```

Resultado:

```python
["Banana", "Laranja"]
```

---

### Início até posição

```python
frutas[:2]
```

---

### Posição até final

```python
frutas[2:]
```

---

## List Comprehension

Forma compacta de criar listas.

```python
quadrados = [x**2 for x in range(5)]
```

Resultado:

```python
[0, 1, 4, 9, 16]
```

---

> [!TIP]
> List Comprehension costuma ser mais legível e performática do que criar listas com `append()` dentro de loops simples.

---

## Métodos Comuns

|Método|Função|
|---|---|
|append()|Adicionar elemento|
|insert()|Inserir em posição|
|remove()|Remover valor|
|pop()|Remover por índice|
|sort()|Ordenar|
|reverse()|Inverter|
|clear()|Limpar lista|

---

## Relacionados

[[Python - Escopo e Funções]]

[[Python - Strings e Arquivos]]

[[Python - Outras Estruturas de Dados]]