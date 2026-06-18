---
tags:

- web
- html
- css
- bootstrap
área: Web
status: draft
---
# 🌐 Web

Área de desenvolvimento web — estrutura, estilização e frameworks. Cobre desde os fundamentos da internet até componentes avançados com Bootstrap.

---

## 📁 Estrutura do Módulo

```
Web
├── Internet & Ferramentas
│   ├── [[Internet]]
│   ├── [[IDE e VS Code]]
│   └── [[GitHub Pages]]
├── HTML
│   ├── [[HTML — Fundamentos]]
│   ├── [[HTML — Elementos de Texto]]
│   ├── [[HTML — Containers e Semântica]]
│   ├── [[HTML — Multimídia e Links]]
│   ├── [[HTML — Tabelas]]
│   └── [[HTML — Formulários]]
├── CSS
│   ├── [[CSS — Fundamentos]]
│   ├── [[CSS — Box Model]]
│   ├── [[CSS — Seletores e Especificidade]]
│   ├── [[CSS — Unidades e Cores]]
│   ├── [[CSS — Estilização Textual]]
│   ├── [[CSS — Layout (Flexbox, Grid, Float)]]
│   ├── [[CSS — Efeitos e Transições]]
│   └── [[CSS — Design Responsivo e Media Queries]]
└── Bootstrap
    ├── [[Bootstrap — Configuração e Grid]]
    ├── [[Bootstrap — Componentes (Menus, Textos, Botões)]]
    └── [[Bootstrap — Avançado (Cards, Modais, Tabelas, Imagens)]]
```

---

## 🌍 Internet & Ferramentas

### Internet

A internet surgiu da **ARPANET** (década de 1960), criada pelos EUA durante a Guerra Fria para manter comunicação militar segura. O protocolo **TCP/IP** (1983) padronizou a comunicação entre redes. Em 1989, **Tim Berners-Lee** propôs a **WWW** e o **HTML**, criando a web como conhecemos.

> [!NOTE] W3C O **World Wide Web Consortium (W3C)**, fundado por Berners-Lee em 1994, padroniza HTML, CSS e JavaScript — garantindo que a web funcione em qualquer dispositivo, idioma ou região.

**Browsers** renderizam HTML, CSS e JavaScript. Os principais hoje: Chrome, Firefox, Edge, Safari e Opera — todos suportam HTML5/CSS3.

**Motores de busca** (Google, Bing) usam _crawlers_ para indexar páginas. O PageRank do Google classifica resultados por relevância e autoridade. SEO é o conjunto de técnicas para melhorar esse ranking.


---

### IDE - VS Code

O **Visual Studio Code** é a IDE padrão do mercado para desenvolvimento web. Extensões essenciais:

|Extensão|Função|
|---|---|
|Live Server|Preview em tempo real no browser|
|Auto Rename Tag|Renomeia tags HTML em par|
|Color Highlight|Visualiza cores no CSS|
|Prettier|Formatação de código|
|Material Icon Theme|Ícones de arquivos|
|ESLint|Qualidade de código JS|


---

## 🏗️ HTML

### Fundamentos

HTML (_HyperText Markup Language_) estrutura o conteúdo de páginas web. Todo documento HTML segue esta hierarquia base:

```html
<!DOCTYPE html>
<html lang="pt-BR">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Título da Página</title>
  </head>
  <body>
    <!-- conteúdo visível -->
  </body>
</html>
```

> [!NOTE] Elementos vs Atributos **Elementos** são as tags (`<p>`, `<h1>`, `<a>`). **Atributos** são propriedades dentro da tag de abertura (`href`, `src`, `alt`, `lang`).



---

### Elementos de Texto

|Tag|Uso|
|---|---|
|`<h1>` a `<h6>`|Títulos em hierarquia|
|`<p>`|Parágrafo|
|`<strong>`|Negrito (semântico)|
|`<em>`|Itálico (semântico)|
|`<ul>` / `<ol>` / `<dl>`|Listas não ordenada / ordenada / de definição|
|`<blockquote>`|Citação em bloco|
|`<abbr>`|Abreviação|


---

### Containers e Semântica

|Tag|Função semântica|
|---|---|
|`<header>`|Cabeçalho da página/seção|
|`<nav>`|Navegação|
|`<main>`|Conteúdo principal|
|`<aside>`|Barra lateral|
|`<section>`|Seção temática|
|`<article>`|Conteúdo independente|
|`<footer>`|Rodapé|
|`<div>`|Agrupamento genérico (sem semântica)|

> [!TIP] Prefira semântica Tags semânticas melhoram acessibilidade e SEO. Use `<div>` apenas quando nenhuma tag semântica se aplicar.


---

### Multimídia e Links

```html
<!-- Link absoluto -->
<a href="https://exemplo.com" target="_blank">Texto</a>

<!-- Link relativo -->
<a href="./pagina.html">Página interna</a>

<!-- Âncora -->
<a href="#secao">Ir para seção</a>

<!-- Imagem -->
<img src="./foto.jpg" alt="Descrição da imagem">
```



---

### Tabelas

```html
<table>
  <thead>
    <tr><th>Nome</th><th>Idade</th></tr>
  </thead>
  <tbody>
    <tr><td>Ana</td><td>25</td></tr>
  </tbody>
  <tfoot>
    <tr><td colspan="2">Total: 1 registro</td></tr>
  </tfoot>
</table>
```

> [!NOTE] Mesclagem de células `colspan` mescla colunas. `rowspan` mescla linhas.


---

### Formulários

```html
<form action="/enviar" method="POST">
  <label for="nome">Nome:</label>
  <input type="text" id="nome" name="nome">

  <input type="checkbox" name="aceito"> Aceito os termos
  <input type="radio" name="sexo" value="m"> Masculino

  <select name="cidade">
    <option value="sp">São Paulo</option>
  </select>

  <button type="submit">Enviar</button>
</form>
```


---

## 🎨 CSS

### Fundamentos

CSS (_Cascading Style Sheets_) estiliza páginas HTML. Sintaxe básica:

```css
seletor {
  propriedade: valor;
}
```

**Formas de aplicar CSS:**

- **Inline:** `<p style="color: red;">` — evitar, baixa manutenibilidade
- **Interno:** `<style>` dentro do `<head>` — use para protótipos
- **Externo:** arquivo `.css` separado — **forma recomendada**


---

### Box Model

Todo elemento HTML é uma caixa composta por quatro camadas:

```
┌─────────────────────────┐
│         margin          │
│  ┌───────────────────┐  │
│  │      border       │  │
│  │  ┌─────────────┐  │  │
│  │  │   padding   │  │  │
│  │  │  ┌───────┐  │  │  │
│  │  │  │content│  │  │  │
│  │  │  └───────┘  │  │  │
│  │  └─────────────┘  │  │
│  └───────────────────┘  │
└─────────────────────────┘
```

> [!TIP] box-sizing Use `box-sizing: border-box` para incluir padding e border no cálculo da largura total — comportamento muito mais intuitivo.


---

### Seletores e Especificidade

|Tipo|Exemplo|Peso|
|---|---|---|
|Universal|`*`|0|
|Elemento|`p`|1|
|Classe|`.destaque`|10|
|ID|`#titulo`|100|
|Inline|`style=""`|1000|
|`!important`|—|Quebra a cascata|

> [!NOTE] Regra dos 100 A especificidade define qual regra vence quando há conflito. Soma os pesos: ID (100) + Classe (10) + Elemento (1).


---

### Unidades e Cores

**Cores:**

- Nome: `red`, `blue`
- Hexadecimal: `#FF5733`
- RGB: `rgb(255, 87, 51)`
- RGBa: `rgba(255, 87, 51, 0.8)`
- HSL: `hsl(11, 100%, 60%)`

**Unidades de tamanho:**

|Unidade|Descrição|
|---|---|
|`px`|Pixels — valor fixo|
|`%`|Relativo ao elemento pai|
|`em`|Relativo ao font-size do elemento|
|`rem`|Relativo ao font-size do `<html>`|
|`vh` / `vw`|Relativo ao viewport|


---

### Layout — Flexbox, Grid e Float

**Flexbox** — distribuição em uma dimensão (linha ou coluna):

```css
.container {
  display: flex;
  justify-content: center;   /* eixo principal */
  align-items: center;       /* eixo secundário */
  flex-wrap: wrap;
}
```

**Grid** — distribuição em duas dimensões:

```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
}
```

**Tipos de layout:**

- **Centralizado:** conteúdo fixo no centro com `margin: auto`
- **Fixo:** largura definida em `px`, não se adapta à tela
- **Elástico:** usa `em`/`rem`, adapta ao zoom e fonte do usuário


---

### Design Responsivo e Media Queries

Media queries aplicam estilos condicionados ao dispositivo:

```css
/* Mobile first */
.container { width: 100%; }

/* Tablet */
@media screen and (min-width: 768px) {
  .container { width: 750px; }
}

/* Desktop */
@media screen and (min-width: 1024px) {
  .container { width: 960px; }
}
```

> [!NOTE] Viewport obrigatório Sempre declare `<meta name="viewport" content="width=device-width, initial-scale=1.0">` para media queries funcionarem em mobile.

**Parâmetros de media query:** `min-width`, `max-width`, `min-height`, `orientation` (landscape/portrait), `resolution` (dpi).


---

## ⚡ Bootstrap

### Configuração e Grid

Bootstrap é um framework CSS que entrega componentes prontos e responsivos. Configuração em 3 passos:

```html
<head>
  <!-- 1. CSS do Bootstrap -->
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5/dist/css/bootstrap.min.css">
</head>
<body>
  <!-- 2. Conteúdo -->

  <!-- 3. JS do Bootstrap (final do body) -->
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5/dist/js/bootstrap.bundle.min.js"></script>
</body>
```

**Sistema de Grid — 12 colunas:**

```html
<div class="container">
  <div class="row">
    <div class="col-md-6">Coluna 1 (50%)</div>
    <div class="col-md-6">Coluna 2 (50%)</div>
  </div>
</div>
```

> [!TIP] Breakpoints Bootstrap `col-` (xs, <576px) · `col-sm-` (≥576px) · `col-md-` (≥768px) · `col-lg-` (≥992px) · `col-xl-` (≥1200px)


---

### Componentes — Menus, Textos e Botões

**Botões:**

```html
<button class="btn btn-primary">Primário</button>
<button class="btn btn-outline-secondary">Outline</button>
<button class="btn btn-danger btn-lg">Grande</button>
```

**Navbar:**

```html
<nav class="navbar navbar-expand-lg navbar-dark bg-dark">
  <a class="navbar-brand" href="#">Logo</a>
  <!-- itens de menu via documentação Bootstrap -->
</nav>
```

**Utilidades de texto:** `.text-center`, `.text-muted`, `.fw-bold`, `.fst-italic`, `.text-primary`


---

### Bootstrap Avançado — Cards, Modais, Tabelas e Imagens

**Cards:**

```html
<div class="card" style="width: 18rem;">
  <img src="..." class="card-img-top" alt="...">
  <div class="card-body">
    <h5 class="card-title">Título</h5>
    <p class="card-text">Descrição.</p>
    <a href="#" class="btn btn-primary">Ação</a>
  </div>
</div>
```

**Imagens responsivas:**

```html
<img src="..." class="img-fluid" alt="...">         <!-- responsiva -->
<img src="..." class="img-thumbnail" alt="...">     <!-- miniatura com borda -->
<img src="..." class="rounded" alt="...">           <!-- bordas arredondadas -->
```

**Tabelas:**

```html
<table class="table table-striped table-bordered table-hover">
  <thead class="table-dark">...</thead>
  <tbody>...</tbody>
</table>
```

**Modal:**

```html
<!-- Botão disparador -->
<button data-bs-toggle="modal" data-bs-target="#meuModal">Abrir</button>

<!-- Modal -->
<div class="modal fade" id="meuModal">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header"><h5>Título</h5></div>
      <div class="modal-body">Conteúdo</div>
      <div class="modal-footer">
        <button data-bs-dismiss="modal">Fechar</button>
      </div>
    </div>
  </div>
</div>
```


---

## 🚀 GitHub Pages

Hospedagem gratuita para projetos HTML/CSS/JS diretamente de um repositório GitHub.

**Como publicar:**

1. Fazer push do projeto para um repositório público no GitHub
2. Ir em **Settings → Pages**
3. Selecionar branch `main` e pasta `/root`
4. GitHub gera uma URL: `usuario.github.io/repositorio`

> [!TIP] Portfolio Use GitHub Pages para hospedar projetos de portfólio e compartilhar o link com recrutadores.


---

_Última atualização: 17/06/2026_
