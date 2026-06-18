---

tags: [ui-ux, html, desenvolvimento, web]

área: UI/UX

status: draft
---
# HTML — Fundamentos

[[UI-UX]] → Módulo 4 

## O que é HTML

**HyperText Markup Language** — base para a criação de qualquer página na web. Organiza e estrutura conteúdo por meio de **tags**.

Tags: `<nome>conteúdo</nome>` | Self-closing: `<br/>`, `<hr/>`, `<img/>`

---

## Estrutura Básica

```html
<!DOCTYPE html>
<html lang="pt-BR">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Título da Aba</title>
  </head>
  <body>
    Conteúdo
  </body>
</html>
```

> [!TIP] Atalho no VSCode Digite `!` + TAB para gerar a estrutura básica automaticamente.

---

## Tags Essenciais

|Tag|Uso|
|---|---|
|`<h1>` a `<h6>`|Títulos (hierarquia semântica — h1 é o maior)|
|`<p>`|Parágrafo|
|`<br/>`|Quebra de linha (self-closing)|
|`<hr/>`|Linha horizontal (self-closing)|
|`<!-- -->`|Comentário (não aparece na página)|
|`<a href="url">`|Link; `target="_blank"` abre em nova aba|
|`<img src="caminho" alt="descrição"/>`|Imagem; `alt` é fundamental para acessibilidade|
|`<div>`|Container genérico para agrupar elementos|
|`<span>`|Container inline|

---

## Listas

```html
<!-- Não ordenada (ul) -->
<ul>
  <li>Item 1</li>
  <li>Item 2</li>
</ul>

<!-- Ordenada (ol) -->
<ol>
  <li>Passo 1</li>
  <li>Passo 2</li>
</ol>
```

> [!NOTE] No projeto Landing Page Listas `<ul>` foram usadas para montar o menu de navegação e, via CSS, dispostas horizontalmente.

---

## Tabelas

```html
<table>
  <tr>
    <th>Título C1</th>
    <th>Título C2</th>
  </tr>
  <tr>
    <td>L1C1</td>
    <td>L1C2</td>
  </tr>
</table>
```

- `<table>` — container da tabela
- `<tr>` — table row (linha)
- `<th>` — table header (cabeçalho)
- `<td>` — table data (célula)

---

## Divisões com `<div>`

```html
<div>
  <h2>Título da Seção 1</h2>
  <p>Conteúdo da seção 1</p>
</div>
```

`<div>` encapsula elementos, organiza o layout e permite aplicar estilos específicos via CSS. Amplamente usada em estruturas como seções hero, features e testimonials.

---

## Ferramentas e Práticas

**Live Server** (extensão VSCode) — serve o HTML com recarregamento automático ao salvar. Para instalar: ícone de apps → buscar "Live Server" → Install → clicar com botão direito no arquivo → "Open with Live Server"

---

## HTML Semântico

Tags como `<header>`, `<nav>`, `<main>`, `<footer>`, `<section>` dão significado estrutural à página, melhorando acessibilidade e SEO.

_Fonte: Fundamentos de Interfaces — Prof. Dálton Reis Leal (Projeto Desenvolve)_