---

tags: [python, ciência-de-dados, numpy, arrays, vetorização]

área: Python

status: draft

---
# Python - NumPy

> [!NOTE] Fonte: _Programação Intermediária com Python — Módulos 3 e 4_ — Prof. Camila Laranjeira / UFMG / SEBRAE (Módulo 3, seção 3.2 NumPy)

## O que é NumPy?

**NumPy (Numerical Python)** é a biblioteca padrão para processamento numérico em Python. É a base do ecossistema científico — Pandas, Matplotlib, scikit-learn e outros são construídos sobre ela.

Duas características centrais:

- **Vetorial multidimensional:** coleções de elementos com 1 ≤ rank ≤ N dimensões
- **Homogêneo:** todos os elementos têm o mesmo tipo (`dtype`)

```python
import numpy as np
```

---

## Arrays e Rank

O **rank** é o número de dimensões do array:

```python
# Rank 1 — vetor
a = np.array([1, 2, 3])
print(a.ndim)    # 1
print(a.shape)   # (3,)
print(a.size)    # 3

# Rank 2 — matriz
b = np.array([[1, 2, 3],
              [4, 5, 6]])
print(b.ndim)    # 2
print(b.shape)   # (2, 3)  → 2 linhas, 3 colunas
print(b.size)    # 6

# Rank 3 — tensor
c = np.array([[[1,2,3,4],
               [5,6,7,8],
               [9,10,11,12]],
              [[13,14,15,16],
               [17,18,19,20],
               [21,22,23,24]]])
print(c.shape)   # (2, 3, 4)  → 2 blocos, 3 linhas, 4 colunas
```

### Atributos principais

|Atributo|Descrição|
|---|---|
|`ndarray.ndim`|Número de dimensões (rank)|
|`ndarray.shape`|Tupla com tamanho de cada dimensão|
|`ndarray.size`|Total de elementos|
|`ndarray.dtype`|Tipo dos elementos|

---

## Tipos de Dados (`dtype`)

```python
# Principais tipos
np.int32      # inteiro 32 bits
np.int64      # inteiro 64 bits
np.float32    # ponto flutuante 32 bits (precisão simples)
np.float64    # ponto flutuante 64 bits (padrão, precisão dupla)
np.bool_      # booleano
np.uint8      # inteiro sem sinal 8 bits (0–255)

# Especificando dtype na criação
a = np.array([1, 2, 3], dtype=np.float64)
```

---

## Criando Arrays

```python
np.zeros((3, 4))           # array 3×4 preenchido com zeros
np.ones((2, 3))            # array 2×3 preenchido com uns
np.full((2, 2), 7)         # array 2×2 preenchido com 7
np.eye(3)                  # matriz identidade 3×3
np.arange(0, 10, 2)        # [0, 2, 4, 6, 8]
np.linspace(0, 1, 5)       # [0, 0.25, 0.5, 0.75, 1.0]
np.random.random((3, 3))   # array 3×3 com valores aleatórios [0, 1)
np.random.randint(0, 10, (3, 3))  # inteiros aleatórios 0–9
```

---

## Eixos (axes)

No NumPy, dimensões são chamadas de **eixos (axes)**. O parâmetro `axis` nas funções especifica ao longo de qual eixo a operação é realizada:

```python
b = np.array([[1, 2, 3],
              [4, 5, 6]])

np.sum(b)          # 21  — soma todos os elementos
np.sum(b, axis=0)  # [5, 7, 9]  — soma ao longo das linhas (por coluna)
np.sum(b, axis=1)  # [6, 15]    — soma ao longo das colunas (por linha)
```

> [!TIP] `axis=0` opera "descendo" pelas linhas (resultado tem menos linhas). `axis=1` opera "atravessando" as colunas (resultado tem menos colunas).

---

## Indexação e Fatiamento

```python
b = np.array([[10, 20, 30, 40],
              [50, 60, 70, 80],
              [90,100,110,120]])

# Elemento específico
b[1, 2]       # 70  — linha 1, coluna 2

# Fatiamento multidimensional
b[:2, 1:3]    # primeiras 2 linhas, colunas 1 e 2
              # [[20, 30], [60, 70]]

# Indexação booleana
b[b > 50]     # [60, 70, 80, 90, 100, 110, 120]
```

> [!NOTE] Fatias são **views** — modificações na fatia afetam o array original. Use `.copy()` para criar uma cópia independente:
> 
> ```python
> fatia = b[:2, :2].copy()
> ```

---

## Operações Matemáticas (Broadcasting)

Operações são realizadas **elemento a elemento**:

```python
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

a + b       # [5, 7, 9]
a * b       # [4, 10, 18]
a ** 2      # [1, 4, 9]
np.sqrt(a)  # [1.0, 1.41, 1.73]

# Operação com escalar
a * 2       # [2, 4, 6]  — broadcasting automático
```

---

## Lendo Arquivos com NumPy

```python
dados = np.loadtxt(
    'dados.csv',
    delimiter=',',
    dtype=np.float64
)
```

---

## Resumos Estatísticos com NumPy

```python
a = np.array([1, 2, 3, 4, 5])

a.sum()          # soma
a.min()          # mínimo
a.max()          # máximo
a.mean()         # média
np.median(a)     # mediana
a.std()          # desvio padrão
a.var()          # variância

a.argmin()       # índice do mínimo
a.argmax()       # índice do máximo
np.unique(a, return_counts=True)  # valores únicos e contagens
np.cov(x, y)     # covariância
np.corrcoef(x, y)# correlação de Pearson
```

---

## Links Relacionados

- [[Python - Introdução à Ciência de Dados]]
- [[Python - Estatística com Python]]
- [[Python - Pandas]]
- [[Python - Visualização de Dados]]