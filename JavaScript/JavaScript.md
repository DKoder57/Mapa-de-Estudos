---
tags:
- javascript
- programacao
- frontend
---

# ⚡ JavaScript

Linguagem de programação essencial para a web — responsável pela lógica, interatividade e dinamismo das páginas. Usada tanto no front-end (browser) quanto no back-end (Node.js).

---

## 📁 Estrutura do Módulo

```
JavaScript
├── [[JS — Fundamentos]]           → variáveis, tipos, escopo, comentários
├── [[JS — Funções]]               → regulares, anônimas, arrow
├── [[JS — Operadores]]            → aritméticos, lógicos, atribuição, comparação
├── [[JS — Controle de Fluxo]]     → if/else, switch, for, while, do...while
├── [[JS — Strings]]               → métodos: slice, trim, split, replace, concat...
├── [[JS — JSON]]                  → sintaxe, parse, stringify, manipulação
├── [[JS — Arrays]]                → criação, métodos básicos e avançados
├── [[JS — DOM e Eventos]]         → árvore DOM, seletores, eventos de mouse/teclado
├── [[JS — Consumo de API]]        → Fetch, Axios, AJAX, APIs falsas
├── [[JS — Orientação a Objetos]]  → classes, herança, encapsulamento, polimorfismo
├── [[JS — Exceções]]              → try/catch/finally, tipos de erro, encapsulamento
├── [[JS — Promises]]              → estados, .then/.catch, encadeamento, async/await
└── [[JS — Boas Práticas]]         → Git, testes, portfólio, frameworks de mercado
```

---

## 🧠 Visão Geral

JavaScript é uma linguagem **interpretada**, **de alto nível** e **dinamicamente tipada**. Os três pilares da web trabalham juntos:

|Tecnologia|Responsabilidade|
|---|---|
|HTML|Estrutura do conteúdo|
|CSS|Aparência e layout|
|**JavaScript**|Lógica e interatividade|

> [!NOTE] JS é universal Com Node.js, JavaScript roda no servidor. Com React, Vue ou Angular, domina o front-end moderno. Uma linguagem para toda a stack.

---

## 🔤 [[JS - Fundamentos]]

### Variáveis

Três formas de declarar, com escopos distintos:

```javascript
var nome = "João";   // Escopo de função/global — evitar em código novo
let idade = 25;      // Escopo de bloco — uso padrão atual
const PI = 3.14159;  // Constante — valor não pode ser reatribuído
```

> [!TIP] Regra prática Use `const` por padrão. Use `let` quando precisar reatribuir. Nunca use `var`.

**Escopo de bloco:** `let` e `const` ficam restritas ao bloco `{}` onde foram declaradas. `var` vaza para o escopo da função.

### Comentários

```javascript
// Comentário de linha única

/*
  Comentário de bloco —
  use para documentar funções e lógicas complexas
*/
```

→ [[JS - Fundamentos]]

---

## 🔧 [[JS - Funções]]

Três formas principais de declarar funções:

```javascript
// Regular — suporta hoisting (pode ser chamada antes da declaração)
function somar(a, b) {
  return a + b;
}

// Anônima — atribuída a uma variável, sem hoisting
const saudacao = function(nome) {
  return `Olá, ${nome}!`;
};

// Arrow (ES6) — sintaxe concisa, this léxico
const dobrar = n => n * 2;
const multiplicar = (a, b) => a * b;
```

> [!NOTE] Arrow e `this` Funções arrow não possuem `this` próprio — herdam o do contexto externo. Isso as torna ideais para callbacks, mas inadequadas como métodos de objetos.

→ [[JS - Funções]]

---

## ➕ Operadores

Símbolos para realizar cálculos, comparações e atribuições entre valores.

### Aritméticos

|Operador|Operação|Exemplo|
|---|---|---|
|`+`|Adição / concatenação|`5 + 3` → `8`|
|`-`|Subtração|`10 - 4` → `6`|
|`*`|Multiplicação|`3 * 4` → `12`|
|`/`|Divisão|`10 / 2` → `5`|
|`%`|Módulo (resto)|`11 % 2` → `1`|
|`**`|Exponenciação|`2 ** 3` → `8`|
|`++` / `--`|Incremento / decremento|`i++`|

### Lógicos

|Operador|Significado|Resultado|
|---|---|---|
|`&&`|E lógico|`true` apenas se ambos forem `true`|
|`\|`|OU lógico|`true` se pelo menos um for `true`|
|`!`|Negação|Inverte o valor booleano|

### Atribuição combinada

```javascript
x += 5;  // x = x + 5
x -= 3;  // x = x - 3
x *= 2;  // x = x * 2
x /= 4;  // x = x / 4
x %= 3;  // x = x % 3
```


---

## 🔀 [[JS - Controle de Fluxo]]

Decisões e repetições que direcionam a execução do código.

### Condicionais

```javascript
// if / else if / else
if (nota >= 90) {
  console.log("A");
} else if (nota >= 70) {
  console.log("B");
} else {
  console.log("Reprovado");
}

// switch — mais legível para múltiplos valores fixos
switch (dia) {
  case 1: console.log("Domingo"); break;
  case 2: console.log("Segunda"); break;
  default: console.log("Dia inválido");
}
```

### Laços de repetição

```javascript
// for — quando se sabe o número de iterações
for (let i = 0; i < 5; i++) { console.log(i); }

// while — enquanto a condição for verdadeira
let n = 0;
while (n < 5) { console.log(n); n++; }

// do...while — executa ao menos uma vez
let x = 10;
do { console.log(x); x++; } while (x < 5); // executa 1x mesmo com condição falsa
```

→ [[JS - Controle de Fluxo]]

---

## 📝 Strings

Strings são **imutáveis** — métodos retornam novos valores, nunca alteram o original.

```javascript
let s = "  JavaScript é incrível  ";

s.length          // tamanho
s.trim()          // remove espaços das pontas → "JavaScript é incrível"
s.toUpperCase()   // "  JAVASCRIPT É INCRÍVEL  "
s.toLowerCase()   // "  javascript é incrível  "
s.slice(2, 12)    // extrai por índice → "JavaScript"
s.replace("incrível", "poderoso")  // substitui
s.split(" ")      // divide em array pelo delimitador
s.includes("Java")  // → true
```

**Template literals** (crase) — forma moderna de concatenar:

```javascript
const nome = "Maria";
const msg = `Olá, ${nome}! Bem-vinda.`;
```


---

## 📦 JSON

JSON (_JavaScript Object Notation_) — formato leve de troca de dados, baseado em pares chave-valor.

```json
{
  "nome": "Carlos",
  "idade": 30,
  "enderecos": { "cidade": "São Paulo" },
  "telefones": ["11111-2222", "33333-4444"]
}
```

**Métodos essenciais:**

```javascript
// Objeto → String (para enviar via rede)
const str = JSON.stringify(objeto);

// String → Objeto (ao receber dados de uma API)
const obj = JSON.parse(str);
```

**Acesso e manipulação:**

```javascript
pessoa.nome         // "Carlos"
pessoa.telefones[0] // "11111-2222"
pessoa.idade = 31   // modifica
delete pessoa.telefones  // remove propriedade
```

→ [[JS — JSON]]

---

## 🗂️ [[JS - Arrays]]

Arrays são coleções ordenadas de elementos, acessados por índice (base 0).

```javascript
let frutas = ["maçã", "banana", "laranja"];
frutas[0]  // "maçã"
```

**Métodos básicos:**

|Método|Ação|
|---|---|
|`push(x)`|Adiciona no final|
|`pop()`|Remove do final|
|`unshift(x)`|Adiciona no início|
|`shift()`|Remove do início|
|`splice(i, n)`|Remove `n` elementos a partir do índice `i`|

**Métodos de iteração:**

```javascript
// map — transforma cada elemento, retorna novo array
const dobrados = [1, 2, 3].map(n => n * 2);  // [2, 4, 6]

// filter — filtra por condição, retorna novo array
const pares = [1, 2, 3, 4].filter(n => n % 2 === 0);  // [2, 4]

// reduce — acumula em um único valor
const soma = [1, 2, 3].reduce((acc, n) => acc + n, 0);  // 6

// forEach — itera sem retornar
["a", "b"].forEach(item => console.log(item));

// find — retorna o primeiro elemento que satisfaz a condição
const maior = [5, 12, 3].find(n => n > 10);  // 12
```

→ [[JS - Arrays]]

---

## 🌐 [[JS - DOM e Eventos]]

O **DOM** (_Document Object Model_) é a representação em árvore do HTML, manipulável via JavaScript.

```javascript
// Selecionando elementos
document.getElementById("titulo")
document.querySelector(".classe")
document.querySelectorAll("p")

// Modificando
elemento.innerHTML = "<strong>Novo conteúdo</strong>";
elemento.style.backgroundColor = "blue";
elemento.classList.add("ativo");

// Criando e inserindo
const div = document.createElement("div");
div.textContent = "Novo bloco";
document.body.appendChild(div);
```

**Eventos principais:**

```javascript
// Mouse
btn.addEventListener("click", () => alert("Clicou!"));
btn.addEventListener("mouseover", () => btn.style.color = "red");

// Teclado
document.addEventListener("keydown", e => console.log(e.key));

// Formulário
form.addEventListener("submit", e => {
  e.preventDefault(); // impede recarregamento da página
  // validar e processar...
});

// Foco
input.addEventListener("focus", () => input.style.background = "yellow");
input.addEventListener("blur",  () => input.style.background = "");
```

→ [[JS - DOM e Eventos]]

---

## 🌍 Consumo de API

APIs são interfaces que permitem comunicação entre sistemas. Dados trocados geralmente em JSON.

**Fetch API (nativa):**

```javascript
fetch("https://api.exemplo.com/usuarios")
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error("Erro:", error));
```

**Axios (biblioteca):**

```javascript
axios.get("https://api.exemplo.com/dados")
  .then(res => console.log(res.data))
  .catch(err => console.error(err));
```

**API falsa para testes:** `https://jsonplaceholder.typicode.com`

> [!TIP] Ferramentas de teste Use **Postman** ou **Insomnia** para testar endpoints de APIs sem escrever código.

→ [[JS — Consumo de API]]

---

## 🏗️ [[JS - Orientação a Objetos]]

### Classes e Objetos

Molde (classe) e instância concreta (objeto) com atributos e comportamentos.

```javascript
class Animal {
  constructor(nome, tipo) {
    this.nome = nome;
    this.tipo = tipo;
  }
  descrever() {
    console.log(`${this.nome} é um ${this.tipo}.`);
  }
}

const gato = new Animal("Mochi", "felino");
gato.descrever(); // "Mochi é um felino."
```

### Herança

Reutilizar comportamento da classe pai e proteger dados internos.

```javascript
class Cachorro extends Animal {
  constructor(nome) {
    super(nome, "canino"); // chama o constructor da classe pai
  }
  latir() { console.log("Au au!"); }
}
```

### Encapsulamento

```javascript
class ContaBancaria {
  #saldo; // campo privado (ES2022)

  constructor(saldoInicial) { this.#saldo = saldoInicial; }
  depositar(valor) { this.#saldo += valor; }
  getSaldo() { return this.#saldo; }
}
```

> [!NOTE] 4 pilares da POO **Abstração** — modelar apenas o essencial · **Encapsulamento** — proteger dados internos · **Herança** — reutilizar comportamento da classe pai · **Polimorfismo** — mesmo método, comportamentos distintos por classe

→ [[JS - Orientação a Objetos]]

---

## ⚠️ Exceções

Erros inesperados durante a execução — capturados e tratados sem quebrar o programa.

```javascript
try {
  // código que pode falhar
  const resultado = operacaoArriscada();
} catch (error) {
  // trata o erro sem quebrar o programa
  console.error("Erro capturado:", error.message);
} finally {
  // executa sempre, independentemente de erro
  console.log("Operação concluída.");
}

// Lançando um erro personalizado
function validar(valor) {
  if (valor <= 0) throw new Error("Valor deve ser positivo");
}
```

**Tipos comuns de erro em JS:** `TypeError`, `ReferenceError`, `SyntaxError`, `RangeError`

→ [[JS — Exceções]]

---

## 🔄 [[JS - Promises]]

Promises representam operações assíncronas com três estados: **pending → fulfilled | rejected**

```javascript
// Criando
const promessa = new Promise((resolve, reject) => {
  setTimeout(() => resolve("Sucesso!"), 2000);
});

// Consumindo
promessa
  .then(resultado => console.log(resultado))
  .catch(erro => console.log(erro));

// Encadeamento
buscarDados()
  .then(dados => processarDados(dados))
  .then(resultado => salvarResultado(resultado))
  .catch(erro => console.error(erro));
```

**Async/Await** — sintaxe mais legível para promises:

```javascript
async function carregarUsuario(id) {
  try {
    const res = await fetch(`/api/users/${id}`);
    const user = await res.json();
    return user;
  } catch (erro) {
    console.error("Falha ao carregar:", erro);
  }
}
```

→ [[JS - Promises]]

---

## ✅ Boas Práticas de Mercado

**Versionamento com Git:**

- Commits frequentes com mensagens descritivas
- Branches por feature/bugfix
- Pull Requests com code review antes de merge no `main`

**Testes:**

|Tipo|O que verifica|
|---|---|
|Unitário|Funções e módulos isolados (Jest)|
|Integração|Comunicação entre partes do sistema|
|Aceitação|Fluxos do ponto de vista do usuário|

**Frameworks de mercado:**

|Área|Opções|
|---|---|
|Front-end|React, Vue.js, Angular|
|Back-end|Node.js + Express, NestJS|
|ORM|Prisma, TypeORM, Sequelize|
|Banco|PostgreSQL (relacional), MongoDB (NoSQL)|

> [!TIP] Portfólio Publique projetos no GitHub com README claro — objetivo, tecnologias usadas, como rodar localmente. É o principal diferencial em processos seletivos.


---

_Última atualização: {{date}}_