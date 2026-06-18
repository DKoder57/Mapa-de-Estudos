---
tags: [javascript, arrays, métodos, iteração]

área: JavaScript

status: draft
---

# ← [[JavaScript]]


## Criação e Acesso

```javascript
// Criação
let numeros = [1, 2, 3, 4, 5];
let misto   = [42, "texto", true, [1, 2]]; // aceita tipos mistos
let vazio   = [];

// Acesso por índice (base 0)
numeros[0]  // 1
numeros[4]  // 5
numeros[numeros.length - 1]  // último elemento → 5

// Modificação
numeros[2] = 99;  // [1, 2, 99, 4, 5]
```

---

## Métodos Básicos — Adicionar / Remover

```javascript
let arr = [1, 2, 3];

arr.push(4);       // Adiciona no final     → [1, 2, 3, 4]
arr.pop();         // Remove do final       → [1, 2, 3]
arr.unshift(0);    // Adiciona no início    → [0, 1, 2, 3]
arr.shift();       // Remove do início      → [1, 2, 3]

// splice — remove/insere em posição específica
arr.splice(1, 1);           // remove 1 elemento na posição 1 → [1, 3]
arr.splice(1, 0, 10, 20);   // insere 10 e 20 na posição 1
```

---

## Métodos de Iteração

> [!TIP] Esses métodos não modificam o array original — retornam um novo valor.

### `map` — transforma

```javascript
const precos = [10, 25, 40];
const comDesconto = precos.map(p => p * 0.9);
// [9, 22.5, 36]
```

### `filter` — filtra por condição

```javascript
const idades = [15, 22, 17, 30, 12];
const maiores = idades.filter(i => i >= 18);
// [22, 30]
```

### `reduce` — acumula em um único valor

```javascript
const notas = [7, 8, 9, 6];
const media = notas.reduce((acc, n) => acc + n, 0) / notas.length;
// 7.5
```

### `find` / `findIndex` — busca

```javascript
const usuarios = [
  { id: 1, nome: "Ana" },
  { id: 2, nome: "Bob" }
];
const ana = usuarios.find(u => u.nome === "Ana");   // { id: 1, nome: "Ana" }
const idx = usuarios.findIndex(u => u.id === 2);    // 1
```

### `forEach` — itera sem retornar

```javascript
["a", "b", "c"].forEach((item, index) => {
  console.log(`${index}: ${item}`);
});
```

### `some` / `every` — verificação booleana

```javascript
const nums = [1, 3, 5, 8];
nums.some(n => n % 2 === 0);   // true — pelo menos um par
nums.every(n => n > 0);        // true — todos positivos
```

---

## Outros Métodos Úteis

```javascript
const a = [1, 2, 3];
const b = [4, 5, 6];

// concat — une arrays
const c = a.concat(b);  // [1, 2, 3, 4, 5, 6]

// spread — alternativa moderna
const d = [...a, ...b]; // [1, 2, 3, 4, 5, 6]

// slice — extrai parte sem modificar
a.slice(1, 3);   // [2, 3] (índice 1 até 2)

// includes — verifica existência
[1, 2, 3].includes(2);  // true

// indexOf
[1, 2, 3].indexOf(2);   // 1

// sort — ordena (modifica o original!)
[3, 1, 2].sort((a, b) => a - b);  // [1, 2, 3] crescente
[3, 1, 2].sort((a, b) => b - a);  // [3, 2, 1] decrescente

// reverse — inverte (modifica o original!)
[1, 2, 3].reverse();  // [3, 2, 1]

// join — converte em string
["a", "b", "c"].join("-");  // "a-b-c"

// flat — achata arrays aninhados
[[1, 2], [3, 4]].flat();  // [1, 2, 3, 4]
```

---

## Desestruturação

```javascript
const [primeiro, segundo, ...resto] = [1, 2, 3, 4, 5];
// primeiro = 1, segundo = 2, resto = [3, 4, 5]

// Ignorar elementos
const [, , terceiro] = [10, 20, 30];
// terceiro = 30
```

---

## Tabela Resumo

|Método|Retorna|Modifica original?|
|---|---|---|
|`push`|novo length|✅|
|`pop`|elemento removido|✅|
|`map`|novo array|❌|
|`filter`|novo array|❌|
|`reduce`|valor acumulado|❌|
|`find`|elemento ou `undefined`|❌|
|`sort`|array ordenado|✅|
|`slice`|novo array|❌|
|`splice`|elementos removidos|✅|