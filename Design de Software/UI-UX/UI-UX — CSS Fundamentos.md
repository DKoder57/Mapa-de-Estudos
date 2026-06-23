---

tags: [ui-ux, css, desenvolvimento, web, estilização]

área: UI/UX

status: draft
---
# CSS — Fundamentos

[[UI-UX]] → Módulo 4 

## O que é CSS

**Cascading Style Sheets** — linguagem para estilizar e aprimorar a apresentação de documentos HTML.

### Formas de Incluir CSS

|Forma|Como|Recomendação|
|---|---|---|
|**Inline**|`<p style="color:red">`|Apenas para ajustes pontuais|
|**Interno**|`<style>` no `<head>`|Projetos pequenos|
|**Externo**|Arquivo `.css` separado via `<link>`|✅ Recomendado — separa responsabilidades|

```html
<!-- Vinculando CSS externo -->
<link rel="stylesheet" href="css/styles.css" />
```

---

## Seletores: Classes e IDs

```css
/* Classe — reutilizável, múltiplos elementos */
.paragrafo-especial {
  color: black;
  background-color: salmon;
}

/* ID — único por página */
#titulo-especial {
  background-color: aqua;
  font-size: 10px;
}
```

```html
<p class="paragrafo-especial">Texto</p>
<h1 id="titulo-especial">Título</h1>
```

> [!NOTE] ID vs Classe IDs devem ser únicos na página — duplicidade funciona no CSS mas causa erros no JavaScript.

---

## Cores em CSS

|Formato|Exemplo|Notas|
|---|---|---|
|**Nome**|`color: brown`|Limitado|
|**Hexadecimal**|`color: #4144fc`|Mais usado; `#FFFFFF` = `#FFF`|
|**RGB**|`color: rgb(255, 0, 0)`|0–255 por canal|
|**RGBA**|`color: rgba(255, 0, 0, 0.5)`|+ canal alpha (transparência 0–1)|
|**HSL**|`color: hsl(120, 30%, 70%)`|Matiz, saturação, brilho|

> [!TIP] Hexadecimal `#000` = preto, `#FFF` = branco. Forma curta: `#112233` = `#123`

---

## Box Model

Todo elemento HTML é uma caixa com 5 camadas:

```
margin (espaço externo)
  border (borda)
    padding (espaço interno)
      content area (conteúdo)
        height / width
```

```css
.elemento {
  width: 400px;
  height: 200px;
  padding: 40px 80px;        /* top/bottom = 40, left/right = 80 */
  margin: 10px 20px 30px 40px; /* top right bottom left */
  box-sizing: border-box;    /* inclui padding e border no width total */
}
```

---

## Propriedade Display

|Valor|Comportamento|
|---|---|
|`block`|Ocupa toda a largura; quebra de linha antes e depois|
|`inline`|Ocupa apenas o espaço necessário; sem quebra de linha|
|`inline-block`|Mesmo que inline, mas aceita width/height|
|`none`|Elemento não é exibido|
|`flex`|Container flexível (Flexbox)|
|`grid`|Container de grade (CSS Grid)|

> [!NOTE] No projeto `display: flex` com `flex-wrap: wrap` foi usado nas seções Features e Testimonials para posicionar elementos lado a lado com responsividade.

---

## Posição (position)

|Valor|Comportamento|
|---|---|
|`static`|Padrão; `top/right/bottom/left` não funcionam|
|`relative`|Relativo ao fluxo do HTML; pode usar `top/left` etc.|
|`absolute`|Quebra o fluxo; posicionado em qualquer ponto da tela|

> [!TIP] No projeto `position: absolute` + `relative` foram usados para fixar o botão do WhatsApp na tela independente da rolagem.

---

## Imagens de Fundo

```css
.secao-hero {
  background-image: url("img/fundo.jpg");
  background-position: center;
  background-size: cover;
  background-repeat: no-repeat;
}
```

---

## Responsividade

Abordada nas videoaulas 31–32 com:

- Unidades relativas (`%`, `vw`, `vh`)
- Flexbox e CSS Grid
- **Media Queries** e breakpoints
- Frameworks Bootstrap e Tailwind

```css
@media (max-width: 768px) {
  .container {
    flex-direction: column;
  }
}
```

_Fonte: Fundamentos de Interfaces — Prof. Dálton Reis Leal (Projeto Desenvolve)_