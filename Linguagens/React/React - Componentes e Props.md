---
tags: [react, componentes, props, functional, class-component]

área: React

status: draft

---
> [!NOTE] Fonte: _Desenvolvimento de Aplicações Web Modernas com React JS_ — Prof. Lucas Gerken Glória / Descomplica (Módulo 1)

## O que são Componentes?

Componentes são os **blocos de construção** de uma aplicação React. Cada elemento visível na interface é (ou deve ser) um componente — um botão, um card, um menu, uma página inteira.

Vantagens da componentização:

- **Reutilização** — escreva uma vez, use em qualquer lugar
- **Encapsulamento** — lógica e estilo isolados, sem vazamento entre componentes
- **Manutenção** — alterar um componente não quebra os outros

---

## Tipos de Componentes

### Componente Funcional (Stateless / Function Component)

A forma moderna e padrão. É uma função JavaScript que retorna JSX.

```jsx
// Declaração com arrow function (estilo moderno)
const UserCard = (props) => {
  return (
    <div style={{ border: '1px solid #ccc', padding: '10px' }}>
      <h2>{props.nome}</h2>
      <p>Idade: {props.idade}</p>
    </div>
  );
};

export default UserCard;
```

Com **desestruturação de props** (mais limpo):

```jsx
const UserCard = ({ nome, idade }) => {
  return (
    <div style={{ border: '1px solid #ccc', padding: '10px' }}>
      <h2>{nome}</h2>
      <p>Idade: {idade}</p>
    </div>
  );
};
```

---

### Componente de Classe (Class Component)

Forma legada — existia antes dos Hooks. Herda de `React.Component` e obrigatoriamente implementa `render()`.

```jsx
import React, { Component } from 'react';

class UserCard extends Component {
  render() {
    return (
      <div style={{ border: '1px solid #ccc', padding: '10px' }}>
        <h2>{this.props.nome}</h2>   {/* acessa via this.props */}
        <p>Idade: {this.props.idade}</p>
      </div>
    );
  }
}

export default UserCard;
```

> [!NOTE] Em projetos modernos, prefira sempre componentes funcionais. Class components ainda funcionam, mas não recebem novos recursos do React.

---

### Comparação

|Característica|Funcional|Classe|
|---|---|---|
|Sintaxe|Função JS|Classe que extends Component|
|Acesso a props|Parâmetro `props`|`this.props`|
|Estado|`useState` hook|`this.state` / `this.setState`|
|Hooks|✅ Suporta|❌ Não suporta|
|Performance|Ligeiramente melhor|Ligeiramente mais pesada|
|Uso atual|✅ Padrão recomendado|⚠️ Legado|

---

## Props

**Props** (abreviação de _properties_) são dados passados de um componente **pai** para um componente **filho**. São a principal forma de comunicação entre componentes.

### Características das Props

|Propriedade|Descrição|
|---|---|
|**Imutáveis**|O filho nunca modifica suas próprias props|
|**Unidirecionais**|Sempre fluem de pai → filho|
|**Qualquer tipo**|String, número, objeto, array, função, JSX|

### Passando e Recebendo Props

```jsx
// Componente filho
const Saudacao = ({ nome, sobrenome, idade }) => {
  return (
    <p>
      Olá, {nome} {sobrenome}! Você tem {idade} anos.
    </p>
  );
};

// Componente pai — passa as props como atributos JSX
const App = () => {
  return (
    <div>
      <Saudacao nome="Danilo" sobrenome="Koder" idade={23} />
      <Saudacao nome="Maria" sobrenome="Silva" idade={30} />
    </div>
  );
};
```

> [!TIP] Strings usam aspas duplas (`nome="João"`). Outros tipos (número, booleano, objeto, expressão) usam chaves (`idade={25}`, `ativo={true}`, `dados={objeto}`).

---

### Props com Valores Padrão

```jsx
const Botao = ({ texto = "Clique aqui", cor = "blue" }) => {
  return (
    <button style={{ backgroundColor: cor }}>
      {texto}
    </button>
  );
};

// Uso sem passar props — usa os padrões
<Botao />

// Uso sobrescrevendo
<Botao texto="Enviar" cor="green" />
```

---

### Passando Funções como Props

É assim que componentes filhos "comunicam" algo ao pai:

```jsx
const BotaoExcluir = ({ onExcluir, id }) => {
  return (
    <button onClick={() => onExcluir(id)}>
      Excluir
    </button>
  );
};

const App = () => {
  const handleExcluir = (id) => {
    console.log(`Excluindo item ${id}`);
  };

  return <BotaoExcluir id={42} onExcluir={handleExcluir} />;
};
```

---

### `children` — Conteúdo Interno

A prop especial `children` representa o conteúdo passado **dentro** das tags do componente:

```jsx
const Card = ({ titulo, children }) => {
  return (
    <div className="card">
      <h3>{titulo}</h3>
      <div className="card-body">
        {children}   {/* renderiza o que foi passado dentro das tags */}
      </div>
    </div>
  );
};

// Uso
<Card titulo="Meu Card">
  <p>Qualquer conteúdo aqui vira children</p>
  <button>Ação</button>
</Card>
```

---

## Composição de Componentes

A composição é o padrão central do React — construir UIs complexas combinando componentes simples:

```jsx
// Componentes atômicos
const Avatar = ({ src, alt }) => <img src={src} alt={alt} className="avatar" />;
const Nome   = ({ nome })     => <h2>{nome}</h2>;
const Bio    = ({ texto })    => <p>{texto}</p>;

// Componente composto
const ProfileCard = ({ usuario }) => {
  return (
    <div className="profile-card">
      <Avatar src={usuario.foto}  alt={usuario.nome} />
      <Nome   nome={usuario.nome} />
      <Bio    texto={usuario.bio} />
    </div>
  );
};

// Uso
const App = () => {
  const usuario = {
    nome: "Danilo",
    foto: "/avatar.png",
    bio: "Desenvolvedor fullstack estudando ADS."
  };

  return <ProfileCard usuario={usuario} />;
};
```

---

## Exportação e Importação

```jsx
// Exportação padrão (default) — um por arquivo
export default UserCard;

// Exportação nomeada — múltiplas por arquivo
export const Botao = () => { ... };
export const Input = () => { ... };

// Importando default
import UserCard from './UserCard';

// Importando nomeado
import { Botao, Input } from './components';
```

> [!TIP] Por convenção, cada componente fica em seu próprio arquivo com o mesmo nome. Ex: `UserCard.jsx` exporta `UserCard`.

---

## Links Relacionados

- [[React - Fundamentos e JSX]]
- [[React - State e Hooks Essenciais]]
- [[React - Eventos e Renderização Condicional]]
- [[React - Formulários]]