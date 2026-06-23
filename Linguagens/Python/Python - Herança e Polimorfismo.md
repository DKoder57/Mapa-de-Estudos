---
tags: [python, oo, herança, polimorfismo, super, MRO]
área: Python
status: draft
---
# Python - Herança e Polimorfismo

> [!NOTE] Fonte: _Programação Intermediária com Python — Módulos 1 e 2_ — Prof. Camila Laranjeira / UFMG / SEBRAE (Módulo 2)

## Herança Simples

Uma subclasse herda atributos e métodos da superclasse:

```python
class Antagonista:
    def __init__(self, nome, bordao):
        self.nome = nome
        self.bordao = bordao

    def dizer_bordao(self):
        print(f"{self.nome}: {self.bordao}")


class NazareTedesco(Antagonista):
    def __init__(self, nome, bordao, isConfusa=True):
        super().__init__(nome, bordao)    # inicializa a superclasse
        self.isConfusa = isConfusa

    def empurrar_escada(self):
        print("Empurrando...")
```

> [!NOTE] Em Python, todas as classes herdam implicitamente de `object`. A hierarquia sempre termina em `object`.

### `super()`

Retorna uma referência à superclasse, permitindo chamar seus métodos sem hardcodar o nome da classe:

```python
super().__init__(...)    # chama o __init__ da superclasse
super().metodo()         # chama qualquer método da superclasse
```

---

## Sobrescrita de Métodos

A subclasse pode redefinir (sobrescrever) métodos herdados:

```python
class Felix(Antagonista):
    def dizer_bordao(self):            # sobrescreve o método herdado
        """Versão especial do Felix"""
        print(f"{self.nome} (rei dos bordões): {self.bordao}!")
```

Após sobrescrever, o método aparece como "definido aqui" no `help()` e não mais como "herdado de".

---

## Method Resolution Order (MRO)

O MRO define a ordem em que Python busca métodos/atributos:

1. Própria classe
2. Superclasses na ordem da definição (da esquerda para a direita)
3. `object`

```python
help(NazareTedesco)
# Method Resolution Order:
#   NazareTedesco → Antagonista → object
```

---

## Herança Múltipla

Uma classe pode herdar de múltiplas superclasses:

```python
class Vehicle:
    def stop(self): print("Veículo parado")

class Car(Vehicle):
    def stop(self): print("Carro frenando")

class Aircraft(Vehicle):
    def stop(self): print("Aeronave pousando")

class FlyingCar(Car, Aircraft):    # herança múltipla
    pass
```

O MRO define qual `stop()` será chamado. A ordem dos pais na definição importa:

```python
FlyingCar.__mro__
# FlyingCar → Car → Aircraft → Vehicle → object

carro = FlyingCar()
carro.stop()    # "Carro frenando"  (Car vem antes de Aircraft)
```

> [!TIP] Inverta a ordem (`FlyingCar(Aircraft, Car)`) e o resultado muda. Pense bem na hierarquia!

---

## Polimorfismo com Herança

O polimorfismo permite tratar objetos de tipos diferentes de forma uniforme:

```python
antagonistas = [
    Antagonista("Norma", "Eu sou rica!"),
    NazareTedesco("Nazaré", "Eu não sou louca!"),
    Felix("Felix", "A vida é uma ópera")
]

for a in antagonistas:
    a.dizer_bordao()    # cada objeto chama sua própria versão
```

---

## Verificando Relações de Herança

```python
isinstance(felix, Felix)        # True
isinstance(felix, Antagonista)  # True — herança
isinstance(felix, object)       # True — toda classe herda de object

issubclass(NazareTedesco, Antagonista)  # True
issubclass(Antagonista, object)         # True
```

---

## Diagrama UML Resumido

```
Antagonista
├── nome
├── bordao
└── dizer_bordao()
    ├── NazareTedesco
    │   ├── isConfusa
    │   └── empurrar_escada()
    └── Felix
        └── dizer_bordao()  ← sobrescreve
```

---

## Links Relacionados

- [[Python - Classes e Atributos]]
- [[Python - Métodos e Métodos Mágicos]]
- [[Python - Pilares da OO]]
- [[Python - Tratamento de Erros]]