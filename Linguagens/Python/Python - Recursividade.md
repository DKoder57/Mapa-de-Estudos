---
tags: [python, recursividade, algoritmos]

área: Python / Conceitos Gerais

status: draft

---
# 🔁 Python - Recursividade

> Fonte: _Programação Intermediária com Python — Módulo 1_ (Prof. Camila Laranjeira / UFMG / SEBRAE)

---

## O que é recursividade?

Recursividade é a capacidade de uma função **chamar a si mesma**. O conceito está ligado à ideia de **auto-similaridade**: um elemento que contém cópias menores de si mesmo — como fractais na natureza (flocos de neve, rios, sinapses).

Na matemática, exemplos clássicos são:

- **Fatorial**: `n! = n * (n-1)!`, com caso base `0! = 1`
- **Somatório**: `Σ(n) = n + Σ(n-1)`, com caso base `Σ(0) = 0`

---

## Estrutura de uma função recursiva

Toda função recursiva tem dois elementos obrigatórios:

|Elemento|Descrição|
|---|---|
|**Caso base**|Forma mais simples do problema, com resposta direta. É a condição de parada.|
|**Passo recursivo**|Chama a própria função com um estado menor, convergindo para o caso base.|

```python
def fatorial(n):
    if n == 0:       # caso base
        return 1
    return n * fatorial(n - 1)   # passo recursivo
```

> [!NOTE] Convergência obrigatória O passo recursivo deve sempre avançar em direção ao caso base. Sem isso, ocorre recursão infinita e estouro de pilha (`RecursionError`).

---

## Pilha de execução

Cada chamada recursiva é empilhada na memória até atingir o caso base. Depois, o resultado é devolvido camada por camada:

```
fatorial(4)
  └─ 4 * fatorial(3)
         └─ 3 * fatorial(2)
                └─ 2 * fatorial(1)
                       └─ 1 * fatorial(0) → 1
```

O retorno sobe: `1 → 1 → 2 → 6 → 24`

> [!TIP] Visualize com `print` Inserir prints antes e depois da chamada recursiva ajuda a rastrear o fluxo de execução e entender a ordem de empilhamento e desempilhamento.

---

## Exemplo: intervalo recursivo

```python
def intervalo(a, b):
    if a > b:
        print("Erro: a deve ser menor ou igual a b")
        return
    print(a)
    intervalo(a + 1, b)   # passo recursivo, avança até a == b (caso base implícito)
```

---

## Quando usar recursividade?

Recursividade é especialmente natural para problemas com estrutura hierárquica ou auto-similar:

- Travessia de árvores (pré-ordem, pós-ordem)
- Algoritmos de divisão e conquista (merge sort, busca binária)
- Geração de fractais
- Árvores de ancestralidade

> [!NOTE] Recursão vs. Iteração Qualquer solução recursiva pode ser reescrita com laços (`while`/`for`). A escolha depende de legibilidade e contexto. Soluções iterativas geralmente são mais eficientes em memória; recursivas, mais legíveis para problemas hierárquicos.

---

## Links relacionados

- [[Python - Escopo e Funções]]
- [[Python - Estruturas de Repetição]]