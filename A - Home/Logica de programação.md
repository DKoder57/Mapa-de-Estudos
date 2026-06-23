---
tags:
  - fundamentos
  - scratch
  - no-code
  - introducao
---

# 🟢 Fundamentos

> [!note] Sobre esta seção Conteúdos introdutórios de lógica e ferramentas visuais. Resumos compactos — sem aprofundamento técnico.

---

## 🐱 Scratch — Lógica de Programação Visual

**Scratch** é uma linguagem de programação visual criada pelo MIT. Funciona com base em **atores** (sprites) que recebem blocos de comandos arrastáveis, sem necessidade de digitar código. É uma porta de entrada para os conceitos fundamentais da programação.

> [!tip] Conceito central Um **algoritmo** é uma sequência definida de instruções para resolver um problema. No Scratch, os blocos empilhados formam o algoritmo.

---

### Variáveis

Variáveis armazenam valores na memória durante a execução do programa. Os tipos básicos são números inteiros, decimais, palavras (strings) e booleanos (verdadeiro/falso).

No Scratch há dois tipos: **variáveis do usuário** (criadas manualmente na seção Variáveis) e **variáveis internas** do programa, como `resposta` e `cronômetro`, acessíveis pela seção Sensores.

**Declaração** = dar nome à variável e associar um tipo. **Definição** = atribuir um valor a ela.

---

### Operadores

|Tipo|Operadores|Descrição|
|---|---|---|
|Aritméticos|`+ - * /`|Operações matemáticas|
|Relacionais|`< = >`|Comparação entre valores, retorna verdadeiro/falso|
|Lógicos|`e` `ou` `não`|Combinação de expressões booleanas|

> [!note] Tabela verdade resumida `e` → verdadeiro só se **ambos** forem verdadeiros `ou` → verdadeiro se **pelo menos um** for verdadeiro `não` → **inverte** o resultado da expressão

---

### Estruturas Condicionais

Controlam quais blocos de código são executados com base em uma condição.

**Se...** — executa o bloco somente se a condição for verdadeira. **Se... Senão...** — executa um bloco para verdadeiro e outro para falso. **Senão se...** — encadeia múltiplas condições antes do caso padrão. No Scratch é montado empilhando estruturas `se/senão` uma dentro da outra.

---

### Estruturas de Repetição

|Estrutura|Comportamento|
|---|---|
|`sempre`|Repete o bloco indefinidamente|
|`repita N vezes`|Repete um número fixo de vezes|
|`repita até que...`|Repete enquanto a condição for **falsa**; para quando se torna verdadeira|

> [!warning] Cuidado com loops infinitos No `repita até que`, garanta que a condição de parada seja atingida dentro do bloco, ou a repetição nunca termina.

---

### Listas e Iteradores

Uma **lista** agrupa múltiplas variáveis em uma única estrutura, acessadas pelo índice. Uma variável usada para percorrer os índices de uma lista é chamada de **iterador** — normalmente incrementada de 1 a cada ciclo de repetição.

Uso comum: percorrer todos os elementos de uma lista com `repita N vezes` ou `repita até que` para somar, comparar ou processar valores.

---

### Condições de Tempo

O Scratch oferece duas formas de controle temporal:

- `espere N seg` — pausa a execução por um tempo fixo (execução sequencial)
- `cronômetro` — variável interna que conta os segundos desde o início do programa; usada como condição em estruturas de repetição sem pausar a execução

---

### De Scratch para linguagens reais

Os conceitos do Scratch mapeiam diretamente para qualquer linguagem. Exemplo de equivalência com Python:

```python
# Bloco "repita 10 vezes → diga Olá, mundo!"
for x in range(10):
    print("Olá, mundo!")
```

> [!tip] Próximo passo natural Após dominar lógica visual, o passo seguinte é aprender a **sintaxe** de uma linguagem — como declarar variáveis, escrever condicionais e loops em código real.

---

## 🔧 No-Code — Ferramentas Sem Código

Desenvolvimento sem escrever código. Existem três abordagens:

|Abordagem|Descrição|Personalização|Curva de aprendizado|
|---|---|---|---|
|**High-Code**|Programação tradicional completa|Total|Alta|
|**Low-Code**|Híbrido: componentes visuais + código opcional|Média|Média|
|**No-Code**|Apenas arrastar e soltar, zero código|Limitada|Baixa|

> [!tip] Palavra-chave da área A resposta para "qual abordagem usar?" é sempre **depende** — do prazo, do orçamento, da complexidade e do nível de personalização necessário.

---

### Quando usar No-Code

No-Code se destaca em soluções **padronizadas e bem definidas**:

- Marketplaces (OLX, Airbnb, plataformas de conexão)
- Sistemas de gestão (escolas, lojas, estoque)
- Soluções fintech simples (organização financeira, gestão de contas)
- Sistemas de delivery
- MVPs e provas de conceito (PoC) — validar ideias rapidamente

> [!warning] Limitações do No-Code Não é adequado para jogos complexos, sistemas embarcados (hardware direto), ou qualquer solução que exija alta personalização fora dos padrões da ferramenta.

---

### Categorias de ferramentas No-Code/Low-Code

As ferramentas se dividem em 9 categorias principais: Business Intelligence, CRM empresarial, IoT, Marketing, E-commerce, Design, Desenvolvimento de software, Automação de workflow e **Desenvolvimento Web/Mobile** — foco do curso.

---

### Ferramentas estudadas

**Bubble** (`bubble.io`) — plataforma totalmente No-Code para aplicações web. Editor visual, banco de dados próprio, editor de fluxo de trabalho (workflow) e hospedagem integrada. Hospeda milhões de apps; foi a primeira plataforma no-code, lançada em 2012.

**FlutterFlow** (`flutterflow.io`) — plataforma No-Code/Low-Code para apps mobile. Baseada no framework Flutter (Google/Dart), gera apps nativos para Android, iOS e Web. Permite exportar o código Flutter gerado, funcionando como ponte para o High-Code.

> [!note] Critério de escolha entre ferramentas Equilíbrio entre **quantidade de recursos** e **facilidade de uso**. Ferramentas muito complexas ou muito limitadas devem ser descartadas. Bubble e FlutterFlow foram escolhidas por oferecerem esse equilíbrio com planos gratuitos viáveis.

