---
tags: [python, ciência-de-dados, pandas, dataframe, análise-de-dados]

área: Python

status: draft

---

# Python - Pandas

> [!NOTE] Fonte: _Programação Intermediária com Python — Módulos 3 e 4_ — Prof. Camila Laranjeira / UFMG / SEBRAE (Módulo 3, seção 3.3 Pandas)

## O que é Pandas?

**Pandas** é a principal biblioteca Python para manipulação e análise de dados tabulares.

Ela fornece estruturas de dados eficientes para carregar, limpar, transformar, filtrar e analisar informações armazenadas em arquivos, bancos de dados ou APIs.

É construída sobre o NumPy e faz parte do núcleo do ecossistema de Ciência de Dados em Python.

```python
import pandas as pd
```

---

## DataFrame

A estrutura principal do Pandas é o **DataFrame**.

Pode ser entendido como uma tabela semelhante a:

- Planilhas Excel
- Arquivos CSV
- Tabelas SQL

Exemplo:

| id | nome | idade |
|----|-------|--------|
| 1 | Ana | 25 |
| 2 | João | 30 |
| 3 | Maria | 22 |

```python
df = pd.DataFrame({
    "nome": ["Ana", "João", "Maria"],
    "idade": [25, 30, 22]
})
```

---

## Componentes de um DataFrame

### Colunas

Representam os atributos (features) dos dados.

```python
df.columns
```

```python
Index(['nome', 'idade'])
```

### Índices

Identificam cada linha.

```python
df.index
```

```python
RangeIndex(start=0, stop=3, step=1)
```

Podem ser personalizados:

```python
df.index = ["A", "B", "C"]
```

---

## Lendo Arquivos CSV

O método mais utilizado do Pandas é:

```python
df = pd.read_csv("dados.csv")
```

Parâmetros importantes:

```python
pd.read_csv(
    "dados.csv",
    delimiter=",",
    header=0,
    index_col=False
)
```

|Parâmetro|Função|
|---|---|
|`delimiter`|Separador utilizado no arquivo|
|`header`|Linha que contém os nomes das colunas|
|`names`|Define manualmente os nomes das colunas|
|`index_col`|Coluna usada como índice|

---

## Informações Gerais do DataFrame

### `.info()`

Exibe resumo estrutural dos dados:

```python
df.info()
```

Resultado:

```python
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 348 entries
Data columns: 44 columns
```

Mostra:

- Quantidade de linhas
- Quantidade de colunas
- Valores nulos
- Tipos de dados
- Consumo de memória

---

## Visualização Inicial

### Primeiras linhas

```python
df.head()
```

```python
df.head(10)
```

### Últimas linhas

```python
df.tail()
```

---

## Tipos de Dados (dtype)

Cada coluna possui um tipo específico.

```python
df.dtypes
```

Tipos comuns:

|Tipo|Descrição|
|---|---|
|`int64`|Inteiros|
|`float64`|Números decimais|
|`bool`|Booleanos|
|`string`|Texto|
|`datetime64`|Datas|
|`category`|Categorias|

---

## Conversão de Tipos

### Conversão genérica

```python
df["idade"] = df["idade"].astype("int64")
```

### Datas

```python
df["data"] = pd.to_datetime(df["data"])
```

### Números

```python
df["preco"] = pd.to_numeric(df["preco"])
```

---

## Criando DataFrames

### A partir de dicionário

```python
df = pd.DataFrame({
    "nome": ["Ana", "João"],
    "idade": [25, 30]
})
```

### A partir de lista de listas

```python
dados = [
    ["Ana", 25],
    ["João", 30]
]

df = pd.DataFrame(
    dados,
    columns=["nome", "idade"]
)
```

### A partir de arrays NumPy

```python
import numpy as np

arr = np.random.randint(0, 10, (3, 2))

df = pd.DataFrame(
    arr,
    columns=["A", "B"]
)
```

---

## Seleção de Dados

### Selecionar coluna

```python
df["idade"]
```

ou

```python
df.idade
```

---

### Múltiplas colunas

```python
df[["nome", "idade"]]
```

---

### Selecionar linha por índice

```python
df.loc[0]
```

---

### Selecionar por posição

```python
df.iloc[0]
```

---

## Filtragem

```python
df[df["idade"] > 25]
```

```python
df[df["cidade"] == "São Paulo"]
```

Filtros compostos:

```python
df[
    (df["idade"] > 20)
    & (df["idade"] < 40)
]
```

---

## Estatísticas Básicas

```python
df.describe()
```

Retorna:

- Média
- Desvio padrão
- Mínimo
- Máximo
- Quartis

---

## Valores Nulos

Verificar:

```python
df.isnull()
```

Contagem:

```python
df.isnull().sum()
```

Remover:

```python
df.dropna()
```

Preencher:

```python
df.fillna(0)
```

---

## Ordenação

```python
df.sort_values("idade")
```

Decrescente:

```python
df.sort_values(
    "idade",
    ascending=False
)
```

---

## Agrupamentos

Equivalente ao `GROUP BY` do SQL.

```python
df.groupby("cidade")["salario"].mean()
```

Exemplo:

```python
df.groupby("cargo")["salario"].max()
```

---

## Exportação

CSV:

```python
df.to_csv("resultado.csv")
```

Excel:

```python
df.to_excel("resultado.xlsx")
```

---

## Fluxo Comum de Trabalho

```text
CSV/Excel/SQL
        ↓
   pd.read_*
        ↓
 Limpeza dos Dados
        ↓
 Transformações
        ↓
 Análise Exploratória
        ↓
 Visualização
        ↓
 Exportação
```

---

## Resumo dos Métodos Mais Importantes

```python
pd.read_csv()

df.head()
df.tail()
df.info()
df.describe()

df.columns
df.dtypes

df.loc[]
df.iloc[]

df.groupby()
df.sort_values()

df.isnull()
df.fillna()
df.dropna()

df.to_csv()
df.to_excel()
```

---

## Links Relacionados

- [[Python - Introdução à Ciência de Dados]]
- [[Python - Estatística com Python]]
- [[Python - NumPy]]
- [[Python - Visualização de Dados]]
- [[Python - SQL com Python]]