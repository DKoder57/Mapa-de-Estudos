---

tags: [python, match-case, pattern-matching, controle-de-fluxo]
área: Python / Conceitos Gerais
status: draft
---
# 🎯 Python - Match-Case

> Fonte: _Programação Intermediária com Python — Módulo 1_ (Prof. Camila Laranjeira / UFMG / SEBRAE)

---

## O que é?

Introduzido no **Python 3.10**, o `match/case` implementa o **structural pattern matching** (casamento de padrões estruturais). É mais poderoso que um simples `switch/case` de outras linguagens: além de comparar valores, valida a _estrutura_ do dado.

> [!NOTE] Requisito de versão `match/case` requer Python 3.10 ou superior. Use `python --version` para verificar.

---

## Sintaxe básica

```python
match opcao:
    case 1:
        print("Um")
    case 2:
        print("Dois")
    case outro:        # captura qualquer valor restante (equivale ao else)
        print(f"Outro valor: {outro}")
```

> [!NOTE] Variáveis nos cases capturam — não comparam Escrever `case x:` não compara com uma variável `x` existente — cria uma **nova variável** que captura o valor. Para comparar com uma variável externa, use notação de ponto: `case Namespace.valor`.

---

## Padrões suportados

|Padrão|Sintaxe|Descrição|
|---|---|---|
|Valor literal|`case "a":`|Compara com o valor exato|
|Coleção exata|`case ["a", "b"]:`|Lista com exatamente esses dois elementos|
|Coleção com captura|`case ["a", valor]:`|Lista de 2 elementos; o 2º é capturado|
|Captura múltipla|`case ["a", *resto]:`|Pelo menos 1 elemento; os demais vão para `resto`|
|Alternativas (or)|`case "a" \| "b":`|Corresponde a qualquer das alternativas|
|Curinga|`case _:`|Corresponde a qualquer valor, sem capturá-lo|

---

## Exemplo: jogo de aventura em texto

```python
comando = input("Ação: ").split()

match comando:
    case ["sair"]:
        print("Saindo do jogo.")

    case ["usar", item]:
        print(f"Usando {item}.")

    case ["atacar", inimigo, arma]:
        print(f"Atacando {inimigo} com {arma}.")

    case _:
        print("Comando inválido.")
```

Cada `case` valida simultaneamente a **quantidade de palavras** e os **valores específicos**.

---

## Guardas condicionais (`if`)

É possível adicionar uma condição extra após o padrão:

```python
match ponto:
    case (x, y) if x == y:
        print("Diagonal")
    case (x, y):
        print(f"Ponto: ({x}, {y})")
```

---

## Match-case vs. if-elif

||`if-elif`|`match-case`|
|---|---|---|
|Compara valores simples|✅|✅|
|Valida estrutura de coleções|❌|✅|
|Captura partes do valor|❌|✅|
|Legibilidade para muitos casos|Regular|Melhor|

> [!TIP] Use match-case quando o dado tem estrutura variável Para menus simples, `if-elif` é suficiente. Para processar comandos, mensagens ou estruturas de dados com formatos distintos, `match-case` é mais expressivo e seguro.

---

## Links relacionados

- [[Python - Condicionais]]
- [[Python - Outras Estruturas de Dados]]
- [[Python - Docstrings e Documentação]]