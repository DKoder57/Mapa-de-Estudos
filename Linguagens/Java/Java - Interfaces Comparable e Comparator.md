---
tags: [java, collections, comparable, comparator, ordenacao, poo] 
área: Desenvolvimento de Sistemas / Java
status: draft
---
# 🔄 Java - Interfaces Comparable e Comparator

> Fonte: _Introdução à Linguagem de Programação Java_

## A Necessidade de Ordenação Customizada

Quando trabalhamos com coleções de tipos primitivos ou classes embrulho (_Wrapper classes_ como `String`, `Integer`, `Double`), o Java já sabe exatamente como ordená-los. Chamar `Collections.sort()` numa lista de strings irá organizá-la automaticamente em ordem alfabética, pois estas classes possuem uma **ordenação natural** predefinida pela linguagem.

Contudo, quando criamos as nossas próprias classes (como `Produto`, `Aluno` ou `Funcionario`), a JVM não sabe qual critério usar para a ordenação (Deve ser pelo ID? Pelo nome? Pelo preço?). Para ensinar ao Java como comparar e ordenar objetos complexos, utilizamos as interfaces **`Comparable`** e **`Comparator`**.

## 1. A Interface `Comparable`

A interface `Comparable` (localizada no pacote base `java.lang`) é utilizada para definir a **ordenação natural** de uma classe. Dizemos que ela implementa uma ordenação "intrinseca", pois a própria classe que representa o dado assume a responsabilidade de se comparar com outra instância do mesmo tipo.

- **Método Único:** `public int compareTo(T o)`
    
- **Regra de Retorno:**
    
    - Retorna um número **negativo** se o objeto atual (`this`) for **menor** que o objeto comparado (`o`).
        
    - Retorna **zero** se o objeto atual (`this`) for **igual** ao objeto comparado (`o`).
        
    - Retorna um número **positivo** se o objeto atual (`this`) for **maior** que o objeto comparado (`o`).
        

Java

```java
// A classe implementa Comparable em si mesma
public class Produto implements Comparable<Produto> {
    private String nome;
    private double preco;

    // Critério de ordenação natural: por preço de forma crescente
    @Override
    public int compareTo(Produto outro) {
        if (this.preco < outro.preco) return -1;
        if (this.preco > outro.preco) return 1;
        return 0;
        // Dica de otimização: Double.compare(this.preco, outro.preco);
    }
}
```

## 2. A Interface `Simple Comparator`

A interface `Comparator` (localizada no pacote utilitário `java.util`) é utilizada para definir **ordenações alternativas, customizadas ou múltiplas**. Ao contrário do `Comparable`, ela é implementada numa classe separada (ou via expressões Lambda), funcionando como um agente externo de comparação.

Esta abordagem é ideal quando não temos acesso ao código-fonte da classe original para modificá-la, ou quando precisamos de ordenar os mesmos objetos por critérios diferentes em momentos distintos do sistema (ex: ora por nome, ora por estoque).

- **Método Principal:** `public int compare(T o1, T o2)`
    
- **Regra de Retorno:**
    
    - Retorna um número **negativo** se `o1` for **menor** que `o2`.
        
    - Retorna **zero** se `o1` for **igual** a `o2`.
        
    - Retorna um número **positivo** se `o1` for **maior** que `o2`.
        

Java

```java
import java.util.Comparator;

// Classe externa focada exclusivamente no critério por Nome
public class ComparadorPorNome implements Comparator<Produto> {
    @Override
    public int compare(Produto p1, Produto p2) {
        return p1.getNome().compareTo(p2.getNome()); // Reutiliza o compareTo da String
    }
}
```

## Tabela Comparativa: Comparable vs. Comparator

|**Característica**|**Comparable**|**Comparator**|
|---|---|---|
|**Pacote**|`java.lang`|`java.util`|
|**Método de Assinatura**|`compareTo(T o)`|`compare(T o1, T o2)`|
|**Tipo de Ordenação**|Ordenação Padrão/Natural|Ordenação Alternativa/Customizada|
|**Modifica a classe original?**|**Sim** (A classe deve implementar a interface)|**Não** (A lógica fica numa classe externa ou bloco isolado)|
|**Quantidade de Critérios**|Apenas **um** critério por classe|**Múltiplos** (Pode criar quantos comparadores quiser)|
|**Invocação Prática**|`Collections.sort(lista)`|`Collections.sort(lista, emComparador)`|

## Exemplo Prático Completo: Estruturando as Comparações

O código unificado abaixo demonstra como criar uma classe com ordenação natural (por ID) e fornecer flexibilidade de ordenação por outros atributos utilizando `Comparator` (tradicional e com recursos modernos do Java 8+):

Java

```java
package br.com.java.aula.ordenacao;

import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;
import java.util.List;

// 1. Classe que define sua ordenação natural pelo ID
class Aluno implements Comparable<Aluno> {
    private int id;
    private String nome;
    private double nota;

    public Aluno(int id, String nome, double nota) {
        this.id = id;
        this.nome = nome;
        this.nota = nota;
    }

    public int getId() { return id; }
    public String getNome() { return nome; }
    public double getNota() { return nota; }

    // Implementação da Ordenação Natural (Crescente por ID)
    @Override
    public int compareTo(Aluno outro) {
        return Integer.compare(this.id, outro.id);
    }

    @Override
    public String toString() {
        return "[" + id + "] " + nome + " - Nota: " + nota;
    }
}

// 2. Classe Comparadora Externa (Ordem Decrescente de Nota)
class ComparadorPorNotaDecrescente implements Comparator<Aluno> {
    @Override
    public int compare(Aluno a1, Aluno a2) {
        return Double.compare(a2.getNota(), a1.getNota()); // Invertido para decrescente
    }
}

// 3. Classe Executável
public class OrdenacaoDemo {
    public static void main(String[] args) {
        List<Aluno> lista = new ArrayList<>();
        lista.add(new Aluno(3, "Carlos", 8.5));
        lista.add(new Aluno(1, "Ana", 9.8));
        lista.add(new Aluno(2, "Bruno", 7.2));

        System.out.println("=== Ordem Original ===");
        lista.forEach(System.out::println);

        // Aplica a ordenação natural (Usa o compareTo interno de Aluno)
        Collections.sort(lista);
        System.out.println("\n=== Ordenado por ID (Natural - Comparable) ===");
        lista.forEach(System.out::println);

        // Aplica a ordenação customizada externa (Usa o compare da classe externa)
        Collections.sort(lista, new ComparadorPorNotaDecrescente());
        System.out.println("\n=== Ordenado por Nota (Decrescente - Comparator) ===");
        lista.forEach(System.out::println);

        // Abordagem Moderna (Java 8+): Usando Lambdas ou Method References sem criar novas classes
        lista.sort(Comparator.comparing(Aluno::getNome));
        System.out.println("\n=== Ordenado por Nome (Moderno - Lambda/Method Reference) ===");
        lista.forEach(System.out::println);
    }
}
```

> ⚠️ **Nota de Performance:** Algoritmos de ordenação em coleções dinâmicas estruturadas (como o Timsort do Java) operam com complexidade de tempo de $O(n \log n)$. Garantir que os métodos `compareTo` e `compare` sejam o mais simples e diretos possíveis evita gargalos de processamento.

## Links relacionados

- [[Java - Programação Orientada a Objetos]]
    
- [[Java - Collections Framework (ArrayList e Vector)]]
    
- [[Java - Conjuntos (HashSet, TreeSet, LinkedHashSet)]]