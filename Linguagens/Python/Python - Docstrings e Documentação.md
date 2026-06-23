---

tags: [python, docstrings, documentação, argparse, cli]
área: Python / Conceitos Gerais
status: draft

---
# 📝 Python - Docstrings e Documentação

> Fonte: _Programação Intermediária com Python — Módulo 1_ (Prof. Camila Laranjeira / UFMG / SEBRAE)

---

## O que são docstrings?

**Docstrings** são strings literais posicionadas como **primeira instrução** de um módulo, classe, método ou função. São armazenadas no atributo `__doc__` do elemento e permitem a geração automática de documentações.

> [!NOTE] Comentário vs. Docstring Comentários (`#`) são ignorados pelo interpretador e não ficam acessíveis em tempo de execução. Docstrings ficam disponíveis via `__doc__` e `help()`.

---

## Consultando documentações existentes

```python
import math

# via atributo __doc__
print(math.__doc__)
print(math.comb.__doc__)

# via função help() — abre sessão interativa no terminal
help(math.comb)
```

Para exportar como HTML:

```bash
python -m pydoc -w ./meu_modulo.py
# gera meu_modulo.html
```

---

## Criando docstrings

### Docstring de uma linha

Para elementos simples e autoexplicativos:

```python
def verificar_tipo(tipo):
    """Verifica se um tipo de Pokémon é válido."""
    return tipo in TIPOS
```

### Docstring de múltiplas linhas

Primeira linha: descrição resumida. Linha em branco. Depois: detalhamento.

```python
def comb(n, k):
    """Número de formas de escolher k itens de n sem repetição.

    Avalia n! / (k! * (n - k)!) quando k <= n,
    e zero quando k > n.

    Parâmetros:
        n (int): Total de itens disponíveis.
        k (int): Itens a escolher.

    Retorna:
        int: O coeficiente binomial.

    Lança:
        TypeError: Se os argumentos não forem inteiros.
        ValueError: Se os argumentos forem negativos.
    """
    pass
```

---

## O que documentar em cada elemento

|Elemento|O que incluir|
|---|---|
|**Módulo**|Visão geral do propósito e funcionalidade|
|**Classe**|Objetivo, atributos principais, métodos públicos|
|**Método**|O que faz, parâmetros (tipo e expectativas), retorno, exceções|
|**Função**|Igual ao método, mas fora de classes|

---

## Padrões de formato

Os dois formatos mais comuns no ecossistema Python:

**Google style:**

```python
def soma(a, b):
    """Soma dois números.

    Args:
        a (int): Primeiro número.
        b (int): Segundo número.

    Returns:
        int: Resultado da soma.
    """
    return a + b
```

**NumPy style:**

```python
def soma(a, b):
    """Soma dois números.

    Parameters
    ----------
    a : int
        Primeiro número.
    b : int
        Segundo número.

    Returns
    -------
    int
        Resultado da soma.
    """
    return a + b
```

> [!TIP] Escolha um padrão e seja consistente Ferramentas como Sphinx, MkDocs e PyDoc conseguem gerar documentação HTML automaticamente a partir de qualquer um dos formatos acima.

---

## `argparse` — Interface de linha de comando (CLI)

O módulo `argparse` cria interfaces textuais para aplicações Python, com suporte a argumentos posicionais, opções e subcomandos — além de gerar `--help` automaticamente.

### Elementos de uma CLI

|Elemento|Descrição|Exemplo|
|---|---|---|
|**Comando**|O programa executado|`pip`|
|**Subcomando**|Ação específica do programa|`pip install`|
|**Argumento posicional**|Entrada obrigatória, definida pela posição|`pip install pandas`|
|**Opção / flag**|Modifica comportamento, nomeada com `-` ou `--`|`ls -l`|
|**Parâmetro de opção**|Valor associado a uma opção|`pip install -r requirements.txt`|

### Uso básico

```python
import argparse

parser = argparse.ArgumentParser()

# argumento posicional obrigatório
parser.add_argument('filename')

# opção com parâmetro inteiro e valor padrão
parser.add_argument('-r', '--row', type=int, default=0)

# opção interruptora (True/False)
parser.add_argument('-i', '--inverted', action='store_true')

args = parser.parse_args()

# acesso aos valores
print(args.filename)
print(args.row)
print(args.inverted)
```

```bash
python script.py arquivo.txt -r 10 --inverted
# Namespace(filename='arquivo.txt', row=10, inverted=True)

python script.py --help
# Usage: script.py [-h] [-r ROW] [-i] filename
# ...
```

---

## Links relacionados

- [[Python - Modularização]]
- [[Python - Ambientes Virtuais]]
- [[Python - Escopo e Funções]]