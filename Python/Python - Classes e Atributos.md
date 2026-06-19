---
tags: [python, oo, classes]
área: Python
status: draft
---
# Python - Classes e Atributos

> [!NOTE] Fonte: _Programação Intermediária com Python — Módulos 1 e 2_ — Prof. Camila Laranjeira / UFMG / SEBRAE (Módulo 2)

## O que é uma Classe?

A **classe** define um novo tipo de dado, estabelecendo atributos e métodos que serão instanciados em futuros objetos. Funciona como um molde ou planta-baixa.

Uma **instância** é o objeto concreto criado a partir da classe. Cada instância é independente, com sua própria identidade e seus próprios valores.

---

## Sintaxe Básica

```python
class NomeDaClasse:

    # CONSTRUTOR: executado ao instanciar o objeto
    def __init__(self, param1, param2):
        # Atributos de instância (prefixados com self)
        self.param1 = param1
        self.param2 = param2

    # Métodos customizados
    def metodo(self):
        return self.param1
```

O primeiro argumento da maioria dos métodos é `self` — uma referência ao objeto atual, necessária para acessar atributos e métodos dentro da classe.

---

## Tipos de Atributos

|Tipo|Definição|Escopo|
|---|---|---|
|**Atributo de instância**|Dentro de `__init__`, prefixado com `self`|Cada objeto tem sua própria cópia|
|**Atributo de classe**|Na raiz da classe, sem `self`|Compartilhado por todos os objetos da classe|

```python
class Personagem:
    especie = "humano"          # atributo de classe

    def __init__(self, nome, nivel):
        self.nome = nome        # atributo de instância
        self.nivel = nivel      # atributo de instância
```

> [!TIP] Atributos de classe passam a existir no momento da definição e são acessíveis diretamente pela classe, sem precisar de instância.

---

## Instanciando e Acessando Membros

```python
# Criando instâncias
p1 = Personagem("Aragorn", 20)
p2 = Personagem("Legolas", 18)

# Acessando atributos (notação de ponto)
print(p1.nome)      # "Aragorn"
print(p1.nivel)     # 20

# Chamando métodos
p1.metodo()

# Atributo de classe via instância ou via classe
print(p1.especie)          # "humano"
print(Personagem.especie)  # "humano"
```

---

## Comportamento de Atributos de Classe ao Modificar

- Modificado **pela classe** → afeta todas as instâncias (exceto as que já sobrescreveram)
- Modificado **por uma instância** → afeta apenas aquela instância

```python
Personagem.especie = "elfo"   # muda para todos
p1.especie = "anão"           # muda só para p1
```

---

## Python Data Model — Tudo é Objeto

No Python, todo elemento da linguagem é um objeto com três propriedades:

|Propriedade|Descrição|Imutável?|
|---|---|---|
|**Identidade**|Endereço na memória (`id(obj)`)|Sim|
|**Tipo**|A classe do objeto (`type(obj)`)|Sim|
|**Valor**|O conteúdo do objeto|Depende (mutável vs imutável)|

```python
x = [1, 2, 3]
y = x          # y aponta para o MESMO objeto
y.append(4)    # altera o objeto original
print(x)       # [1, 2, 3, 4]

y = y + [5]    # cria um NOVO objeto
print(x)       # [1, 2, 3, 4]  — x não foi alterado
```

> [!NOTE] Atribuição em Python não copia objetos — cria ligações entre nome e objeto. Use `.copy()` quando precisar de uma cópia independente.

---

## Links Relacionados

- [[Python - Métodos e Métodos Mágicos]]
- [[Python - Pilares da OO]]
- [[Python - Herança e Polimorfismo]]
- [[Python - Encapsulamento]]