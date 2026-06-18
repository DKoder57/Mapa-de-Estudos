---

tags: [javascript, dom, eventos, interatividade]

área: JavaScript

status: draft
---


# ← [[JavaScript]]


## O que é o DOM?

O **Document Object Model** é a representação em árvore do documento HTML, criada pelo browser ao carregar a página. JavaScript acessa e manipula essa árvore em tempo real, sem recarregar a página.

```
Document (raiz)
└── html
    ├── head
    │   └── title
    └── body
        ├── h1
        ├── p
        └── div
            └── button
```

---

## Selecionando Elementos

```javascript
// Por ID — retorna um único elemento
const titulo = document.getElementById("titulo");

// Por seletor CSS — retorna o primeiro que casar
const btn = document.querySelector(".btn-primario");
const input = document.querySelector("input[type='email']");

// Por seletor CSS — retorna NodeList (todos que casarem)
const paragrafos = document.querySelectorAll("p");
const itens = document.querySelectorAll(".item");

// Iterar NodeList
paragrafos.forEach(p => console.log(p.textContent));

// Formas legadas (menos usadas hoje)
document.getElementsByClassName("classe"); // HTMLCollection
document.getElementsByTagName("div");      // HTMLCollection
```

---

## Modificando Elementos

```javascript
const el = document.querySelector("#titulo");

// Conteúdo
el.textContent = "Texto simples (sem HTML)";
el.innerHTML   = "<strong>Texto com HTML</strong>";

// Atributos
el.setAttribute("id", "novoId");
el.getAttribute("class");
el.removeAttribute("disabled");

// Estilos inline
el.style.color = "red";
el.style.fontSize = "24px";
el.style.backgroundColor = "#f0f0f0";

// Classes CSS
el.classList.add("ativo");
el.classList.remove("inativo");
el.classList.toggle("visivel");
el.classList.contains("ativo"); // → true/false
```

---

## Criando e Inserindo Elementos

```javascript
// Criar
const div = document.createElement("div");
div.className = "card";
div.innerHTML = "<h2>Título</h2><p>Conteúdo</p>";

// Inserir
document.body.appendChild(div);        // no final do body
document.body.prepend(div);            // no início do body
pai.insertBefore(div, irmao);          // antes de um irmão

// Remover
div.remove();
pai.removeChild(filho);
```

---

## Eventos

Eventos são ações do usuário (ou do browser) capturadas pelo JavaScript.

### Adicionando Event Listeners

```javascript
const btn = document.querySelector("#meuBotao");

btn.addEventListener("click", function(event) {
  console.log("Clicado!");
  console.log(event.target); // elemento que disparou o evento
});

// Com arrow function
btn.addEventListener("click", (e) => {
  e.preventDefault(); // previne comportamento padrão (ex: submit de form)
  e.stopPropagation(); // para a propagação do evento
});

// Removendo
const handler = () => console.log("clique");
btn.addEventListener("click", handler);
btn.removeEventListener("click", handler);
```

---

### Eventos de Mouse

```javascript
el.addEventListener("click",      () => {}); // clique simples
el.addEventListener("dblclick",   () => {}); // clique duplo
el.addEventListener("mouseover",  () => el.style.background = "lightblue");
el.addEventListener("mouseout",   () => el.style.background = "");
el.addEventListener("mousedown",  () => {}); // botão pressionado
el.addEventListener("mouseup",    () => {}); // botão solto
el.addEventListener("mousemove",  (e) => console.log(e.clientX, e.clientY));
```

---

### Eventos de Teclado

```javascript
document.addEventListener("keydown", (e) => {
  console.log(e.key);     // "a", "Enter", "ArrowUp"...
  console.log(e.code);    // "KeyA", "Enter", "ArrowUp"
  console.log(e.ctrlKey); // true se Ctrl estava pressionado
});

document.addEventListener("keyup", (e) => {}); // tecla liberada
```

---

### Eventos de Formulário

```javascript
const form  = document.querySelector("form");
const input = document.querySelector("#email");

form.addEventListener("submit", (e) => {
  e.preventDefault(); // sem isso, a página recarrega
  const dados = new FormData(form);
  console.log(dados.get("email"));
});

input.addEventListener("input",  (e) => console.log(e.target.value)); // a cada digitação
input.addEventListener("change", (e) => console.log(e.target.value)); // ao perder foco com mudança
input.addEventListener("focus",  () => input.style.background = "yellow");
input.addEventListener("blur",   () => input.style.background = "");
```

---

### Eventos de Janela / Documento

```javascript
window.addEventListener("load",   () => console.log("Página carregada"));
window.addEventListener("resize", () => console.log(window.innerWidth));
window.addEventListener("scroll", () => console.log(window.scrollY));

document.addEventListener("DOMContentLoaded", () => {
  // DOM pronto, mas imagens podem ainda não ter carregado
  // Melhor ponto para inicializar scripts
});
```

---

## Event Delegation

Em vez de adicionar listeners em cada filho, adicione no pai e verifique o alvo:

```javascript
const lista = document.querySelector("#lista");

lista.addEventListener("click", (e) => {
  if (e.target.matches("li")) {
    console.log("Item clicado:", e.target.textContent);
  }
});
```

> [!TIP] Por que usar delegation? Funciona para elementos criados dinamicamente depois do listener ser registrado. Muito mais eficiente do que N listeners.

---

## Tabela de Eventos Comuns

|Evento|Dispara quando...|
|---|---|
|`click`|Usuário clica|
|`dblclick`|Duplo clique|
|`mouseover`|Cursor entra no elemento|
|`mouseout`|Cursor sai do elemento|
|`keydown`|Tecla é pressionada|
|`keyup`|Tecla é liberada|
|`submit`|Formulário é enviado|
|`input`|Valor de input muda|
|`change`|Input perde foco com mudança|
|`focus`|Elemento recebe foco|
|`blur`|Elemento perde foco|
|`load`|Página/recurso carregado|
|`DOMContentLoaded`|DOM pronto|
|`resize`|Janela redimensionada|
|`scroll`|Página rolada|