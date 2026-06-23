---
tags: [java, diretrizes, convenções, identificadores, camelcase, sintaxe]
área: Desenvolvimento de Sistemas / Java
status: draft
---

# 📝 Java - Diretrizes de Programação e Convenções

> Fonte: _Introdução à Linguagem de Programação Java_

---

## Regras para Identificadores

Em Java, um **identificador** é o nome utilizado para definir uma variável, um método, uma classe ou uma interface. O compilador impõe regras estritas sobre quais caracteres podem compor um identificador válido.

### Regras de formação:
1. **Caractere inicial:** Deve obrigatoriamente começar com uma **letra**, um caractere de moeda (`$`) ou um caractere de conexão, como o sublinhado (`_`). Identificadores **nunca** podem começar com números.
2. **Caracteres subsequentes:** Após o primeiro caractere, o identificador pode conter qualquer combinação de letras, caracteres monetários, caracteres de conexão ou dígitos numéricos (0-9).
3. **Sensibilidade de caixa (*Case-Sensitive*):** O Java diferencia rigidamente letras maiúsculas de minúsculas. Portanto, `var` e `Var` são tratados como dois identificadores completamente diferentes e independentes.
4. **Palavras reservadas:** Não é permitido a utilização de nenhuma palavra-chave da linguagem Java (como `public`, `static`, `class`, `int`, etc.) como nome de um identificador.

| Exemplo de Código | Validação | Motivo |
| :--- | :---: | :--- |
| `int variavel1 = 10;` | **Válido** | Começa com uma letra e contém número na sequência. |
| `int 4var = 10;` | ❌ **Inválido** | O identificador não pode começar com um dígito numérico. |

---

## Convenções de Nomenclatura (Padrões de Código)

Além das regras obrigatórias do compilador, a comunidade Java adota amplamente convenções de nomenclatura para padronizar o código, facilitando a leitura e a manutenção por diferentes programadores.

O ecossistema Java utiliza primordialmente variações do padrão **camelCase** (onde as palavras internas são destacadas por letras maiúsculas em vez de espaços ou traços):

### 1. Classes e Interfaces
A primeira letra do identificador deve ser obrigatoriamente **maiúscula**. Se o nome for composto por múltiplas palavras vinculadas, a primeira letra de cada uma das palavras internas também deve estar em maiúscula (padrão conhecido como *UpperCamelCase* ou *PascalCase*).
- `HelloWorld`
- `Carro`
- `TesteCarro`

### 2. Métodos
A primeira letra deve ser obrigatoriamente **minúscula**. Caso o nome do método seja composto por mais de uma palavra, as iniciais das palavras subsequentes devem ser grafadas em maiúsculas (*lowerCamelCase*). Geralmente começam com verbos.
- `getBalance`
- `doCalculation`
- `setCustomerName`

### 3. Variáveis
Seguem o mesmo formato dos métodos (*lowerCamelCase*), começando sempre com uma letra **minúscula** e destacando as palavras internas com iniciais maiúsculas. É altamente recomendado o uso de nomes curtos, porém autoexplicativos e significativos.
- `meuCarro`
- `velocidadeMaxima`
- `variavel1`

---

> [!TIP] Legibilidade do código
> Embora o compilador aceite caracteres como `$` e `_` em qualquer parte do identificador, por convenção, o uso do `$` é geralmente evitado na programação do dia a dia, sendo mais utilizado por ferramentas de geração automática de código. Prefira sempre nomes claros e significativos em formato textual.

---

## Links relacionados

- [[Java - Introdução e Plataforma]]
- [[Java - Terminologias Fundamentais]]
- [[Java - Estrutura do Programa e HelloWorld]]