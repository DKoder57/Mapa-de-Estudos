---
tags: [javascript, fundamentos, variáveis, escopo]
área: JavaScript 
status: draft
---

# ← [[JavaScript]]

## O que é JavaScript?

Linguagem **interpretada**, **de alto nível** e **dinamicamente tipada**. Roda diretamente no browser sem compilação prévia. Com Node.js, também roda no servidor.

Faz parte dos três pilares da web:

- **HTML** → estrutura
- **CSS** → aparência
- **JavaScript** → lógica e interatividade

---

## Variáveis

### `var` — evitar

```javascript
var nome = "João"; // escopo de função ou global
var nome = "Maria"; // pode ser redeclarada sem erro — perigoso
```

### `let` — uso padrão

```javascript
let idade = 25;      // escopo de bloco
idade = 26;          // pode ser reatribuída
// let idade = 27;   // erro: não pode ser redeclarada no mesmo escopo
```

### `const` — preferência

```javascript
const PI = 3.14159;  // não pode ser reatribuída
// PI = 3.2;         // erro!

const obj = { x: 1 };
obj.x = 2;           // válido — o objeto em si não muda, apenas a propriedade
```

> [!TIP] Regra simples Comece com `const`. Se precisar reatribuir, troque para `let`. Nunca use `var`.

---

## Escopo

O escopo define onde uma variável pode ser acessada.

```javascript
function testeEscopo() {
  var funcaoEscopo = "visível na função inteira";

  if (true) {
    let blocoEscopo = "visível só dentro do if";
    const tambemBloco = "idem";
    console.log(funcaoEscopo); // funciona
  }

  console.log(funcaoEscopo);  // funciona
  // console.log(blocoEscopo); // ReferenceError
}
```

|Declaração|Escopo|Hoisting|Redeclarável|
|---|---|---|---|
|`var`|Função / global|Sim (como `undefined`)|Sim|
|`let`|Bloco|Não (TDZ)|Não|
|`const`|Bloco|Não (TDZ)|Não|

> [!NOTE] Hoisting `var` é movida para o topo do escopo durante a compilação, mas com valor `undefined`. `let` e `const` ficam em **Temporal Dead Zone (TDZ)** até a linha de declaração.

---

## Tipos de Dados

```javascript
// Primitivos
let texto   = "olá";          // string
let numero  = 42;             // number
let decimal = 3.14;           // number (não há float separado)
let booleano = true;          // boolean
let nulo    = null;           // null (ausência intencional de valor)
let indefinido;               // undefined (variável declarada sem valor)

// Referência
let array   = [1, 2, 3];      // Array
let objeto  = { nome: "Ana" }; // Object
let funcao  = () => {};        // Function
```

**Verificar tipo:**

```javascript
typeof "texto"   // "string"
typeof 42        // "number"
typeof true      // "boolean"
typeof undefined // "undefined"
typeof null      // "object" — quirk histórico do JS
typeof []        // "object"
typeof {}        // "object"
```

---

## Comentários

```javascript
// Comentário de linha — para notas curtas e inline

/*
  Comentário de bloco
  Use para documentar funções, classes e decisões de design
*/

/**
 * JSDoc — padrão para gerar documentação automática
 * @param {number} a - Primeiro número
 * @param {number} b - Segundo número
 * @returns {number} Soma de a e b
 */
function somar(a, b) {
  return a + b;
}
```

> [!TIP] Bons comentários Explique o **porquê**, não o **o quê**. O código já mostra o que está sendo feito; o comentário deve esclarecer a intenção ou contexto.