---

tags: [react, eventos, renderização-condicional, listas, keys]
área: React
status: draft

---
# React - Eventos e Renderização Condicional

> [!NOTE] Fonte: _Desenvolvimento de Aplicações Web Modernas com React JS_ — Prof. Lucas Gerken Glória / Descomplica (Módulo 2)

## Eventos no React

O React usa um sistema de **eventos sintéticos** — um wrapper sobre os eventos nativos do browser que garante comportamento consistente entre plataformas.

### Diferenças em relação ao HTML puro

||HTML puro|React|
|---|---|---|
|Sintaxe|`onclick="handler()"` — string|`onClick={handler}` — função|
|Nomenclatura|lowercase (`onclick`)|camelCase (`onClick`)|
|Passagem|String|Referência de função|

```jsx
// HTML puro
<button onclick="alert('clicou')">Clique</button>

// React
const handleClick = () => alert('clicou');
<button onClick={handleClick}>Clique</button>

// Ou inline (para lógica simples)
<button onClick={() => alert('clicou')}>Clique</button>
```

---

## Eventos Comuns

|Evento|Quando dispara|
|---|---|
|`onClick`|Clique do mouse|
|`onChange`|Mudança de valor em input|
|`onSubmit`|Envio de formulário|
|`onMouseOver`|Mouse passa sobre o elemento|
|`onMouseOut`|Mouse sai do elemento|
|`onKeyDown`|Tecla pressionada|
|`onKeyUp`|Tecla solta|
|`onFocus`|Elemento ganha foco|
|`onBlur`|Elemento perde foco|

---

## O Objeto de Evento (`e`)

Todo handler de evento recebe automaticamente o objeto de evento sintético:

```jsx
const Input = () => {
  const handleChange = (e) => {
    console.log(e.target.value);      // valor atual do input
    console.log(e.target.name);       // atributo name do input
    console.log(e.target.type);       // tipo do input
  };

  const handleSubmit = (e) => {
    e.preventDefault();   // evita o recarregamento da página
    console.log('form enviado');
  };

  return (
    <form onSubmit={handleSubmit}>
      <input name="email" onChange={handleChange} />
      <button type="submit">Enviar</button>
    </form>
  );
};
```

---

## Passando Parâmetros para Eventos

```jsx
const handleExcluir = (id) => {
  console.log(`Excluindo id: ${id}`);
};

// ✅ Arrow function no JSX para passar parâmetro
<button onClick={() => handleExcluir(42)}>Excluir</button>

// ⚠️ ERRADO — executa imediatamente (na renderização, não no clique)
<button onClick={handleExcluir(42)}>Errado</button>
```

---

## Renderização Condicional

Exibir diferentes elementos com base em condições — login/logout, loading, erros, permissões.

### 1. `if-else` (fora do JSX)

```jsx
const UserStatus = ({ isLoggedIn }) => {
  if (isLoggedIn) {
    return <h2>Bem-vindo de volta!</h2>;
  } else {
    return <h2>Por favor, faça login.</h2>;
  }
};
```

### 2. Operador Ternário (inline no JSX)

```jsx
const UserStatus = ({ isLoggedIn }) => {
  return (
    <div>
      <h2>{isLoggedIn ? 'Bem-vindo!' : 'Faça login'}</h2>
      <button onClick={toggleLogin}>
        {isLoggedIn ? 'Logout' : 'Login'}
      </button>
    </div>
  );
};
```

### 3. Operador `&&` (exibir ou nada)

Ideal para exibir algo opcionalmente — se a condição for `false`, nada é renderizado:

```jsx
const Notificacao = ({ hasNotification, count }) => {
  return (
    <div>
      <h2>Dashboard</h2>
      {hasNotification && <p>Você tem {count} notificações!</p>}
    </div>
  );
};
```

> [!NOTE] Cuidado com `0 && <Componente />` — o React renderiza o número `0` em vez de nada. Prefira `count > 0 && <Componente />` ou o ternário.

### 4. Função auxiliar de render

Para condições complexas ou múltiplos branches, extraia para uma função:

```jsx
const Conteudo = ({ status }) => {
  const renderConteudo = () => {
    if (status === 'loading') return <Spinner />;
    if (status === 'error')   return <MensagemErro />;
    if (status === 'empty')   return <EstadoVazio />;
    return <ListaDados />;
  };

  return <div>{renderConteudo()}</div>;
};
```

---

## Listas e Keys

### Renderizando listas com `.map()`

```jsx
const frutas = ['Maçã', 'Banana', 'Laranja'];

const ListaFrutas = () => {
  return (
    <ul>
      {frutas.map((fruta, index) => (
        <li key={index}>{fruta}</li>
      ))}
    </ul>
  );
};
```

### A importância das `key`

A prop `key` é usada pelo React para identificar qual item mudou, foi adicionado ou removido — otimiza a re-renderização.

```jsx
const usuarios = [
  { id: 1, nome: 'Danilo' },
  { id: 2, nome: 'Ana' },
  { id: 3, nome: 'João' },
];

const ListaUsuarios = () => {
  return (
    <ul>
      {usuarios.map(usuario => (
        <li key={usuario.id}>{usuario.nome}</li>   // ✅ key única e estável
      ))}
    </ul>
  );
};
```

> [!TIP] Use sempre um **ID único** como key quando disponível. Evite usar o índice do array em listas que podem ser reordenadas — causa bugs de reconciliação.

### Renderizando listas com componentes

```jsx
const ItemUsuario = ({ nome, email }) => (
  <li>
    <strong>{nome}</strong> — {email}
  </li>
);

const ListaUsuarios = ({ usuarios }) => (
  <ul>
    {usuarios.map(u => (
      <ItemUsuario key={u.id} nome={u.nome} email={u.email} />
    ))}
  </ul>
);
```

> [!NOTE] A `key` fica no componente externo (no `.map()`), não dentro do componente `ItemUsuario`.

---

## Lista Dinâmica — Adicionar e Remover

```jsx
import { useState } from 'react';

const ListaDinamica = () => {
  const [itens, setItens] = useState(['Item 1', 'Item 2']);
  const [novo, setNovo]   = useState('');

  const adicionar = () => {
    if (novo.trim() === '') return;
    setItens(prev => [...prev, novo]);
    setNovo('');
  };

  const remover = (index) => {
    setItens(prev => prev.filter((_, i) => i !== index));
  };

  return (
    <div>
      <input
        value={novo}
        onChange={e => setNovo(e.target.value)}
        placeholder="Novo item"
      />
      <button onClick={adicionar}>Adicionar</button>

      <ul>
        {itens.map((item, index) => (
          <li key={index}>
            {item}
            <button onClick={() => remover(index)}>✕</button>
          </li>
        ))}
      </ul>
    </div>
  );
};
```

---

## Padrões Combinados: Evento + State + Condicional

```jsx
const LoginToggle = () => {
  const [isLoggedIn, setIsLoggedIn] = useState(false);
  const [loading, setLoading]       = useState(false);

  const handleLogin = async () => {
    setLoading(true);
    await new Promise(r => setTimeout(r, 1000));   // simula requisição
    setIsLoggedIn(true);
    setLoading(false);
  };

  if (loading) return <p>Autenticando...</p>;

  return (
    <div>
      {isLoggedIn
        ? <p>✅ Logado! <button onClick={() => setIsLoggedIn(false)}>Sair</button></p>
        : <button onClick={handleLogin}>Entrar</button>
      }
    </div>
  );
};
```

---

## Links Relacionados

- [[React - Componentes e Props]]
- [[React - State e Hooks Essenciais]]
- [[React - Formulários]]
- [[React - Ciclo de Vida]]