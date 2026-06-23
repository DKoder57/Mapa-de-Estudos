---

tags: [matriz, python, programação]

área: Introdução à Programação / Python

status: draft

---
gi
# 🐍 Python — Matriz da Aba

> Arquivo de navegação central para todos os tópicos de Python do vault. Baseado em três apostilas do Projeto Desenvolve Itabira (Prof. Camila Laranjeira / UFMG / SEBRAE).

---

## 📚 Fontes

|Apostila|Cobertura|
|---|---|
|Programação Básica com Python|Módulos 1–8 (fundamentos completos)|
|Programação Intermediária com Python — Mód. 1 e 2|Conceitos Gerais + Orientação a Objetos|
|Programação Intermediária com Python — Mód. 3 e 4|Ciência de Dados + Web/APIs|

---

## 🟢 Seção 1 — Python Básico

> Fonte: _Programação Básica com Python_ (189p)

| #    | Nota                                                  | Tópicos                                                                             |
| ---- | ----------------------------------------------------- | ----------------------------------------------------------------------------------- |
| 1.1  | [[Python - Algoritmos e Pensamento Computacional]]    | Algoritmo, pensamento computacional, decomposição, abstração, pseudocódigo          |
| 1.2  | [[Python - Ferramentas e Ambiente (Google Colab)]]    | Google Colab, células, runtime, notebooks                                           |
| 1.3  | [[Python - Variáveis e Tipos de Dados]]               | Variáveis, int, float, str, bool, erros de tipo                                     |
| 1.4  | [[Python - Instruções, Expressões e Funções Básicas]] | Expressões, operadores, `input()`, `print()`, formatação                            |
| 1.5  | [[Python - Condicionais]]                             | Expressões relacionais, lógicas, tabela verdade, `if/elif/else`, decisões múltiplas |
| 1.6  | [[Python - Estruturas de Repetição]]                  | `while`, `for`, `range()`, `break`, `continue`                                      |
| 1.7  | [[Python - Escopo e Funções]]                         | Funções embutidas, bibliotecas, funções customizadas, escopo, `lambda`              |
| 1.8  | [[Python - Listas]]                                   | Propriedades, operações, fatiamento, list comprehension, `map()`, `filter()`        |
| 1.9  | [[Python - Strings e Arquivos]]                       | Operações de string, acesso a arquivos, arquivos de texto e binários                |
| 1.10 | [[Python - Outras Estruturas de Dados]]               | `set`, `tuple`, `dict`                                                              |

---

## 🔵 Seção 2 — Conceitos Gerais Intermediários

> Fonte: _Programação Intermediária — Módulo 1_ (Mód. 1 e 2.pdf)

| #   | Nota                                   | Tópicos                                                          |
| --- | -------------------------------------- | ---------------------------------------------------------------- |
| 2.1 | [[Python - Recursividade]]             | Auto-similaridade, caso base, passo recursivo, pilha de execução |
| 2.2 | [[Python - Ambientes Virtuais]]        | `venv`, `pip`, `requirements.txt`, isolamento de dependências    |
| 2.3 | [[Python - Modularização]]             | Módulos, pacotes, `import`, organização de projetos              |
| 2.4 | [[Python - Docstrings e Documentação]] | Docstrings, padrões (Google, NumPy), `argparse`                  |
| 2.5 | [[Python - Match-Case]]                | Sintaxe `match/case`, pattern matching, casos de uso             |

---

## 🟣 Seção 3 — Orientação a Objetos

> Fonte: _Programação Intermediária — Módulo 2_ (Mód. 1 e 2.pdf)

|#|Nota|Tópicos|
|---|---|---|
|3.1|[[Python - Classes e Atributos]]|Sintaxe de classe, `__init__`, atributos de instância e de classe|
|3.2|[[Python - Métodos e Métodos Mágicos]]|Métodos de instância, de classe, estáticos; dunder methods (`__str__`, `__add__`, etc.)|
|3.3|[[Python - Pilares da OO]]|Encapsulamento, herança, polimorfismo, abstração|
|3.4|[[Python - Herança e Polimorfismo]]|Herança simples e múltipla, `super()`, polimorfismo em prática|
|3.5|[[Python - Tratamento de Erros]]|`try/except/finally`, tipos de exceção, `raise`, erros customizados|

---

## 🟡 Seção 4 — Ciência de Dados

> Fonte: _Programação Intermediária — Módulo 3_ (Mód. 3 e 4.pdf)

|#|Nota|Tópicos|
|---|---|---|
|4.1|[[Python - Introdução à Ciência de Dados]]|Papéis na área, perfis profissionais, Python como ferramenta principal|
|4.2|[[Python - Estatística com Python]]|Módulo `statistics`, tendência central, distribuições, tipos de variáveis|
|4.3|[[Python - NumPy]]|Arrays, operações vetorizadas, tipos, indexação, broadcasting|
|4.4|[[Python - Pandas]]|DataFrame, Series, `.loc/.iloc`, leitura de arquivos, limpeza de dados|
|4.5|[[Python - Visualização de Dados]]|Matplotlib, Seaborn, Plotly — gráficos exploratórios|
|4.6|[[Python - SQL com Python]]|`sqlite3`, queries, integração com Pandas|
|4.7|[[Python - SQLAlchemy e ORM]]|SQLAlchemy Core, ORM, mapeamento objeto-relacional, CRUD|

---

## 🔴 Seção 5 — Web e APIs

> Fonte: _Programação Intermediária — Módulo 4_ (Mód. 3 e 4.pdf)

|#|Nota|Tópicos|
|---|---|---|
|5.1|[[Python - APIs REST e Consumo com Requests]]|REST, HTTP methods, status codes, `requests`, paginação, autenticação|
|5.2|[[Python - Pydantic e Validação de Dados]]|Modelos Pydantic, validação, parsing de respostas de API|
|5.3|[[Python - Flask — Fundamentos]]|Micro-framework, rotas, métodos HTTP, retorno de dados|
|5.4|[[Python - Flask — Padrões Web e CRUD]]|Flask-SQLAlchemy, modelos, relacionamentos, rotas CRUD completas|

---

## 🗺️ Mapa de Progressão Sugerido


1.1 → 1.2 → 1.3 → 1.4 → 1.5 → 1.6 → 1.7 → 1.8 → 1.9 → 1.10
                                                              ↓
                                                    2.1 → 2.2 → 2.3 → 2.4 → 2.5
                                                                              ↓
                                                              3.1 → 3.2 → 3.3 → 3.4 → 3.5
                                                                                        ↓
                                                              4.1 → 4.2 → 4.3 → 4.4 → 4.5 → 4.6 → 4.7
                                                                                                      ↓
                                                                              5.1 → 5.2 → 5.3 → 5.4


---

> [!NOTE] Padrão das notas filhas Todas as notas seguem: frontmatter YAML → conceito principal → `[!NOTE]` / `[!TIP]` → exemplos de código → links relacionados.