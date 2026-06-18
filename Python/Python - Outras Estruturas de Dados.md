---
tags: [python, tuplas, conjuntos, dicionarios]
área: Python
status: draft
---

# ← [[Python]]

## Tuplas (tuple)

Coleções ordenadas e imutáveis.

```python
cores = ("Azul", "Verde", "Vermelho")
```

---

## Acessando Elementos

```python
print(cores[0])
```

Resultado:

```text
Azul
```

---

> [!NOTE]
> Após criada, uma tupla não pode ser modificada.

---

## Sets (Conjuntos)

Coleções não ordenadas e sem elementos duplicados.

```python
numeros = {1, 2, 3, 3, 3}
```

Resultado:

```python
{1, 2, 3}
```

---

## Adicionando Elementos

```python
numeros.add(4)
```

---

## Removendo Elementos

```python
numeros.remove(2)
```

---

## Operações de Conjunto

### União

```python
a = {1, 2}
b = {2, 3}

a.union(b)
```

Resultado:

```python
{1, 2, 3}
```

---

### Interseção

```python
a.intersection(b)
```

Resultado:

```python
{2}
```

---

## Dicionários (dict)

Estruturas baseadas em chave → valor.

```python
pessoa = {
    "nome": "Ana",
    "idade": 25
}
```

---

## Acessando Valores

```python
print(pessoa["nome"])
```

Resultado:

```text
Ana
```

---

## Alterando Valores

```python
pessoa["idade"] = 26
```

---

## Adicionando Novas Chaves

```python
pessoa["cidade"] = "São Paulo"
```

---

## Métodos Comuns

### keys()

```python
pessoa.keys()
```

---

### values()

```python
pessoa.values()
```

---

### items()

```python
pessoa.items()
```

---

### get()

```python
pessoa.get("nome")
```

---

> [!TIP]
> Prefira `get()` quando a chave pode não existir. Evita erros de acesso.

---

## Comparativo

|Estrutura|Ordenada|Mutável|Duplicados|
|---|---|---|---|
|Lista|✅|✅|✅|
|Tupla|✅|❌|✅|
|Set|❌|✅|❌|
|Dicionário|✅*|✅|Chaves únicas|

\* A partir do Python 3.7 mantém ordem de inserção.

---

## Quando Utilizar

|Estrutura|Uso Ideal|
|---|---|
|Lista|Sequências gerais|
|Tupla|Dados fixos|
|Set|Eliminar duplicados|
|Dicionário|Relacionamento chave → valor|

---

## Relacionados

[[Python - Listas]]

[[Python - Strings e Arquivos]]