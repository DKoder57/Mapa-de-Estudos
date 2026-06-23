---
tags: [java, collections, arraylist, vector, list, estruturas-de-dados] 
área: Desenvolvimento de Sistemas / Java 
status: draft
---
# 📦 Java - Collections Framework (ArrayList e Vector)

> Fonte: _Introdução à Linguagem de Programação Java_

## O que é o Collections Framework?

O **Collections Framework** é um conjunto unificado de classes e interfaces fornecido pelo Java (dentro do pacote `java.util`) para armazenar e manipular grupos de objetos de forma eficiente. Antes da sua introdução (no Java 1.2), a manipulação de múltiplos elementos dependia exclusivamente de arrays estáticos ou de classes utilitárias isoladas como `Vector` e `Hashtable`.

A interface **`List`** é uma das principais ramificações deste ecossistema. Ela representa uma sequência ordenada de elementos (uma coleção indexada) que permite duplicados e garante o controlo posicional de cada item. Duas das implementações mais conhecidas da interface `List` são o **`ArrayList`** e o **`Vector`**.

## 1. O que é um ArrayList?

O **`ArrayList`** é a implementação padrão e mais utilizada da interface `List`. Ele funciona como um **array dinâmico**, o que significa que ele gerencia um array tradicional internamente, mas possui a capacidade de aumentar ou diminuir de tamanho automaticamente à medida que elementos são adicionados ou removidos.

### Características Principais:

- **Acesso Aleatório Rápido:** Como é baseado em arrays, a busca por um elemento através do seu índice (`.get(index)`) é extremamente rápida, operando em tempo constante $O(1)$.
    
- **Não Sincronizado:** O `ArrayList` **não é seguro para ambientes multi-thread** (_not thread-safe_). Se múltiplas threads acederem e modificarem o mesmo `ArrayList` simultaneamente sem sincronização externa, o comportamento será imprevisível, disparando frequentemente a exceção `ConcurrentModificationException`.
    
- **Redimensionamento:** Quando a capacidade máxima atual do array interno é atingida, o `ArrayList` cria um novo array maior (geralmente **50% maior** que o original) e copia os elementos antigos para este novo espaço.
    

## 2. O que é um Vector?

O **`Vector`** é uma classe herdada das primeiras versões do Java (Java 1.0) que foi posteriormente refatorada para implementar a interface `List` e integrar-se ao Collections Framework. Tal como o `ArrayList`, o `Vector` também implementa um array dinâmico.

### Características Principais:

- **Sincronizado (Thread-Safe):** Quase todos os métodos do `Vector` contêm a palavra-chave `synchronized`. Isso significa que ele é seguro para ser utilizado por múltiplas threads concorrentes, pois o Java bloqueia o objeto para garantir que apenas uma thread altere a lista de cada vez.
    
- **Sobrecarga de Performance:** Devido ao mecanismo de bloqueio da sincronização, o `Vector` é significativamente **mais lento** que o `ArrayList` em cenários de thread única (single-thread).
    
- **Redimensionamento:** Quando o `Vector` precisa de expandir o seu espaço interno, ele duplica de tamanho (**100% de crescimento**), a menos que um fator de incremento específico tenha sido definido no seu construtor.
    

## Tabela Comparativa: ArrayList vs. Vector

|**Característica**|**ArrayList**|**Vector**|
|---|---|---|
|**Versão de Introdução**|Java 1.2|Java 1.0 (Classe Legada)|
|**Sincronização (Thread-Safe)**|Não|**Sim**|
|**Performance**|**Mais Rápida** (Sem overhead de locks)|Mais Lenta (Devido aos locks sincronizados)|
|**Taxa de Crescimento**|Aumenta em ~50% do tamanho atual|Dobra de tamanho (100% de aumento)|
|**Iteradores**|Usa `Iterator` e `ListIterator` (Fail-Fast)|Usa `Iterator` e a legada `Enumeration`|

## Exemplo Prático de Implementação

O código abaixo demonstra a criação, manipulação básica e as semelhanças sintáticas entre o `ArrayList` e o `Vector`:

Java

```java
package br.com.java.aula.collections;

import java.util.ArrayList;
import java.util.Vector;
import java.util.List;

public class ListDemo {
    public static void main(String[] args) {
        // 1. Instanciação usando Polimorfismo com a Interface List
        List<String> arrayList = new ArrayList<>();
        List<String> vectorList = new Vector<>();

        // 2. Adicionando Elementos (.add)
        arrayList.add("Java");
        arrayList.add("Python");
        arrayList.add("JavaScript");

        vectorList.add("Linux");
        vectorList.add("Debian");
        vectorList.add("Fedora");

        // 3. Acesso por Índice (.get)
        System.out.println("Elemento 1 do ArrayList: " + arrayList.get(0));
        System.out.println("Elemento 1 do Vector: " + vectorList.get(0));

        // 4. Remoção de Elementos (.remove)
        arrayList.remove("JavaScript");

        // 5. Iteração usando o Enhanced For (Aprimorado)
        System.out.println("\n--- Iterando sobre o ArrayList ---");
        for (String tecnologia : arrayList) {
            System.out.println("Tecnologia: " + tecnologia);
        }

        System.out.println("\n--- Iterando sobre o Vector ---");
        for (String sistema : vectorList) {
            System.out.println("SO: " + sistema);
        }
    }
}
```

## Abordagem Moderna: Como substituir o Vector?

Na engenharia de software moderna em Java, o uso direto da classe `Vector` é considerado uma **má prática** (descontinuado em termos de preferência arquitetural). Se a sua aplicação necessitar de uma lista dinâmica que seja segura para múltiplas threads, prefira utilizar as seguintes alternativas de alta performance do pacote `java.util.concurrent`:

1. **`Collections.synchronizedList()`**: Envolve um `ArrayList` comum num invólucro sincronizado.
    
    Java
    
    ```java
    List<String> listaSegura = Collections.synchronizedList(new ArrayList<>());
    ```
    
2. **`CopyOnWriteArrayList`**: Ideal para cenários concorrentes onde o volume de leituras é muito superior ao de modificações/escritas.
    

## Links relacionados

- [[Java - Programação Orientada a Objetos]]
    
- [[Java - Loop Enhanced For (Aprimorado)]]
    
- [[Java - Manipulação de Strings]]