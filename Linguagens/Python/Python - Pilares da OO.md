---

tags: [python, oo, encapsulamento, herança, polimorfismo, abstração]
área: Python
status: draft
---
# Python - Pilares da OO

> [!NOTE] Fonte: _Programação Intermediária com Python — Módulos 1 e 2_ — Prof. Camila Laranjeira / UFMG / SEBRAE (Módulo 2)

## Os Quatro Pilares

|Pilar|Ideia Central|
|---|---|
|**Encapsulamento**|Controle de acesso — expor publicamente só o necessário|
|**Herança**|Criar novas classes baseadas em existentes, herdando atributos e métodos|
|**Abstração**|Ocultar detalhes de implementação; criar interfaces e contratos|
|**Polimorfismo**|Uma entidade que assume diferentes formas — interface comum para tipos distintos|

---

## Encapsulamento — Convenções de Nomenclatura

Python não possui controle de acesso real (como `private` em Java), mas usa convenções:

|Prefixo|Significado|Equivalente|
|---|---|---|
|`membro`|Público — uso livre|`public`|
|`_membro`|Protegido — não use externamente|`protected`|
|`__membro`|"Privado" — sofre _name mangling_|`private`|

### Name Mangling

Atributos com `__` têm o nome transformado automaticamente para `_NomeDaClasse__membro`, dificultando o acesso externo acidental:

```python
class Cofre:
    __senha = "1234"          # vira _Cofre__senha

cofre = Cofre()
# cofre.__senha      → AttributeError
# cofre._Cofre__senha → "1234"  (ainda possível, mas desaconselhado)
```

### `property` — Getters e Setters Pythônicos

```python
class Temperatura:
    def __init__(self, celsius):
        self._celsius = celsius

    @property
    def celsius(self):              # getter
        return self._celsius

    @celsius.setter
    def celsius(self, valor):       # setter com validação
        if valor < -273.15:
            raise ValueError("Temperatura abaixo do zero absoluto!")
        self._celsius = valor

    @celsius.deleter
    def celsius(self):              # deleter
        del self._celsius

t = Temperatura(25)
print(t.celsius)    # 25 — usa o getter
t.celsius = 100     # usa o setter
```

---

## Abstração — ABCs e Interfaces

```python
from abc import ABC, abstractmethod

class Animal(ABC):                  # Classe Base Abstrata

    @abstractmethod
    def falar(self):                # método abstrato — sem corpo
        pass

    @abstractmethod
    def mover(self):
        pass

class Cachorro(Animal):
    def falar(self):                # obrigatório sobrescrever
        return "Au!"

    def mover(self):
        return "Correndo"

# animal = Animal()   → TypeError: não pode instanciar classe abstrata
dog = Cachorro()      # OK
```

> [!TIP] Classes abstratas podem ter um ou mais métodos abstratos. **Interfaces** são classes onde **todos** os métodos são abstratos.

---

## Polimorfismo

### Sobrescrita de Métodos (Herança)

```python
class Shape:
    def area(self): return 0

class Circulo(Shape):
    def area(self): return 3.14 * self.r ** 2   # sobrescreve

class Quadrado(Shape):
    def area(self): return self.lado ** 2        # sobrescreve

# Polimorfismo em ação:
shapes = [Circulo(5), Quadrado(4)]
for s in shapes:
    print(s.area())   # chama o método correto para cada tipo
```

### Duck Typing

> _"Se parece com um pato, nada como um pato e grasna como um pato, então provavelmente é um pato."_

Python não verifica o tipo do objeto — apenas se ele possui os atributos/métodos necessários:

```python
class Pato:
    def grasnar(self): return "Quack!"

class Pessoa:
    def grasnar(self): return "Estou imitando um pato"

def fazer_grasnar(animal):
    print(animal.grasnar())    # não importa o tipo, só o método

fazer_grasnar(Pato())    # Quack!
fazer_grasnar(Pessoa())  # Estou imitando um pato
```

> [!NOTE] Duck typing não requer herança. Qualquer classe que implemente os métodos necessários pode ser usada de forma polimórfica.

---

## Expressões do Polimorfismo em Python

- Sobrescrita de métodos em herança
- Sobrecarga de operadores (métodos mágicos `__add__`, `__eq__`, etc.)
- Classes abstratas e interfaces
- Duck typing

---

## Links Relacionados

- [[Python - Classes e Atributos]]
- [[Python - Métodos e Métodos Mágicos]]
- [[Python - Herança e Polimorfismo]]
- [[Python - Tratamento de Erros]]