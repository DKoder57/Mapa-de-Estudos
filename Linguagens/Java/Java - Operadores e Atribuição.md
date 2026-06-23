---
tags: [java, operadores, atribuicao, casting, expressoes] 
área: Desenvolvimento de Sistemas / Java 
status: draft
---
# 🧮 Java - Operadores e Atribuição

> Fonte: _Introdução à Linguagem de Programação Java_

## 1. O Operador de Atribuição (`=`)

A atribuição de um valor a uma variável consiste em transferir o dado processado do lado **direito** do sinal de igual (`=`) para a variável declarada à **esquerda**.

Java

```java
x = 10; // Atribui o valor inteiro 10 à variável x
```

### Atribuição Primitiva

Pode ser realizada por meio de um valor fixo (literal) ou do resultado calculado de uma expressão matemática:

Java

```java
int x = 7;       // Atribuição literal
int y = x + 2;   // Atribuição baseada numa expressão
int z = x * y;   // Atribuição misturando expressão e literal
```

### Casting de Tipos Primitivos (Conversão de Tipos)

O Java monitora rigorosamente a compatibilidade de tamanhos entre os recipientes de memória. Quando tentamos mover dados entre tipos diferentes, ocorrem dois cenários:

1. **Conversão Implícita (Alargamento / _Widening_):** Ocorre de forma automática quando atribuímos uma variável de menor capacidade a uma de maior capacidade (ex: colocar um `byte` ou `short` dentro de um `int`). Não há risco de perda de dados.
    
2. **Conversão Explícita (Estreitamento / _Narrowing_):** Ocorre quando tentamos atribuir um tipo de maior precisão/tamanho a um de menor precisão (ex: colocar um `int` dentro de um `byte`). Exige a aplicação do operador de _casting_ `(tipo)`. Caso contrário, o compilador emitirá o erro **"possível perda de precisão"**.
    

Java

```java
int a = 50;
byte v = (byte) a; // Casting explícito obrigatório
```

#### Atribuição de Literais Fora do Limite (Estouro de Escopo)

Se for forçado um _casting_ explícito em um valor literal que ultrapassa o limite físico do tipo primitivo destino, o Java não gerará um erro em tempo de execução, mas reduzirá o número aplicando o método de **complemento de dois**.

- **Exemplo prático com `byte` (limite de -128 a 127):**
    
    Java
    
    ```java
    byte b = (byte) 129; 
    System.out.println(b); // O resultado impresso será -127
    ```
    

### Atribuição de Variáveis de Referência

Ao contrário dos tipos primitivos, as variáveis de referência apontam para a localização de objetos guardados dinamicamente na memória.

Java

```java
String s = new String("Abel");
```

A execução desta linha de código realiza três operações sequenciais:

1. Cria a variável de referência denominada `s` na memória _Stack_ (tipo `String`).
    
2. Aloca e cria um novo objeto `String` real na memória _Heap_.
    
3. Interliga-os, fazendo com que a variável `s` aponte para o objeto criado.
    

#### Atribuição de valor nulo

É perfeitamente possível atribuir o literal `null` a qualquer variável de referência. Isto indica que o espaço de referência está reservado, mas não aponta para nenhum objeto físico na memória:

Java

```java
Funcionário a = null; // Espaço alocado, nenhum objeto criado na Heap
```

## 2. Operadores de Atribuição Composta

Quando há necessidade de modificar o valor de uma variável e salvar o novo resultado imediatamente na mesma variável, utilizam-se os operadores abreviados:

|**Operador**|**Exemplo**|**Equivalência Real**|
|---|---|---|
|**`+=`**|`i += 8;`|`i = i + 8;`|
|**`-=`**|`i -= 3;`|`i = i - 3;`|
|**`*=`**|`i *= 2;`|`i = i * 2;`|
|**`/=`**|`i /= 4;`|`i = i / 4;`|
|**`%=`**|`i %= 2;`|`i = i % 2;`|

## 3. Operadores Aritméticos

Os operadores aritméticos executam cálculos tradicionais algébricos. São classificados como **operadores binários** porque exigem obrigatoriamente dois operandos (um em cada lado do símbolo). Os operandos devem ser estritamente numéricos ou do tipo `char` (uma vez que caracteres são mapeados internamente como inteiros).

Java

```java
int total = 47 + 3; // 47 e 3 são os operandos
```

### Regras de Promoção Numérica (Tipo do Resultado)

O tipo primitivo resultante de um cálculo aritmético binário segue uma hierarquia estrita de conversão automática baseada nos operandos envolvidos:

1. Se um dos operandos for `double`, o outro é promovido a `double` e o resultado será **`double`**.
    
2. Caso contrário, se um for `float`, o outro é promovido a `float` e o resultado será **`float`**.
    
3. Caso contrário, se um for `long`, o outro é promovido a `long` e o resultado será **`long`**.
    
4. Caso contrário, **ambos os operandos são convertidos automaticamente para `int`**, e o resultado final da expressão matemática será **`int`**.
    

> [!WARNING] Promoção de Tipos Pequenos
> 
> Para operadores unários ou binários aplicados diretamente sobre variáveis isoladas do tipo `byte`, `short` ou `char`, o Java promove implicitamente estes valores para **`int`** durante a operação.

### Divisão Inteira vs. Ponto Flutuante

Ao efetuar a divisão entre dois números inteiros, o Java trunca o resultado, descartando completamente qualquer componente fracionário.

Java

```java
int divInteira = 5 / 2;      // Resultado: 2
double divReal = 5.0 / 2.0;  // Resultado: 2.5
```

#### Divisão por Zero

Tentar realizar uma operação de divisão inteira por zero (`0`) gerará uma exceção crítica em tempo de execução:

Java

```java
int erro = 10 / 0; // Dispara uma ArithmeticException no console
```

### O Operador de Módulo (`%`)

O operador de módulo retorna estritamente o **resto de uma divisão inteira**, sendo aplicável tanto a números inteiros quanto a tipos de ponto flutuante.

Java

```java
int resto = 15 % 4; // O resultado será 3 (pois 15 dividido por 4 dá 3, com resto 3)
```

## 4. Operadores de Atalho (Incremento e Decremento)

Fornecem uma sintaxe simplificada para somar ou subtrair uma unidade (`1`) do valor atual de uma variável numérica:

- **Incremento (`++`):** `x++;` é o equivalente direto a `x = x + 1;`
    
- **Decremento (`--`):** `x--;` é o equivalente direto a `x = x - 1;`
    

## 5. Operadores Relacionais / Condicionais

Utilizados para determinar a relação lógica ou igualdade estrutural entre dois operandos. O retorno destas operações é obrigatoriamente um valor lógico **`boolean`** (`true` ou `false`).

|**Operador**|**Descrição**|**Exemplo**|
|---|---|---|
|**`==`**|Igual a|`if (total == 10)`|
|**`!=`**|Diferente de|`if (total != 0)`|
|**`<`**|Menor que|`if (idade < 18)`|
|**`>`**|Maior que|`if (salario > 2500)`|
|**`<=`**|Menor ou igual a|`if (contador <= 10)`|
|**`>=`**|Maior ou igual a|`if (nota >= 6.0)`|

> [!CAUTION] Atenção à Grafia
> 
> Nunca confunda o operador de atribuição de dados (**`=`**) com o operador condicional de teste de igualdade (**`==`**). Trocar um pelo outro gerará falhas de lógica ou erros de compilação.

## Links relacionados

- [[Java - Terminologias Fundamentais]]
    
- [[Java - Diretrizes de Programação e Convenções]]
    
- [[Java - Tipos de Dados Primitivos]]
    
- [[Java - Variáveis de Instância vs. Locais]]