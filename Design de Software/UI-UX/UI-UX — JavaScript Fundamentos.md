---

tags: [ui-ux, javascript, desenvolvimento, web]

área: UI/UX

status: draft
---
# JavaScript — Fundamentos

[[UI-UX]] → Módulo 4 
## O que é JavaScript

Linguagem de programação de alto nível que adiciona **dinamicidade e interatividade** às páginas web. É **case sensitive**.

Executado via arquivo externo importado no HTML:

```html
<script src="js/scripts.js" defer></script>
```

> `defer` — aguarda o HTML ser lido antes de carregar o JS.

---

## Tipos de Dados e Operadores

### Numbers

```js
console.log(2);         // inteiro
console.log(2.6);       // ponto flutuante (separador: ponto)
console.log(2**2);      // potência = 4
console.log(Infinity);  // número especial
console.log(2*"teste"); // NaN — Not a Number
```

### Strings

```js
"aspas duplas"
'aspas simples'
`crase (template literal)`

// Concatenação
"Olá " + "mundo"

// Interpolação (só com crase)
`O resultado de 3 + 3 é: ${3+3}`
```

### Booleanos e Comparações

```js
true / false
8 >= 8   // true
8 == "8" // true  (compara valor)
8 === "8"// false (compara valor E tipo)
8 !== "8"// true
```

### Operadores Lógicos

```js
true && true   // AND — true
true || false  // OR — true
!true          // NOT — false
```

### Valores Vazios

- `null` — ausência de objeto
- `undefined` — variável declarada sem valor

> [!NOTE] Conversão de tipo silenciosa `3 * null` → 0 | `"5" - 4` → 1 | `"5" + 4` → "54" | `"a" * "b"` → NaN

---

## Variáveis

```js
let nome = "Dálton";       // pode ser reatribuída
const idade = 57;          // constante — não pode ser sobrescrita
let a = 1, b = 2, c = 3;  // múltiplas em uma linha
```

**Regras de nomenclatura:** não iniciar com número; não usar `@`, `#`; case sensitive; símbolos permitidos: `_` e `$`.

---

## Estruturas de Controle

```js
// if / else if / else
if (valor > 5) {
  console.log("maior que 5");
} else if (valor === 5) {
  console.log("igual a 5");
} else {
  console.log("menor que 5");
}

// switch
switch (value) {
  case 1: console.log("um"); break;
  case 2: console.log("dois"); break;
  default: console.log("outro");
}
```

---

## Estruturas de Repetição

```js
// while
let p = 0;
while (p < 5) { console.log(p); p++; }

// do while (executa ao menos uma vez)
let q = 5;
do { console.log(q); q--; } while (q > 0);

// for (mais comum)
for (let t = 0; t < 5; t++) { console.log(t); }

// break — sai do loop | continue — pula para próxima iteração
```

---

## Funções

```js
// Declaração padrão
function nomeFuncao(param) {
  return param * 2;
}

// Função em variável (anônima)
const funcao = function() { console.log("olá"); };

// Arrow function
const somar = (a, b) => a + b;
const raiz = (t) => t * t;

// Valor default
function dizerOla(nome = "Amigo") {
  console.log(`Olá, ${nome}!`);
}

// Recursão (função chama a si mesma — precisa de condição de parada)
function contarAteZero(n) {
  if (n <= 0) return;
  console.log(n);
  contarAteZero(n - 1);
}
```

### Escopo

- **Global** — fora da função
- **Local** — dentro da função
- **Aninhado** — dentro de blocos `{}` (if, for, while)

---

## Funções Nativas Úteis

```js
const nome = prompt("Seu nome:");  // entrada de dados
alert("Mensagem ao usuário");      // alerta na tela
Math.max(3, 7, 9);                 // maior valor
Math.floor(3.7);                   // arredonda para baixo → 3
Math.ceil(3.7);                    // arredonda para cima → 4
console.error("Erro!");
console.warn("Aviso!");
```

_Fonte: Fundamentos de Interfaces — Prof. Dálton Reis Leal (Projeto Desenvolve)_