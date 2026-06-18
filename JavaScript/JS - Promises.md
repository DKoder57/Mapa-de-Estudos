---

tags: [javascript, promises, async, await, assíncrono]

área: JavaScript

status: draft

---

# ← [[JavaScript]]


## O que são Promises?

Promises representam o resultado eventual de uma operação assíncrona. Em vez de bloquear a execução, o JS continua rodando e trata o resultado quando ele chegar.

**3 estados possíveis:**

```
pending  →  fulfilled (resolve)
         ↘  rejected  (reject)
```

---

## Criando uma Promise

```javascript
const minhaPromessa = new Promise((resolve, reject) => {
  const sucesso = true;

  setTimeout(() => {
    if (sucesso) {
      resolve("Operação concluída com sucesso!");
    } else {
      reject(new Error("Algo deu errado."));
    }
  }, 2000);
});
```

---

## Consumindo com `.then` / `.catch` / `.finally`

```javascript
minhaPromessa
  .then(resultado => {
    console.log(resultado); // "Operação concluída com sucesso!"
    return resultado.toUpperCase(); // valor passado para o próximo .then
  })
  .then(transformado => console.log(transformado))
  .catch(erro => {
    console.error("Erro:", erro.message); // captura qualquer rejeição na cadeia
  })
  .finally(() => {
    console.log("Finalizado — executado sempre"); // sucesso ou falha
  });
```

---

## Encadeamento de Promises

Cada `.then` pode retornar uma nova Promise, criando uma cadeia sequencial.

```javascript
function buscarUsuario(id) {
  return fetch(`/api/users/${id}`).then(r => r.json());
}

function buscarPedidos(usuario) {
  return fetch(`/api/orders?userId=${usuario.id}`).then(r => r.json());
}

buscarUsuario(1)
  .then(usuario => {
    console.log("Usuário:", usuario.nome);
    return buscarPedidos(usuario); // retorna nova promise
  })
  .then(pedidos => {
    console.log("Pedidos:", pedidos.length);
  })
  .catch(erro => console.error("Falha:", erro));
```

---

## Async / Await — Sintaxe Moderna

`async/await` é açúcar sintático sobre Promises — o código parece síncrono, mas é assíncrono.

```javascript
async function carregarDados(id) {
  try {
    const res  = await fetch(`/api/users/${id}`);
    const user = await res.json();
    console.log(user.nome);
    return user;
  } catch (erro) {
    console.error("Erro ao carregar:", erro.message);
  } finally {
    console.log("Requisição finalizada");
  }
}

// Funções async sempre retornam uma Promise
carregarDados(1).then(user => console.log("Retorno:", user));
```

> [!NOTE] `await` só funciona dentro de `async` Tentar usar `await` fora de uma função `async` gera um SyntaxError (a não ser no top-level de módulos ES6).

---

## Promise.all — Paralelo

Executa várias promises em paralelo. Resolve quando **todas** resolverem. Rejeita se **qualquer uma** falhar.

```javascript
const [usuarios, produtos, pedidos] = await Promise.all([
  fetch("/api/users").then(r => r.json()),
  fetch("/api/products").then(r => r.json()),
  fetch("/api/orders").then(r => r.json()),
]);
```

---

## Promise.allSettled — Paralelo sem falha total

Aguarda todas, independentemente de sucesso ou falha.

```javascript
const resultados = await Promise.allSettled([
  Promise.resolve("ok"),
  Promise.reject(new Error("falhou")),
  Promise.resolve("ok também"),
]);

resultados.forEach(r => {
  if (r.status === "fulfilled") console.log("✓", r.value);
  else console.log("✗", r.reason.message);
});
```

---

## Promise.race — O mais rápido vence

Resolve/rejeita assim que a primeira Promise terminar.

```javascript
const resultado = await Promise.race([
  fetch("/api/fast-server"),
  fetch("/api/slow-server"),
]);
// Usa a resposta do servidor mais rápido
```

---

## Comparativo: Callbacks → Promises → Async/Await

```javascript
// Callback hell (evitar)
buscarA(function(a) {
  buscarB(a, function(b) {
    buscarC(b, function(c) {
      console.log(c); // pirâmide da morte
    });
  });
});

// Promises (melhor)
buscarA()
  .then(a => buscarB(a))
  .then(b => buscarC(b))
  .then(c => console.log(c))
  .catch(console.error);

// Async/Await (mais legível)
async function fluxo() {
  const a = await buscarA();
  const b = await buscarB(a);
  const c = await buscarC(b);
  console.log(c);
}
```