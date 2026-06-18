---
tags:
  - javascript
  - funções
  - arrow
  - callback
área: JavaScript
status: draft
---

# ← [[JavaScript]]
---

## O que são Funções?

Blocos de código reutilizáveis que realizam uma tarefa específica. Vantagens:

- **Reutilização** — chame a mesma lógica em vários lugares
- **Legibilidade** — nome da função comunica a intenção
- **Modularidade** — divide problemas grandes em partes menores
- **Escopo isolado** — variáveis internas não poluem o escopo externo

---

## Funções Regulares

Declaradas com a palavra-chave `function`. Suportam **hoisting** — podem ser chamadas antes da declaração no código.

```javascript
// Declaração
function somar(a, b) {
  return a + b;
}

// Chamada
console.log(somar(3, 5)); // 8

// Hoisting em ação
console.log(multiplicar(4, 5)); // funciona! → 20
function multiplicar(a, b) { return a * b; }

// Sem retorno explícito
function exibirMensagem(msg) {
  console.log(msg); // retorna undefined implicitamente
}
```

**Parâmetros padrão (ES6):**

```javascript
function saudar(nome = "visitante") {
  return `Olá, ${nome}!`;
}
saudar();       // "Olá, visitante!"
saudar("Ana");  // "Olá, Ana!"
```

---

## Funções Anônimas

Funções sem nome, geralmente atribuídas a variáveis ou passadas como callbacks. **Sem hoisting**.

```javascript
// Atribuída a variável
const saudacao = function(nome) {
  return `Olá, ${nome}!`;
};
console.log(saudacao("Carlos")); // "Olá, Carlos!"

// Como callback (passada como argumento)
const numeros = [1, 2, 3, 4];
const dobrados = numeros.map(function(n) {
  return n * 2;
});
// [2, 4, 6, 8]
```

> [!NOTE] Desvantagem Funções anônimas aparecem como `anonymous` em stack traces, dificultando o debug. Em produção, prefira nomeá-las ou usar arrow functions.

---

## Funções Arrow (ES6)

Sintaxe concisa e `this` léxico (herdado do contexto externo).

```javascript
// Equivalentes
const somar = (a, b) => { return a + b; };
const somar = (a, b) => a + b;          // return implícito (uma expressão)

// Um único parâmetro — parênteses opcionais
const dobrar = n => n * 2;

// Sem parâmetros — parênteses obrigatórios
const agora = () => new Date();

// Retornando objeto literal — precisa de parênteses
const criarPessoa = (nome, idade) => ({ nome, idade });
```

**Como callbacks — muito mais limpo:**

```javascript
const numeros = [1, 2, 3, 4, 5];

const pares    = numeros.filter(n => n % 2 === 0);  // [2, 4]
const dobrados = numeros.map(n => n * 2);           // [2, 4, 6, 8, 10]
const soma     = numeros.reduce((acc, n) => acc + n, 0); // 15
```

> [!NOTE] `this` nas arrow functions Arrow functions **não têm `this` próprio** — capturam o `this` do escopo onde foram definidas. Por isso, **não devem ser usadas como métodos de objetos ou construtores**.

```javascript
// Problema com função regular em callback
const objeto = {
  nome: "Objeto",
  iniciar: function() {
    setTimeout(function() {
      console.log(this.nome); // undefined — this perdido
    }, 1000);
  }
};

// Solução com arrow function
const objeto = {
  nome: "Objeto",
  iniciar: function() {
    setTimeout(() => {
      console.log(this.nome); // "Objeto" — this herdado do método
    }, 1000);
  }
};
```

---

## Comparativo

|Característica|Regular|Anônima|Arrow|
|---|---|---|---|
|Hoisting|✅|❌|❌|
|`this` próprio|✅|✅|❌ (léxico)|
|Como construtor (`new`)|✅|✅|❌|
|Sintaxe concisa|❌|❌|✅|
|Ideal para callbacks|✓|✓|✅✅|