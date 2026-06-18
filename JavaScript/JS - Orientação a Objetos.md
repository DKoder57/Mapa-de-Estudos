---

tags: [javascript, poo, classes, herança, encapsulamento, polimorfismo]
área: JavaScript

status: draft

---



# ← [[JavaScript]]


## Os 4 Pilares da POO

|Pilar|Definição|
|---|---|
|**Abstração**|Modelar apenas os atributos e comportamentos essenciais|
|**Encapsulamento**|Proteger dados internos, expondo só o necessário|
|**Herança**|Classe filha reutiliza e estende a classe pai|
|**Polimorfismo**|Mesmo método, comportamentos distintos por classe|

---

## Classes e Objetos

Uma **classe** é o molde. Um **objeto** é uma instância concreta da classe.

```javascript
class Animal {
  constructor(nome, especie) {
    this.nome = nome;
    this.especie = especie;
  }

  descrever() {
    return `${this.nome} é um(a) ${this.especie}.`;
  }
}

// Criando instâncias
const gato = new Animal("Mochi", "felino");
const cao  = new Animal("Rex", "canino");

console.log(gato.descrever()); // "Mochi é um(a) felino."
console.log(cao.nome);         // "Rex"
```

---

## Herança (`extends` / `super`)

A classe filha herda todos os métodos e propriedades da pai, podendo sobrescrevê-los ou adicionar novos.

```javascript
class Veiculo {
  constructor(marca, velocidade) {
    this.marca = marca;
    this.velocidade = velocidade;
  }

  mover() {
    return `${this.marca} se move a ${this.velocidade} km/h.`;
  }
}

class Carro extends Veiculo {
  constructor(marca, velocidade, portas) {
    super(marca, velocidade); // chama o constructor do pai
    this.portas = portas;
  }

  descrever() {
    return `${this.marca} com ${this.portas} portas.`;
  }
}

const carro = new Carro("Toyota", 120, 4);
console.log(carro.mover());    // herdado de Veiculo
console.log(carro.descrever()); // próprio de Carro
```

---

## Encapsulamento

Controlar o acesso a dados internos do objeto.

**Convenção (underscore)** — não é realmente privado:

```javascript
class Pessoa {
  constructor(nome) {
    this._nome = nome; // convenção: "privado", mas acessível
  }
  getNome() { return this._nome; }
}
```

**Campos privados reais (ES2022 — `#`):**

```javascript
class ContaBancaria {
  #saldo;

  constructor(saldoInicial) {
    this.#saldo = saldoInicial;
  }

  depositar(valor) {
    if (valor <= 0) throw new Error("Valor inválido");
    this.#saldo += valor;
  }

  sacar(valor) {
    if (valor > this.#saldo) throw new Error("Saldo insuficiente");
    this.#saldo -= valor;
  }

  get saldo() { return this.#saldo; } // getter
}

const conta = new ContaBancaria(1000);
conta.depositar(500);
console.log(conta.saldo); // 1500
// conta.#saldo           // SyntaxError — inacessível externamente
```

---

## Abstração

Focar no essencial, ignorando detalhes irrelevantes para o contexto.

```javascript
class Imovel {
  constructor(endereco, tamanho) {
    this.endereco = endereco;
    this.tamanho = tamanho;
  }

  descrever() {
    return `Imóvel em ${this.endereco} — ${this.tamanho}m²`;
  }

  validar() {
    if (!this.endereco || this.tamanho <= 0) {
      throw new Error("Dados inválidos");
    }
  }
}
```

---

## Polimorfismo

Mesmo método, comportamentos distintos. Classes filhas sobrescrevem métodos do pai.

```javascript
class Casa extends Imovel {
  constructor(endereco, tamanho, quartos) {
    super(endereco, tamanho);
    this.quartos = quartos;
  }

  descrever() { // sobrescreve o método pai
    return `Casa de ${this.quartos} quartos em ${this.endereco}.`;
  }
}

class Apartamento extends Imovel {
  constructor(endereco, tamanho, andar) {
    super(endereco, tamanho);
    this.andar = andar;
  }

  descrever() { // comportamento diferente, mesmo nome
    return `Apartamento no ${this.andar}º andar em ${this.endereco}.`;
  }
}

const imoveis = [
  new Casa("Rua A, 10", 150, 3),
  new Apartamento("Av. B, 500", 80, 12)
];

// Polimorfismo: mesmo método, resultados diferentes
imoveis.forEach(i => console.log(i.descrever()));
```

---

## Getters e Setters

```javascript
class Temperatura {
  #celsius;

  constructor(celsius) { this.#celsius = celsius; }

  get fahrenheit() { return this.#celsius * 9/5 + 32; }
  set celsius(valor) {
    if (valor < -273.15) throw new Error("Abaixo do zero absoluto");
    this.#celsius = valor;
  }
  get celsius() { return this.#celsius; }
}

const t = new Temperatura(100);
console.log(t.fahrenheit); // 212
t.celsius = 0;
console.log(t.fahrenheit); // 32
```

---

## Métodos Estáticos

Pertencem à classe, não às instâncias. Chamados diretamente na classe.

```javascript
class MathUtils {
  static somar(a, b) { return a + b; }
  static PI = 3.14159;
}

MathUtils.somar(3, 4); // 7 — sem precisar de `new`
MathUtils.PI;          // 3.14159
```