---
tags: [java, tipos-primitivos, memoria, variaveis, escopo]
área: Desenvolvimento de Sistemas / Java
status: draft
---

# 🔢 Java - Tipos de Dados Primitivos

> Fonte: _Introdução à Linguagem de Programação Java_

---

## O que são Tipos Primitivos?

Nem tudo no ecossistema Java é tratado como um objeto. Por razões estritas de **desempenho e eficiência**, os desenvolvedores da linguagem mantiveram um grupo especial de tipos nativos denominados **tipos primitivos** (ou tipos simples).

Uma das principais características que garante a portabilidade do Java é que o tamanho e o comportamento de cada tipo primitivo são estritamente fixados pela especificação da linguagem. Isso significa que **os tamanhos não mudam** de um sistema operacional ou arquitetura de hardware para outro.

O Java define exatamente **oito tipos primitivos de dados**, divididos em quatro grandes grupos:

| Grupo | Tipos Primitivos | Descrição |
| --- | --- | --- |
| **Inteiros** | `byte`, `short`, `int`, `long` | Números inteiros assinalados (com sinal positivo ou negativo). |
| **Ponto Flutuante** | `float`, `double` | Números reais que representam precisão fracionária. |
| **Caracteres** | `char` | Símbolos isolados baseados no conjunto de caracteres Unicode. |
| **Booleano** | `boolean` | Tipo especial lógico que representa apenas valores verdadeiros ou falsos. |

> [!TIP] Economia de Memória
> Escolher o tipo primitivo correto é uma excelente prática para otimizar o uso da memória, especialmente ao manipular matrizes (*arrays*) de grandes dimensões. 
> 
> Exemplo de alocação para o mesmo valor numérico (`24`):
> - `byte byteVariable = 24;` $\rightarrow$ Usa **8 bits** de memória.
> - `int intVariável = 24;` $\rightarrow$ Usa **32 bits** de memória (4x maior que o byte).
> - `long longVariable = 24L;` $\rightarrow$ Usa **64 bits** de memória (8x maior que o byte).

---

## Detalhes Técnicos dos Oito Tipos

### 1. Grupo dos Inteiros

#### `byte`
- **Tamanho:** 8 bits (1 byte)
- **Intervalo:** $-128$ até $127$
- **Uso:** Muito útil para economizar espaço de paginação em matrizes gigantescas onde as restrições de memória são críticas.
- **Exemplo:** `byte b = 100;`

#### `short`
- **Tamanho:** 16 bits (2 bytes)
- **Intervalo:** $-32.768$ até $32.767$
- **Uso:** Semelhante ao byte, aplicado em matrizes ou fluxos específicos para poupar hardware.
- **Exemplo:** `short s = 123;`

#### `int`
- **Tamanho:** 32 bits (4 bytes)
- **Intervalo:** $-2.147.483.648$ até $2.147.483.647$
- **Uso:** É o tipo inteiro mais comumente utilizado no dia a dia. É o padrão para controlar laços de repetição (*loops*) e indexar posições de matrizes.
- **Exemplo:** `int v = 123543;`

#### `long`
- **Tamanho:** 64 bits (8 bytes)
- **Intervalo:** $-9.223.372.036.854.775.808$ até $9.223.372.036.854.775.807$
- **Uso:** Utilizado quando o limite do `int` não é grande o suficiente. Bastante comum em aplicações bancárias, sistemas de auditoria e cálculos computacionais massivos. Requer o sufixo `L` ou `l` na inicialização do valor literal.
- **Exemplo:** `long longoVal = 1234567891L;`

---

### 2. Grupo de Ponto Flutuante (Números Reais)

#### `float`
- **Tamanho:** 32 bits (4 bytes) — Precisão simples (IEEE 754).
- **Uso:** Utilizado na avaliação de expressões que exigem frações (como taxas de juro simples ou raízes quadradas) quando o espaço em memória de matrizes é um fator limitante. É mais rápido em determinados processadores. Requer o sufixo `f` ou `F`.
- **Exemplo:** `float taxaJuros = 12.25f;`

#### `double`
- **Tamanho:** 64 bits (8 bytes) — Precisão dupla.
- **Uso:** É o padrão para números fracionários em Java. Em processadores modernos otimizados para matemática de alta velocidade, o `double` executa operações de forma extremamente rápida. Funções matemáticas nativas da classe `Math` (como `sin()`, `cos()` e `sqrt()`) retornam obrigatoriamente `double`. Pode usar o sufixo opcional `d` ou `D`.
- **Exemplo:** `double duplo = 12345.234d;`

---

### 3. Grupo de Caracteres e Lógicos

#### `boolean`
- **Tamanho:** Atribuído dinamicamente pela JVM de acordo com a arquitetura.
- **Valores:** `true` (verdadeiro) ou `false` (falso).
- **Uso:** Usado como sinalizador (*flag*) de controle para rastrear condições lógicas. É a estrutura retornada por todos os operadores relacionais (ex: `a < b`) e o tipo obrigatório exigido por estruturas condicionais como `if` e `while`.
- **Exemplo:** `boolean val = false;`

#### `char`
- **Tamanho:** 16 bits (2 bytes) — Baseado no padrão internacional Unicode.
- **Intervalo:** `'\u0000'` (0) até `'\uffff'` ($65.535$).
- **Uso:** Armazena um único caractere de texto. Como aceita mapeamento numérico direto da tabela de caracteres, não existem caracteres negativos.
- **Exemplo:** ```java
  char ch1 = 88;   // Mapeamento numérico (Código ASCII/Unicode para 'X')
  char ch2 = 'Y';  // Atribuição literal direta entre aspas simples```


#### Inicialização e Escopo de Variáveis Primitivas

O comportamento de inicialização de uma variável primitiva varia drasticamente dependendo do local onde ela foi declarada dentro da estrutura do código.

#### 1. Variáveis de Instância (Nível de Classe)

São aquelas declaradas fora de qualquer método, pertencendo diretamente ao corpo da classe.

- **Inicialização:** **Não é obrigatória**. Se não for fornecido um valor inicial, o compilador atribuirá automaticamente um **valor padrão** baseado no tipo de dados.
    
- **Boa Prática:** Embora o compilador forneça o valor padrão, depender implicitamente dessa atribuição automática é considerado uma má prática de engenharia de software.
    

|**Tipo Primitivo**|**Valor Padrão Inicial**|
|---|---|
|`byte`, `short`, `int`|`0`|
|`long`|`0L`|
|`float`|`0.0f`|
|`double`|`0.0d`|
|`char`|`'\u0000'` (Caractere nulo / espaço em branco)|
|`boolean`|`false`|

### 2. Variáveis Locais (Nível de Método)

São aquelas declaradas dentro do escopo de um método ou bloco de controle (como laços `for` ou `if`).

- **Inicialização:** **Obrigatória antes da utilização**. O compilador Java **nunca** atribui valores padrão para variáveis locais.
    
- **Consequência:** Tentar acessar ou ler uma variável local que não tenha sido explicitamente inicializada no código resultará num **erro em tempo de compilação**.
    

## Exemplo Prático: `DemoPrimitivo`

Abaixo está a implementação clássica demonstrando a declaração, inicialização correta e a impressão via console de todos os tipos primitivos abordados:

Java

```java
package br.com.java.aula;

public class DemoPrimitivo {
    public static void main(String[] args) {
        // Declaração e Inicialização de Variáveis Locais
        byte b = 100;
        short s = 123;
        int v = 123543;
        long longoVal = 1234567891L;
        
        float taxaJuros = 12.25f;
        double duplo = 12345.234;
        
        boolean val = true;
        char ch1 = 88; // Imprime 'X'
        char ch2 = 'Y';

        // Exibindo os valores no console
        System.out.println("Valor Byte: " + b);
        System.out.println("Valor Short: " + s);
        System.out.println("Valor Int: " + v);
        System.out.println("Valor Long: " + longoVal);
        System.out.println("Valor Float: " + taxaJuros);
        System.out.println("Valor Double: " + duplo);
        System.out.println("Valor Boolean: " + val);
        System.out.println("Valor Char 1: " + ch1);
        System.out.println("Valor Char 2: " + ch2);
    }
}
```

## Links relacionados

- [[Java - Introdução e Plataforma]]
    
- [[Java - Terminologias Fundamentais]]
    
- [[Java - Estrutura do Programa e HelloWorld]]
    
- [[Java - Diretrizes de Programação e Convenções]]