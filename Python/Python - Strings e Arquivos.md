---
tags: [python, strings, arquivos]
área: Python
status: draft
---

# ← [[Python]]

## Strings

Strings representam sequências de caracteres.

```python
nome = "Python"
```

---

## Criando Strings

```python
texto = "Olá"

texto = 'Olá'
```

Ambas são válidas.

---

## Concatenação

```python
nome = "Python"

print("Olá " + nome)
```

Resultado:

```text
Olá Python
```

---

## Repetição

```python
print("=" * 10)
```

Resultado:

```text
==========
```

---

## Comprimento

```python
len("Python")
```

Resultado:

```text
6
```

---

## Métodos Comuns

### upper()

```python
"python".upper()
```

Resultado:

```text
PYTHON
```

---

### lower()

```python
"PYTHON".lower()
```

Resultado:

```text
python
```

---

### strip()

Remove espaços.

```python
"  Olá  ".strip()
```

---

### replace()

```python
"Olá".replace("Olá", "Oi")
```

---

### split()

```python
"Python Java C".split()
```

Resultado:

```python
['Python', 'Java', 'C']
```

---

## Percorrendo Strings

```python
for letra in "Python":
    print(letra)
```

---

## Arquivos

Permitem armazenar dados permanentemente.

---

## Abrindo Arquivos

```python
arquivo = open("dados.txt")
```

---

## Modos de Abertura

|Modo|Descrição|
|---|---|
|r|Leitura|
|w|Escrita|
|a|Adicionar conteúdo|
|x|Criar arquivo|

---

## Leitura

```python
arquivo = open("dados.txt", "r")

conteudo = arquivo.read()

print(conteudo)
```

---

## Escrita

```python
arquivo = open("dados.txt", "w")

arquivo.write("Olá Mundo")
```

---

## Fechando Arquivos

```python
arquivo.close()
```

---

> [!WARNING]
> Sempre feche arquivos após utilizá-los para evitar desperdício de recursos.

---

## Context Manager

Forma moderna e segura.

```python
with open("dados.txt", "r") as arquivo:
    conteudo = arquivo.read()
```

> [!TIP]
> O `with` fecha o arquivo automaticamente, mesmo em caso de erro.

---

## Relacionados

[[Python - Listas]]

[[Python - Outras Estruturas de Dados]]