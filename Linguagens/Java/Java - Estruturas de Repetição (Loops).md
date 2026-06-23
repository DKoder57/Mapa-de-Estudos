---
tags: [java, loops, estruturas-de-repeticao, controle-de-fluxo] 
área: Desenvolvimento de Sistemas / Java 
status: draft
---
# 🔄 Java - Estruturas de Repetição (Loops)

> Fonte: _Introdução à Linguagem de Programação Java_

## O que é uma Estrutura de Repetição?

Na programação, um **loop** é uma estrutura de controlo de fluxo que permite executar repetidamente um bloco de instruções com base numa expressão booleana.

Enquanto a expressão avaliada for **verdadeira** (`true`), o corpo do loop continua a ser executado. No momento em que a avaliação passa a ser **falsa** (`false`), o loop termina e o fluxo do programa avança para a linha imediatamente seguinte.

Java fornece quatro construções principais de loops, divididas essencialmente entre loops de **pré-teste** (validação no topo), **pós-teste** (validação na base) e loops **definidos/contados**.

## 1. O Loop `while` (Pré-teste)

O loop `while` avalia a sua expressão booleana **antes** de executar o corpo de instruções. É ideal para cenários onde não sabemos exatamente quantas vezes o bloco precisará de ser repetido.

> [!IMPORTANT] Execução Zero
> 
> Como a verificação é feita no topo, se a condição for falsa logo na primeira validação, o corpo do loop **nunca será executado**.

### Sintaxe Básica

Java

```java
while (expressão_booleana) {
    // Bloco de código (corpo do loop)
}
```

### Exemplo Prático (Loop Definido / Contado)

Para criar um loop contado com `while`, é necessário inicializar uma variável de controlo antes e certificar-se de modificar essa variável dentro do bloco para evitar um loop infinito.

Java

```java
public class WhileLoopDemo {
    public static void main(String[] args) {
        int var = 1;
        int limit = 11;
        
        while (var < limit) {
            System.out.println("Contador do Loop: " + var);
            var++; // Modificação da variável de controlo
        }
    }
}
```

> [!WARNING] Loops Infinitos
> 
> Se a expressão booleana for configurada para ser sempre verdadeira (ex: `while(true)`) ou se o programador esquecer-se de atualizar a variável de controlo (`var++`), o programa entrará em loop infinito. Isso consome processamento e causará uma exceção de estouro de memória (_Out of Memory_).

## 2. O Loop `do-while` (Pós-teste)

O loop `do-while` é uma estrutura de pós-teste. A expressão booleana só é avaliada **após** a execução do bloco de código.

- **Garantia:** O código dentro do bloco `do` será executado **pelo menos uma vez**, independentemente de a condição ser verdadeira ou falsa.
    
- **Sintaxe:** Note que o `while` fica na parte inferior e **exige** um ponto e vírgula (`;`) no final.
    

### Sintaxe Básica

Java

```java
do {
    // Corpo do loop
} while (condição);
```

### Exemplo Prático (O efeito pós-teste)

Java

``` java
public class DoWhileLoopDemo {
    public static void main(String[] args) {
        int i = 10;
        
        do {
            i = i + 10;
            System.out.println("Contador do Loop = " + i);
        } while (i < 10);
    }
}
```

**Resultado no Console:** `Contador do Loop = 20`

_Explicação:_ O programa entra direto no bloco `do`, soma `10` à variável `i` (tornando-a `20`) e imprime a mensagem. Só então valida se `i < 10` (20 < 10 é `false`), encerrando o loop após uma iteração.

## 3. O Loop `for` Tradicional

O loop `for` fornece uma notação compacta e abreviada para loops definidos (com número fixo de iterações). Ele agrupa a **inicialização**, o **teste lógico** e a **atualização** numa única linha conveniente.

Java

```java
for (inicialização; condição; atualização) {
    // Corpo do loop
}
```

### Exemplo Convencional

Java

```java
for (int contador = 1; contador < 11; contador++) {
    System.out.println(contador); // Imprime de 1 a 10
}
```

### Variações e Flexibilidades do `for`

O Java permite customizar as seções do cabeçalho do `for`:

- **Múltiplas variáveis:** Pode-se inicializar e atualizar mais do que uma variável, separando as instruções por vírgulas:
    
    Java
    
    ```java
    for (int g = 0, h = 1; g < 6; g++, h--) { ... }
    ```
    
- **Decremento:** A variável de controlo pode decrescer em vez de somar:
    
    Java
    
    ```java
    for (int g = 5; g >= 1; g--) { ... }
    ```
    
- **Seções Omitidas:** É permitido deixar seções vazias se a variável já tiver sido declarada ou se a lógica for tratada dentro do corpo do loop. Contudo, os dois pontos e vírgulas (`;;`) continuam a ser **obrigatórios**:
    
    Java
    
    ```java
    int x = 0;
    for (; x < 10; x++) { ... }
    ```
    

## 4. O Loop `enhanced for` (For-Each)

Introduzido para simplificar a leitura de estruturas de dados, o _enhanced for_ (ou "for aprimorado") permite percorrer de forma sequencial arrays ou coleções de elementos **sem a necessidade de gerir índices** ou definir limites iniciais e finais.

### Sintaxe Básica

Java

```java
for (Tipo iterador : array_ou_colecao) {
    // Bloco de instruções utilizando o iterador
}
```

### Exemplo Prático com Array

Java

```java
public class EnhancedForLoopDemo {
    public static void main(String[] args) {
        int[] meuArray = {100, 90, 80, 70, 60, 50, 40, 30, 20, 10};
        
        // Percorrendo de forma limpa e segura com enhanced for
        for (int loopVal : meuArray) {
            System.out.println(loopVal);
        }
    }
}
```

## 5. Instruções de Ramificação / Desvio (`break` e `continue`)

Utilizadas dentro dos blocos de repetição (`for`, `while`, `do-while`), estas palavras-chave permitem interromper ou saltar fluxos internos do algoritmo.

- **`break`:** Interrompe imediatamente a execução do loop e transfere o controlo do programa para a linha de código logo abaixo e fora desse loop.
    
- **`continue`:** Abandona a iteração atual (ignora as linhas de código que estão abaixo dele dentro do bloco) e força o loop a saltar imediatamente para a próxima iteração (ou teste lógico).
    

### O uso de Rótulos (_Labels_)

Quando trabalhamos com **loops aninhados** (um loop dentro do outro), as instruções `break` e `continue` controlam apenas o loop mais interno por padrão. Para interagir com o loop externo a partir de dentro, utilizamos **rótulos**.

Um rótulo consiste num identificador válido seguido por dois pontos (`:`), posicionado imediatamente antes do loop que se deseja gerir.

Java

```java
public class LoopRotuladoDemo {
    public static void main(String[] args) {
        
        loopExterno: // Definição do rótulo
        for (int i = 1; i <= 3; i++) {
            for (int j = 1; j <= 3; j++) {
                if (i == 2 && j == 2) {
                    break loopExterno; // Interrompe o loop de fora, não apenas o interno
                }
                System.out.println("i = " + i + ", j = " + j);
            }
        }
    }
}
```

## Resumo Comparativo das Estruturas

|**Estrutura**|**Tipo de Teste**|**Quantidade Mínima de Execuções**|**Cenário Ideal**|
|---|---|---|---|
|**`while`**|Pré-teste|0|Quando o número de iterações é desconhecido antecipadamente.|
|**`do-while`**|Pós-teste|1|Quando o bloco precisa de rodar pelo menos uma vez (ex: menus).|
|**`for`**|Pré-teste|0|Quando sabemos exatamente o limite ou intervalo de repetições.|
|**`enhanced for`**|Automático|0 (se vazio)|Para ler todos os elementos de arrays ou coleções sem usar índices.|

## Links relacionados

- [[Java - Operadores e Atribuição]]
    
- [[Java - Casting e Conversão de Tipos]]
    
- [[Java - Tipos de Dados Primitivos]]
    
- [[Java - Estruturas Condicionais]]