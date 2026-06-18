---

tags: [ui-ux, javascript, dom, eventos, web]

área: UI/UX

status: draft
---
# DOM e Eventos no JavaScript

[[UI-UX]] → Módulo 4 

## O que é o DOM

**Document Object Model** — representação em árvore dos elementos HTML de uma página. Permite que o JavaScript:

- Adicione, altere ou remova conteúdo
- Altere o estilo dos elementos
- Responda a ações do usuário

O DOM funciona como "interface" entre o JavaScript e o HTML.

---

## Acessando Elementos no DOM

```js
// Por tag
document.getElementsByTagName("p")

// Por ID (retorna único elemento)
document.getElementById("titulo")

// Por classe (retorna coleção)
document.getElementsByClassName("produto")

// Por seletor CSS (mais usado — flexível)
document.querySelector(".btn")          // primeiro elemento
document.querySelectorAll(".link")      // todos os elementos
document.querySelector("#container")   // por ID com #
```

---

## Manipulando o DOM

```js
// Criar elemento
const p = document.createElement("p");
const texto = document.createTextNode("Conteúdo");
p.appendChild(texto);

// Inserir antes de outro elemento
pai.insertBefore(novoElemento, elementoReferencia);

// Adicionar ao final de um pai
pai.appendChild(novoElemento);

// Substituir elemento
pai.replaceChild(novoElemento, elementoAntigo);

// Alterar conteúdo textual
elemento.textContent = "Novo Título";
```

---

## Atributos e Propriedades

```js
// Ler/alterar atributos
elemento.getAttribute("href")
elemento.setAttribute("href", "https://exemplo.com")
elemento.setAttribute("target", "_blank")

// Propriedades de dimensão
elemento.offsetWidth     // largura total
elemento.offsetHeight    // altura total
elemento.clientWidth     // largura sem bordas
elemento.getBoundingClientRect() // posição + dimensões completas
```

---

## Estilos via JavaScript

```js
// Alterar CSS inline (camelCase para propriedades com traço)
container.style.color = "red";
container.style.backgroundColor = "green";  // background-color → camelCase
container.style.padding = "2px";

// Iterar sobre HTMLCollection
for (const li of listaItens) {
  li.style.backgroundColor = "gray";
}
```

---

## Eventos

Eventos correspondem a **ações do usuário** (clicar, teclar, mover o mouse).

```js
// Adicionar evento
elemento.addEventListener("click", function() {
  console.log("clicou");
});

// Remover evento (a função NÃO pode ser anônima para remover)
function mensagem() { console.log("clicou"); }
btn.addEventListener("click", mensagem);
btn.removeEventListener("click", mensagem);

// Acessar informações do evento
titulo.addEventListener("click", (event) => {
  console.log(event.target);
  console.log(event.offsetX);
});

// Prevenir comportamento padrão
link.addEventListener("click", (e) => {
  e.preventDefault();
});
```

### Tipos de Eventos

|Tipo|Eventos|
|---|---|
|**Mouse**|`click`, `dblclick`, `mousedown`, `mouseup`, `mousemove`|
|**Teclado**|`keydown`, `keyup`|
|**Scroll**|`scroll` + `window.scrollY`|
|**Foco (inputs)**|`focus`, `blur`|
|**Carregamento**|`load`, `beforeunload`|

```js
// Scroll com condição
window.addEventListener("scroll", (e) => {
  if (window.scrollY > 200) {
    console.log("rolou mais de 200px");
  }
});

// Focus/blur em input
input.addEventListener("focus", () => console.log("entrou"));
input.addEventListener("blur", () => console.log("saiu"));

// Carregamento da página
window.addEventListener("load", () => console.log("página carregada"));
```

---

## No Projeto Landing Page

- **Videoaula 27** — DOM e navegação pela estrutura
- **Videoaula 28** — Eventos associados a botões e janela; condicionais
- **Videoaula 30** — JavaScript no formulário da seção Modal
- **Videoaula 24** — `position: absolute/relative` para botão WhatsApp fixo; Back to Top via JS

_Fonte: Fundamentos de Interfaces — Prof. Dálton Reis Leal (Projeto Desenvolve)_