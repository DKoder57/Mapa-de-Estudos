---
tags: [react, jsx, virtual-dom, fundamentos, componentes]

área: React

status: draft

---
# React - Fundamentos e JSX

> [!NOTE] Fonte: _Desenvolvimento de Aplicações Web Modernas com React JS_ — Prof. Lucas Gerken Glória / Descomplica (Módulo 1)

## O que é React?

React.js é uma **biblioteca JavaScript** criada pelo Facebook (Meta) em 2013 para construir interfaces de usuário dinâmicas e interativas. Diferente de frameworks como Angular ou Vue, o React foca exclusivamente na **camada de interface (UI)** — como os elementos são exibidos e como reagem ao usuário.

É usado por Facebook, Instagram, Netflix e inúmeras outras empresas.

---

## Problemas que o React resolve

### Problema 1 — Atualização manual da interface

Antes do React, quando um usuário interagia com a página (ex: adicionar item ao carrinho), o desenvolvedor precisava manipular o DOM manualmente para refletir a mudança — código verboso e propenso a bugs.

### Problema 2 — Código desorganizado

Com o crescimento da aplicação, funções interligadas para manipular a interface tornavam o código difícil de manter e depurar.

### Solução do React

Dois mecanismos centrais:

|Mecanismo|O que faz|
|---|---|
|**Componentes**|Dividem a UI em partes independentes e reutilizáveis|
|**Virtual DOM**|Cópia virtual da interface — o React compara e atualiza **somente** o que mudou, sem recarregar a página|

---

## Virtual DOM — Como funciona

```
Estado muda
    ↓
React gera novo Virtual DOM
    ↓
Compara com o Virtual DOM anterior (diffing)
    ↓
Aplica apenas as diferenças no DOM real (reconciliation)
```

> [!TIP] O Virtual DOM é o principal responsável pela performance do React. Em vez de redesenhar a página inteira, ele cirurgia os mínimos necessários.

---

## JSX — JavaScript + XML

JSX é uma extensão de sintaxe que permite escrever estrutura HTML dentro do JavaScript. É transformado em chamadas `React.createElement()` pelo compilador (Babel/Vite).

```jsx
// JSX
const elemento = <h1 className="titulo">Olá, mundo!</h1>;

// O que o compilador gera por baixo
const elemento = React.createElement('h1', { className: 'titulo' }, 'Olá, mundo!');
```

### Regras do JSX

```jsx
// 1. Um único elemento raiz (ou Fragment)
return (
  <div>           {/* raiz única */}
    <h1>Título</h1>
    <p>Parágrafo</p>
  </div>
);

// Ou usando Fragment (sem nó extra no DOM)
return (
  <>
    <h1>Título</h1>
    <p>Parágrafo</p>
  </>
);

// 2. Expressões JavaScript com chaves {}
const nome = "Danilo";
return <p>Olá, {nome}!</p>;
return <p>Soma: {2 + 2}</p>;
return <img src={usuario.avatar} />;

// 3. className no lugar de class (class é palavra reservada em JS)
return <div className="container">...</div>;

// 4. Tags devem ser fechadas (incluindo self-closing)
return <input type="text" />;   // ✓
return <br />;                  // ✓
```

---

## Ambiente de Desenvolvimento

### Pré-requisitos

- **VS Code** — editor recomendado
- **Node.js LTS** — runtime JS (inclui npm)

### Extensões úteis no VS Code

- ES7+ React/Redux/React-Native snippets — atalhos para criar componentes
- Prettier — formatação automática
- React Developer Tools (extensão do browser) — debug

### Verificando instalação

```bash
node -v    # ex: v20.11.0
npm -v     # ex: 10.2.4
```

---

## Criando o Primeiro Projeto

```bash
# Criar projeto com Vite (recomendado — mais rápido que CRA)
npm create vite@latest meu-app -- --template react
cd meu-app
npm install
npm run dev

# Alternativa clássica (Create React App — mais lento)
npx create-react-app meu-app
cd meu-app
npm start
```

### Estrutura de pastas gerada

```
meu-app/
├── node_modules/     # dependências instaladas (não versionar)
├── public/           # arquivos estáticos (favicon, index.html)
├── src/              # todo o código da aplicação
│   ├── App.jsx       # componente raiz
│   ├── main.jsx      # ponto de entrada — monta o React no DOM
│   └── index.css
├── package.json      # dependências e scripts
└── vite.config.js    # configuração do bundler
```

### O ponto de entrada

```jsx
// src/main.jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```

> [!NOTE] `React.StrictMode` ativa verificações extras em desenvolvimento (sem impacto em produção). Ele pode renderizar componentes duas vezes de propósito para detectar efeitos colaterais impuros.

---

## O que é um Componente (visão geral)

Tudo que é visível na tela é um componente. A UI é uma árvore de componentes:

```
App
├── Header
│   └── Navbar
├── Main
│   ├── ProductCard
│   └── ProductCard
└── Footer
```

Cada componente:

- É uma função (ou classe) JavaScript
- Retorna JSX
- Pode receber dados (props)
- Pode ter estado interno (state)

> [!TIP] Componentes por convenção começam com **letra maiúscula** — assim o React distingue `<div>` (elemento HTML) de `<Div>` (componente customizado).

---

## Links Relacionados

- [[React - Componentes e Props]]
- [[React - State e Hooks Essenciais]]
- [[React - Ciclo de Vida]]