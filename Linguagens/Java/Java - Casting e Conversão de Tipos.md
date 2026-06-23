---
tags: [java, casting, conversao-de-tipos, primitivos, compilacao] 
área: Desenvolvimento de Sistemas / Java 
status: draft
---
# 🔀 Java - Casting e Conversão de Tipos

> Fonte: _Introdução à Linguagem de Programação Java_

## O que é a Conversão de Tipos (Casting)?

Em Java, a conversão de tipos (_type casting_) é o mecanismo que permite transformar um valor primitivo de um determinado tipo de dados noutro tipo. Como o Java é uma linguagem fortemente tipada e define tamanhos fixos para cada primitivo, o compilador monitoriza rigorosamente se o "recipiente" de destino tem capacidade suficiente para armazenar o valor proveniente do "recipiente" de origem.

As conversões dividem-se fundamentalmente em dois cenários estruturais: **Conversão Implícita** e **Conversão Explícita**.

## 1. Conversão Implícita (Alargamento / _Widening_)

Acontece de forma automática e transparente pelo compilador, sem a necessidade de intervenção ou sintaxe especial por parte do programador.

- **Regra:** Ocorre sempre que se tenta atribuir uma variável de um **recipiente menor** para uma variável de um **recipiente maior** (tipos com maior capacidade de armazenamento ou maior precisão).
    
- **Segurança:** É uma operação totalmente segura, pois não há qualquer risco de perda de informação ou de precisão numérica.
    
- **Exemplo:** Atribuir uma variável do tipo `byte` ou `short` diretamente a uma variável do tipo `int`.
    

Java

```java
byte pequeno = 50;
int grande = pequeno; // Conversão implícita automática
```

## 2. Conversão Explícita (Estreitamento / _Narrowing_)

Ocorre quando se tenta forçar a entrada de um dado de maior capacidade ou precisão num recipiente fisicamente menor.

- **Regra:** Ocorre ao tentar atribuir um tipo primitivo de **maior precisão** a um de **menor precisão**.
    
- **Intervenção Obrigatória:** Exige que o programador utilize a sintaxe de _casting_ explícito, informando o tipo desejado entre parênteses `(tipo)` antes do valor ou variável de origem.
    

### O Erro de "Possível Perda de Precisão"

Se o programador tentar realizar o estreitamento de tipos sem indicar explicitamente o _casting_, o compilador Java bloqueará o programa e lançará um erro em tempo de compilação:

> ❌ **Erro:** `Type mismatch: cannot convert from int to byte` (ou _"possível perda de precisão"_).

#### Exemplo de Correção com Casting Explícito:

Java

```java
int a = 120;
// byte v = a; // Erro em tempo de compilação!
byte v = (byte) a; // Correção utilizando o casting explícito
```

## Atribuição de Literais Fora do Escopo (Estouro de Limite)

Um comportamento crítico do Java ocorre quando se realiza um _casting_ explícito de um valor numérico literal que está **completamente fora do intervalo de cobertura** do tipo primitivo de destino.

Neste cenário, o compilador aceitará a instrução devido ao operador de conversão explícita, mas o valor real será reduzido/truncado utilizando o **método de complemento de dois**.

### Caso Prático: Estouro do tipo `byte`

O tipo primitivo `byte` consegue armazenar apenas valores no intervalo de **-128 a 127**. Se tentarmos forçar o número literal `129` (que está fora do intervalo) para dentro de um `byte`, o valor sofrerá uma rotação binária:

Java

```java
// 129 ultrapassa o limite máximo de 127 por 2 unidades
byte b = (byte) 129; 

System.out.println(b); // O resultado impresso no console será -127
```

## Exemplo Prático Completo: `DemoCasting`

O programa abaixo demonstra os efeitos práticos das conversões implícitas, explícitas e o comportamento do complemento de dois em caso de estouro de escopo:

Java

```java
package br.com.java.aula;

public class DemoCasting {
    public static void main(String[] args) {
        
        // 1. Demonstração de Conversão Implícita (Automática)
        byte amostraByte = 24;
        int amostraInt = amostraByte; // Alargamento automático de 8 para 32 bits
        long amostraLong = amostraInt; // Alargamento automático de 32 para 64 bits
        System.out.println("Conversão Implícita (long): " + amostraLong);
        
        // 2. Demonstração de Conversão Explícita (Casting)
        double valorDouble = 123.45;
        // int valorInt = valorDouble; // Lançaria erro de compilação
        int valorInt = (int) valorDouble; // Estreitamento explícito: trunca as casas decimais
        System.out.println("Conversão Explícita (int): " + valorInt); // Imprime 123
        
        // 3. Efeito do Complemento de Dois (Estouro de Limite)
        int numeroGrande = 129;
        byte resultadoByte = (byte) numeroGrande;
        System.out.println("Resultado do Estouro de Escopo (byte): " + resultadoByte); // Imprime -127
    }
}
```

## Links relacionados

- [[Java - Tipos de Dados Primitivos]]
    
- [[Java - Variáveis de Instância vs. Locais]]
    
- [[Java - Operadores e Atribuição]]
    
- [[Java - Diretrizes de Programação e Convenções]]