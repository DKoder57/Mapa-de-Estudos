---

tags: [react, hooks, useState, useEffect, useContext, useRef, state]

área: React

status: draft

---
# React - State e Hooks Essenciais

> [!NOTE] Fonte: _Desenvolvimento de Aplicações Web Modernas com React JS_ — Prof. Lucas Gerken Glória / Descomplica (Módulos 1 e 2)

## State vs Props

||Props|State|
|---|---|---|
|**Origem**|Passado pelo pai|Gerenciado internamente|
|**Mutabilidade**|Imutável (filho não altera)|Mutável — atualizado com setter|
|**Quem controla**|Componente pai|O próprio componente|
|**Re-renderização**|Quando o pai re-renderiza|Quando o setter é chamado|

> [!NOTE] Toda vez que o **state** muda, o React automaticamente re-renderiza o componente para refletir o novo valor na UI.

---

## O que são Hooks?

Hooks são **funções especiais** do React que permitem usar recursos como estado e efeitos colaterais dentro de componentes funcionais. Introduzidos no React 16.8.

**Regras obrigatórias dos Hooks:**

- Sempre chamados no **nível raiz** do componente (nunca dentro de `if`, `for` ou funções aninhadas)
- Apenas em **componentes funcionais** ou outros hooks customizados

---

## `useState` — Estado Local

```jsx
import { useState } from 'react';

const [valor, setValor] = useState(valorInicial);
//     ↑             ↑           ↑
//  estado atual   setter    valor inicial (só usado na montagem)
```

### Exemplos

```jsx
// Estado simples: contador
const Contador = () => {
  const [count, setCount] = useState(0);

  return (
    <div>
      <h2>Contador: {count}</h2>
      <button onClick={() => setCount(count + 1)}>+</button>
      <button onClick={() => setCount(count - 1)}>-</button>
      <button onClick={() => setCount(0)}>Reset</button>
    </div>
  );
};
```

### Atualização baseada no valor anterior

Quando a nova state depende do valor atual, use a forma funcional — evita problemas com múltiplas atualizações assíncronas:

```jsx
// ⚠️ Pode ter problema se setCount for chamado várias vezes seguidas
setCount(count + 1);

// ✅ Forma correta — sempre recebe o valor mais recente
setCount(prevCount => prevCount + 1);
```

### State com objetos

```jsx
const [usuario, setUsuario] = useState({ nome: '', email: '' });

// ⚠️ ERRADO — substitui o objeto inteiro
setUsuario({ nome: 'Danilo' });

// ✅ CORRETO — spread para preservar os demais campos
setUsuario(prev => ({ ...prev, nome: 'Danilo' }));
```

### State com arrays

```jsx
const [itens, setItens] = useState([]);

// Adicionar
setItens(prev => [...prev, novoItem]);

// Remover por índice
setItens(prev => prev.filter((_, i) => i !== indexParaRemover));

// Atualizar item específico
setItens(prev => prev.map((item, i) => i === index ? novoValor : item));
```

---

## `useEffect` — Efeitos Colaterais

Executa código após a renderização. Usado para: chamadas de API, timers, manipulação do DOM, assinaturas (subscriptions).

```jsx
import { useEffect } from 'react';

useEffect(() => {
  // código do efeito
  return () => {
    // cleanup (opcional) — executado antes do próximo efeito ou na desmontagem
  };
}, [dependencias]);
```

### Variações pelo array de dependências

```jsx
// 1. Sem array — executa após CADA renderização
useEffect(() => {
  console.log('renderizou');
});

// 2. Array vazio — executa apenas na MONTAGEM (equivale a componentDidMount)
useEffect(() => {
  console.log('montou uma vez');
}, []);

// 3. Com dependências — executa quando alguma dependência mudar
useEffect(() => {
  document.title = `Contador: ${count}`;
}, [count]);                              // roda quando count muda

// 4. Com cleanup — ex: cancelar timer na desmontagem
useEffect(() => {
  const timer = setInterval(() => {
    setCount(c => c + 1);
  }, 1000);

  return () => clearInterval(timer);   // cleanup
}, []);
```

### Busca de dados com useEffect

```jsx
const ListaUsuarios = () => {
  const [usuarios, setUsuarios] = useState([]);
  const [loading, setLoading]   = useState(true);
  const [erro, setErro]         = useState(null);

  useEffect(() => {
    fetch('https://jsonplaceholder.typicode.com/users')
      .then(res => {
        if (!res.ok) throw new Error('Erro na requisição');
        return res.json();
      })
      .then(data => {
        setUsuarios(data);
        setLoading(false);
      })
      .catch(err => {
        setErro(err.message);
        setLoading(false);
      });
  }, []);   // array vazio — busca apenas na montagem

  if (loading) return <p>Carregando...</p>;
  if (erro)    return <p>Erro: {erro}</p>;

  return (
    <ul>
      {usuarios.map(u => <li key={u.id}>{u.name}</li>)}
    </ul>
  );
};
```

---

## `useContext` — Estado Global sem Prop Drilling

Permite compartilhar dados entre componentes distantes na árvore sem passar props manualmente em cada nível.

```jsx
import { createContext, useContext, useState } from 'react';

// 1. Criar o contexto
const TemaContext = createContext();

// 2. Criar o Provider (envolve os componentes que precisam do contexto)
const TemaProvider = ({ children }) => {
  const [tema, setTema] = useState('claro');

  const alternarTema = () => setTema(t => t === 'claro' ? 'escuro' : 'claro');

  return (
    <TemaContext.Provider value={{ tema, alternarTema }}>
      {children}
    </TemaContext.Provider>
  );
};

// 3. Consumir o contexto em qualquer componente filho (qualquer nível)
const BotaoTema = () => {
  const { tema, alternarTema } = useContext(TemaContext);

  return (
    <div style={{
      background: tema === 'claro' ? '#fff' : '#333',
      color:      tema === 'claro' ? '#000' : '#fff',
      padding: '20px'
    }}>
      <p>Tema atual: {tema}</p>
      <button onClick={alternarTema}>Alternar Tema</button>
    </div>
  );
};

// 4. Envolver o App com o Provider
const App = () => (
  <TemaProvider>
    <BotaoTema />
  </TemaProvider>
);
```

> [!TIP] Context é ótimo para dados globais estáveis (tema, idioma, autenticação). Evite para estados altamente dinâmicos (inputs em tempo real) — pode causar re-renderizações excessivas.

---

## `useRef` — Referência Sem Re-renderização

`useRef` cria um objeto `{ current: valor }` que persiste entre renderizações **sem causar re-renderização** ao ser alterado.

Dois usos principais:

### 1. Acessar elementos do DOM diretamente

```jsx
import { useRef, useEffect } from 'react';

const AutoFocusInput = () => {
  const inputRef = useRef(null);

  useEffect(() => {
    inputRef.current.focus();   // acessa o elemento DOM diretamente
  }, []);

  return <input ref={inputRef} type="text" placeholder="foco automático" />;
};
```

### 2. Armazenar valor mutável sem disparar re-render

```jsx
const Cronometro = () => {
  const [segundos, setSegundos] = useState(0);
  const timerRef = useRef(null);   // guarda o ID do intervalo

  const iniciar = () => {
    timerRef.current = setInterval(() => {
      setSegundos(s => s + 1);
    }, 1000);
  };

  const parar = () => {
    clearInterval(timerRef.current);
  };

  return (
    <div>
      <p>{segundos}s</p>
      <button onClick={iniciar}>Iniciar</button>
      <button onClick={parar}>Parar</button>
    </div>
  );
};
```

---

## `useReducer` — Estado Complexo

Alternativa ao `useState` para estados com múltiplas ações ou lógica de transição mais elaborada. Segue o mesmo padrão do Redux.

```jsx
import { useReducer } from 'react';

const reducer = (state, action) => {
  switch (action.type) {
    case 'incrementar':  return { count: state.count + 1 };
    case 'decrementar':  return { count: state.count - 1 };
    case 'resetar':      return { count: 0 };
    default:             return state;
  }
};

const Contador = () => {
  const [state, dispatch] = useReducer(reducer, { count: 0 });

  return (
    <div>
      <h2>Contador: {state.count}</h2>
      <button onClick={() => dispatch({ type: 'incrementar' })}>+</button>
      <button onClick={() => dispatch({ type: 'decrementar' })}>-</button>
      <button onClick={() => dispatch({ type: 'resetar' })}>Reset</button>
    </div>
  );
};
```

---

## Resumo dos Hooks Essenciais

|Hook|Para que serve|Re-renderiza?|
|---|---|---|
|`useState`|Estado local simples|Sim, ao chamar o setter|
|`useEffect`|Efeitos colaterais (API, DOM, timers)|Não diretamente|
|`useContext`|Consumir contexto global|Sim, quando o contexto muda|
|`useRef`|Referência DOM ou valor persistente|**Não**|
|`useReducer`|Estado complexo com múltiplas ações|Sim, ao chamar dispatch|
|`useMemo`|Memorizar valor calculado|Não — apenas recalcula quando deps mudam|
|`useCallback`|Memorizar função|Não — apenas recria quando deps mudam|

---

## Links Relacionados

- [[React - Componentes e Props]]
- [[React - Eventos e Renderização Condicional]]
- [[React - Ciclo de Vida]]
- [[React - Gerenciamento de Estado]]
- [[React - Performance e Deploy]]