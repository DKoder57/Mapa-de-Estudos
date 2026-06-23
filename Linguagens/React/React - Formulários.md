---

tags: [react, formulários, controlled, uncontrolled, validação, useState]

área: React
status: draft

---
# React - Formulários

> [!NOTE] Fonte: _Desenvolvimento de Aplicações Web Modernas com React JS_ — Prof. Lucas Gerken Glória / Descomplica (Módulo 2)

## Controlled vs Uncontrolled Components

||Controlled|Uncontrolled|
|---|---|---|
|**Onde vive o valor**|State do React (`useState`)|DOM (via `ref`)|
|**Como ler o valor**|Diretamente da variável de state|`ref.current.value`|
|**Validação em tempo real**|✅ Fácil|❌ Difícil|
|**Recomendado**|✅ Sim (padrão moderno)|Casos específicos (ex: upload de arquivo)|

> [!TIP] Prefira sempre **controlled components** — o React mantém a fonte de verdade, facilitando validação, formatação e integração com outros estados.

---

## Formulário Simples com `useState`

```jsx
import { useState } from 'react';

const FormularioSimples = () => {
  const [nome, setNome] = useState('');

  const handleSubmit = (e) => {
    e.preventDefault();          // evita recarregar a página
    alert(`Nome enviado: ${nome}`);
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Nome:
        <input
          type="text"
          value={nome}                          // valor controlado pelo state
          onChange={e => setNome(e.target.value)}  // atualiza o state
        />
      </label>
      <button type="submit">Enviar</button>
    </form>
  );
};
```

---

## Múltiplos Campos com um Único State

Em vez de um `useState` por campo, use um objeto — mais escalável:

```jsx
const FormularioCadastro = () => {
  const [formData, setFormData] = useState({
    nome:  '',
    email: '',
    senha: '',
  });

  // Handler genérico — usa o atributo name do input como chave
  const handleChange = (e) => {
    const { name, value } = e.target;
    setFormData(prev => ({ ...prev, [name]: value }));
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log('Dados enviados:', formData);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input
        type="text"
        name="nome"                    // deve coincidir com a chave no state
        value={formData.nome}
        onChange={handleChange}
        placeholder="Nome"
      />
      <input
        type="email"
        name="email"
        value={formData.email}
        onChange={handleChange}
        placeholder="E-mail"
      />
      <input
        type="password"
        name="senha"
        value={formData.senha}
        onChange={handleChange}
        placeholder="Senha"
      />
      <button type="submit">Cadastrar</button>
    </form>
  );
};
```

> [!NOTE] O `name` do input deve ser idêntico à chave no objeto do state. O handler genérico usa `[name]: value` (computed property) para atualizar apenas o campo alterado.

---

## Validação de Formulários

### Validação no `onSubmit`

```jsx
const FormComValidacao = () => {
  const [form, setForm]     = useState({ nome: '', email: '' });
  const [erros, setErros]   = useState({});

  const validar = () => {
    const novosErros = {};
    if (!form.nome.trim())              novosErros.nome  = 'Nome é obrigatório';
    if (!form.email.includes('@'))      novosErros.email = 'E-mail inválido';
    return novosErros;
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    const errosEncontrados = validar();

    if (Object.keys(errosEncontrados).length > 0) {
      setErros(errosEncontrados);
      return;
    }

    setErros({});
    alert('Formulário válido!');
  };

  const handleChange = (e) => {
    const { name, value } = e.target;
    setForm(prev => ({ ...prev, [name]: value }));
    // Limpa o erro do campo ao digitar
    if (erros[name]) setErros(prev => ({ ...prev, [name]: '' }));
  };

  return (
    <form onSubmit={handleSubmit}>
      <div>
        <input
          name="nome"
          value={form.nome}
          onChange={handleChange}
          placeholder="Nome"
        />
        {erros.nome && <span style={{ color: 'red' }}>{erros.nome}</span>}
      </div>

      <div>
        <input
          name="email"
          value={form.email}
          onChange={handleChange}
          placeholder="E-mail"
        />
        {erros.email && <span style={{ color: 'red' }}>{erros.email}</span>}
      </div>

      <button type="submit">Enviar</button>
    </form>
  );
};
```

---

## Tipos de Input

### Select (dropdown)

```jsx
const SelectCor = () => {
  const [cor, setCor] = useState('vermelho');

  return (
    <select value={cor} onChange={e => setCor(e.target.value)}>
      <option value="vermelho">Vermelho</option>
      <option value="azul">Azul</option>
      <option value="verde">Verde</option>
    </select>
  );
};
```

### Checkbox

```jsx
const CheckboxTermos = () => {
  const [aceitou, setAceitou] = useState(false);

  return (
    <label>
      <input
        type="checkbox"
        checked={aceitou}
        onChange={e => setAceitou(e.target.checked)}   // usa .checked, não .value
      />
      Aceito os Termos de Uso
    </label>
  );
};
```

### Múltiplos Checkboxes

```jsx
const FiltrosCategorias = () => {
  const [selecionados, setSelecionados] = useState([]);

  const handleChange = (e) => {
    const { value, checked } = e.target;
    setSelecionados(prev =>
      checked
        ? [...prev, value]
        : prev.filter(item => item !== value)
    );
  };

  return (
    <fieldset>
      {['React', 'Node', 'Python', 'SQL'].map(tech => (
        <label key={tech}>
          <input
            type="checkbox"
            value={tech}
            checked={selecionados.includes(tech)}
            onChange={handleChange}
          />
          {tech}
        </label>
      ))}
      <p>Selecionados: {selecionados.join(', ')}</p>
    </fieldset>
  );
};
```

### Radio Buttons

```jsx
const SeletorGenero = () => {
  const [genero, setGenero] = useState('');

  return (
    <fieldset>
      {['Masculino', 'Feminino', 'Outro'].map(opcao => (
        <label key={opcao}>
          <input
            type="radio"
            value={opcao}
            checked={genero === opcao}
            onChange={e => setGenero(e.target.value)}
          />
          {opcao}
        </label>
      ))}
    </fieldset>
  );
};
```

### Textarea

```jsx
const [mensagem, setMensagem] = useState('');

<textarea
  value={mensagem}
  onChange={e => setMensagem(e.target.value)}
  rows={5}
  placeholder="Sua mensagem..."
/>
```

---

## Formulário Completo — Exemplo Real

```jsx
import { useState } from 'react';

const FormContato = () => {
  const [form, setForm]   = useState({ nome: '', email: '', assunto: 'duvida', mensagem: '', aceito: false });
  const [erros, setErros] = useState({});
  const [enviado, setEnviado] = useState(false);

  const handleChange = (e) => {
    const { name, value, type, checked } = e.target;
    setForm(prev => ({
      ...prev,
      [name]: type === 'checkbox' ? checked : value
    }));
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    const novosErros = {};
    if (!form.nome.trim())     novosErros.nome     = 'Obrigatório';
    if (!form.email.includes('@')) novosErros.email = 'E-mail inválido';
    if (!form.mensagem.trim()) novosErros.mensagem = 'Obrigatório';
    if (!form.aceito)          novosErros.aceito   = 'Aceite os termos';

    if (Object.keys(novosErros).length > 0) {
      setErros(novosErros);
      return;
    }

    console.log('Enviando:', form);
    setEnviado(true);
  };

  if (enviado) return <p>✅ Mensagem enviada com sucesso!</p>;

  return (
    <form onSubmit={handleSubmit}>
      <input  name="nome"     value={form.nome}     onChange={handleChange} placeholder="Nome" />
      {erros.nome     && <span>{erros.nome}</span>}

      <input  name="email"    value={form.email}    onChange={handleChange} placeholder="E-mail" />
      {erros.email    && <span>{erros.email}</span>}

      <select name="assunto"  value={form.assunto}  onChange={handleChange}>
        <option value="duvida">Dúvida</option>
        <option value="suporte">Suporte</option>
        <option value="comercial">Comercial</option>
      </select>

      <textarea name="mensagem" value={form.mensagem} onChange={handleChange} rows={4} />
      {erros.mensagem && <span>{erros.mensagem}</span>}

      <label>
        <input type="checkbox" name="aceito" checked={form.aceito} onChange={handleChange} />
        Aceito os termos
      </label>
      {erros.aceito && <span>{erros.aceito}</span>}

      <button type="submit">Enviar</button>
    </form>
  );
};
```

---

## Padrão: Handler Genérico com Checkbox e Radio

O handler abaixo cobre **todos** os tipos de input em um único lugar:

```jsx
const handleChange = (e) => {
  const { name, value, type, checked } = e.target;
  setForm(prev => ({
    ...prev,
    [name]: type === 'checkbox' ? checked : value
  }));
};
```

---

## Links Relacionados

- [[React - Componentes e Props]]
- [[React - State e Hooks Essenciais]]
- [[React - Eventos e Renderização Condicional]]
- [[React - Requisições HTTP]]