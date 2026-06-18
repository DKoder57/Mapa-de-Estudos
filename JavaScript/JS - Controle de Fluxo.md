---
tags: [javascript, controle-de-fluxo, loops, condicionais]
área: JavaScript
status: draft

---

# ← [[JavaScript]]


## Condicionais

### if / else if / else

```javascript
let nota = 75;

if (nota >= 90) {
  console.log("A");
} else if (nota >= 70) {
  console.log("B");
} else if (nota >= 50) {
  console.log("C");
} else {
  console.log("Reprovado");
}
```

**Operador ternário** — para condições simples em uma linha:

```javascript
const resultado = nota >= 60 ? "Aprovado" : "Reprovado";
```

**Nullish coalescing (`??`)** — valor padrão quando `null` ou `undefined`:

```javascript
const nome = usuarioDigitado ?? "Visitante";
```

---

### switch

Preferível ao `if/else if` quando há múltiplos valores fixos para comparar.

```javascript
let dia = 3;

switch (dia) {
  case 1:
    console.log("Domingo");
    break;
  case 2:
    console.log("Segunda-feira");
    break;
  case 3:
    console.log("Terça-feira");
    break;
  default:
    console.log("Dia inválido");
}
```

> [!NOTE] `break` é obrigatório Sem o `break`, o código "cai" para o próximo `case` — comportamento raramente desejado chamado _fall-through_.

**Fall-through intencional** (agrupar cases):

```javascript
switch (mes) {
  case 1:
  case 3:
  case 5:
    console.log("31 dias");
    break;
  case 2:
    console.log("28 ou 29 dias");
    break;
}
```

---

## Laços de Repetição

### for

Quando se sabe o número exato de iterações.

```javascript
for (let i = 0; i < 5; i++) {
  console.log(i); // 0, 1, 2, 3, 4
}

// Iterando array
const frutas = ["maçã", "banana", "laranja"];
for (let i = 0; i < frutas.length; i++) {
  console.log(frutas[i]);
}

// for...of — forma moderna para iterar arrays
for (const fruta of frutas) {
  console.log(fruta);
}

// for...in — itera sobre as chaves de um objeto
const pessoa = { nome: "Ana", idade: 30 };
for (const chave in pessoa) {
  console.log(`${chave}: ${pessoa[chave]}`);
}
```

---

### while

Quando não se sabe quantas iterações são necessárias.

```javascript
let vidas = 3;

while (vidas > 0) {
  console.log(`Vidas restantes: ${vidas}`);
  vidas--;
}
// Após o loop: vidas === 0
```

> [!NOTE] Cuidado com loop infinito Garanta que a condição do `while` eventualmente se torne `false`. Se a variável de controle não for atualizada dentro do bloco, o programa trava.

---

### do...while

Executa o bloco **ao menos uma vez**, independentemente da condição.

```javascript
let tentativas = 0;

do {
  console.log("Tentativa:", tentativas);
  tentativas++;
} while (tentativas < 3);

// Mesmo com condição falsa desde o início, executa 1x:
let x = 100;
do {
  console.log("Executou!"); // imprime "Executou!" uma vez
} while (x < 5);
```

---

## Controle de Loop

```javascript
// break — interrompe o loop completamente
for (let i = 0; i < 10; i++) {
  if (i === 5) break;
  console.log(i); // 0, 1, 2, 3, 4
}

// continue — pula para a próxima iteração
for (let i = 0; i < 5; i++) {
  if (i === 2) continue;
  console.log(i); // 0, 1, 3, 4
}
```

**Labels** — para `break`/`continue` em loops aninhados:

```javascript
externo: for (let i = 0; i < 3; i++) {
  for (let j = 0; j < 3; j++) {
    if (i === j) break externo; // sai do loop externo
    console.log(`i:${i} j:${j}`);
  }
}
```

---

## Comparativo de Loops

|Loop|Quando usar|
|---|---|
|`for`|Número de iterações conhecido|
|`for...of`|Iterar elementos de array/iterável|
|`for...in`|Iterar chaves de objeto|
|`while`|Condição verificada antes de cada iteração|
|`do...while`|Garantir pelo menos uma execução|