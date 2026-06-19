---
tags: [python, oo, métodos, dunder]
área: Python
status: draft
---
# Python - Métodos e Métodos Mágicos

> [!NOTE] Fonte: _Programação Intermediária com Python — Módulos 1 e 2_ — Prof. Camila Laranjeira / UFMG / SEBRAE (Módulo 2)

## Tipos de Métodos

Todos os métodos pertencem ao namespace da classe, mas diferem no parâmetro automático que recebem:

|Tipo|Decorador|Primeiro parâmetro|Chamado por|
|---|---|---|---|
|**Instância**|(nenhum)|`self` → referência ao objeto|Apenas instâncias|
|**Classe**|`@classmethod`|`cls` → referência à classe|Classe ou instâncias|
|**Estático**|`@staticmethod`|(nenhum)|Classe ou instâncias|

```python
class Exemplo:

    contador = 0

    def __init__(self, valor):
        self.valor = valor
        Exemplo.contador += 1

    def metodo_instancia(self):         # acessa self
        return self.valor

    @classmethod
    def metodo_classe(cls):             # acessa cls
        return cls.contador

    @staticmethod
    def metodo_estatico(x, y):          # sem acesso à classe/instância
        return x + y
```

---

## Decoradores

Decoradores modificam o comportamento de funções sem alterar o código delas. Usam a sintaxe `@nome_do_decorador` acima da definição.

```python
def meu_decorador(funcao):
    def wrapper():
        print("Antes")
        funcao()
        print("Depois")
    return wrapper

@meu_decorador
def saudacao():
    print("Olá!")

saudacao()
# Antes
# Olá!
# Depois
```

---

## Métodos Mágicos (Dunder Methods)

Também chamados de **métodos especiais** ou **métodos dunder** (double underscore). Permitem customizar comportamentos nativos da linguagem para nossas classes.

> [!NOTE] Você não chama `__metodo__()` diretamente — ele é disparado indiretamente por operações da linguagem.

### Personalização Básica

|Método|Quando é chamado|
|---|---|
|`__init__(self)`|Ao instanciar um objeto|
|`__str__(self)`|Por `print()`, `str()`, `format()`|
|`__repr__(self)`|Por `repr()` — representação "oficial"|

```python
class Pocao:
    def __init__(self, nome, cura):
        self.nome = nome
        self.cura = cura

    def __str__(self):
        return f"Poção de {self.nome} (+{self.cura} HP)"

    def __repr__(self):
        return f"Pocao(nome='{self.nome}', cura={self.cura})"

p = Pocao("Vida", 50)
print(p)       # Poção de Vida (+50 HP)
repr(p)        # "Pocao(nome='Vida', cura=50)"

# Recriando objeto a partir de repr
p2 = eval(repr(p))
```

---

### Operadores Aritméticos e de Comparação

```python
class Pocao:
    def __add__(self, other):
        # self + other
        if isinstance(other, Pocao):
            return Pocao("Combinada", self.cura + other.cura)
        return Pocao(self.nome, self.cura + other)

    def __gt__(self, other):    # >
        return self.cura > other.cura

    def __lt__(self, other):    # <
        return self.cura < other.cura
```

|Operador|Método mágico|
|---|---|
|`+`|`__add__`|
|`-`|`__sub__`|
|`*`|`__mul__`|
|`>`|`__gt__`|
|`<`|`__lt__`|
|`==`|`__eq__`|
|`>=`|`__ge__`|
|`<=`|`__le__`|

---

### Protocolo de Coleção

Para que uma classe se comporte como uma coleção:

```python
class Bolsa:
    def __init__(self, capacidade):
        self.itens = []
        self.capacidade = capacidade

    def __getitem__(self, chave):     # bolsa[i]
        return self.itens[chave]

    def __setitem__(self, chave, valor):  # bolsa[i] = x
        self.itens[chave] = valor

    def __contains__(self, item):    # item in bolsa
        return item in self.itens

    def __len__(self):               # len(bolsa)
        return len(self.itens)
```

---

### Protocolo de Contexto (`with`)

```python
class Portal:
    def __enter__(self):
        print("Portal aberto!")
        return self           # valor vinculado ao `as`

    def __exit__(self, exc_type, exc_val, exc_tb):
        print("Portal fechado!")
        return False          # True suprime exceções

with Portal() as p:
    print("Dentro do portal")
# Portal aberto!
# Dentro do portal
# Portal fechado!
```

---

## Links Relacionados

- [[Python - Classes e Atributos]]
- [[Python - Pilares da OO]]
- [[Python - Herança e Polimorfismo]]