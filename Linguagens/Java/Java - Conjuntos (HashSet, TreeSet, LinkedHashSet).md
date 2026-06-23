---
tags: [java, collections, set, hashset, treeset, linkedhashset, estruturas-de-dados] 
área: Desenvolvimento de Sistemas / Java 
status: draft
---
# 📦 Java - Framework de Coleções: Conjuntos (HashSet, TreeSet, LinkedHashSet)

> Fonte: _Introdução à Linguagem de Programação Java_

## A Interface `Set`

No Java Collections Framework, a interface **`Set`** (também pertencente ao pacote `java.util`) representa o conceito matemático de um **conjunto**. A sua principal característica diferencial em relação à interface `List` é que **ela não permite elementos duplicados**.

Se tentar adicionar um elemento que já existe dentro do conjunto, a operação `.add()` simplesmente retornará `false` e a estrutura ignorará a inserção, garantindo a unicidade dos dados.

O Java fornece três implementações principais para a interface `Set`, cada uma projetada para cenários de performance e ordenação específicos: `HashSet`, `LinkedHashSet` e `TreeSet`.

## 1. `HashSet`

O **`HashSet`** é a implementação mais popular e performática da interface `Set`. Ele armazena os seus elementos utilizando uma tabela de espalhamento (_Hash Table_, baseada internamente num `HashMap`).

### Características:

- **Sem Ordem Garantida:** Os elementos não são guardados por ordem de inserção e nem por ordem alfabética/numérica. A disposição dos itens pode inclusive mudar com o tempo e após novas inserções.
    
- **Alta Performance:** Oferece excelente desempenho para as operações básicas como adicionar (`add`), remover (`remove`) e verificar a existência de um item (`contains`), operando em tempo constante $O(1)$.
    
- **Elemento Nulo:** Permite o armazenamento de **um** único elemento `null`.
    
- **Mecanismo de Unicidade:** Para determinar se dois objetos são duplicados, o `HashSet` depende estritamente da implementação correta dos métodos `hashCode()` e `equals()` nos objetos contidos.
    

## 2. `LinkedHashSet`

O **`LinkedHashSet`** é uma subclasse direta do `HashSet`. Ele opera exatamente da mesma forma, mas com uma adição estrutural: mantém uma **lista duplamente ligada** (_Doubly-Linked List_) que percorre todos os seus elementos.

### Características:

- **Preserva a Ordem de Inserção:** Ao iterar sobre um `LinkedHashSet`, os elementos serão retornados exatamente na mesma ordem em que foram inseridos no conjunto.
    
- **Performance Linear Próxima ao HashSet:** O custo das operações básicas continua a ser $O(1)$, porém com um leve _overhead_ (sobrecarga) de tempo e memória para gerir os ponteiros da lista ligada.
    
- **Elemento Nulo:** Também permite a inclusão de um elemento `null`.
    

## 3. `TreeSet`

O **`TreeSet`** adota uma abordagem estrutural completamente diferente, baseando-se internamente numa estrutura de dados de árvore binária auto-balanceada (especificamente uma **Árvore Rubro-Negra** ou _Red-Black Tree_).

### Características:

- **Ordenação Natural ou Customizada:** Os elementos são organizados automaticamente de forma crescente. Se forem `Strings`, estarão em ordem alfabética; se forem números, em ordem numérica. Também é possível passar um `Comparator` customizado no construtor da classe.
    
- **Performance Logarítmica:** Devido à navegação em árvore, as operações de busca, inserção e remoção são ligeiramente mais lentas que as dos outros conjuntos, operando em tempo logarítmico $O(\log n)$.
    
- **Proibição de Nulos:** **Não permite** elementos `null`. Tentar adicionar um valor nulo resultará numa exceção `NullPointerException`, pois a estrutura precisa de invocar métodos de comparação entre os itens.
    
- **Mecanismo de Unicidade:** Em vez de usar `equals()`, o `TreeSet` utiliza o método `compareTo()` (da interface `Comparable`) ou um `Comparator` para validar se um elemento é duplicado. Se `compareTo(A, B) == 0`, o elemento é considerado duplicado e rejeitado.
    

## Tabela Comparativa de Conjuntos

|**Característica**|**HashSet**|**LinkedHashSet**|**TreeSet**|
|---|---|---|---|
|**Estrutura Interna**|Tabela Hash|Tabela Hash + Lista Ligada|Árvore Rubro-Negra|
|**Ordenação**|Nenhuma|Ordem de Inserção|Ordem Natural (ou via `Comparator`)|
|**Velocidade ($add/contains$)**|$O(1)$|$O(1)$|$O(\log n)$|
|**Permite `null`?**|Sim (Apenas 1)|Sim (Apenas 1)|**Não**|

## Exemplo Prático de Implementação

O programa abaixo ilustra o comportamento de rejeição de duplicados e as diferenças cruciais de ordenação entre cada uma das três implementações:

Java

```java
package br.com.java.aula.collections;

import java.util.HashSet;
import java.util.LinkedHashSet;
import java.util.TreeSet;
import java.util.Set;

public class SetDemo {
    public static void main(String[] args) {
        
        // 1. Criando as três variantes de conjuntos
        Set<String> hashSet = new HashSet<>();
        Set<String> linkedHashSet = new LinkedHashSet<>();
        Set<String> treeSet = new TreeSet<>();

        // Lista de elementos com um item duplicado ("Linux")
        String[] elementos = {"Linux", "Ubuntu", "Fedora", "Debian", "Linux"};

        // 2. Populando as estruturas
        for (String el : elementos) {
            hashSet.add(el);
            linkedHashSet.add(el);
            treeSet.add(el);
        }

        // 3. Exibindo os resultados e analisando a ordenação
        System.out.println("====== COMPORTAMENTO DOS CONJUNTOS ======");
        
        // Nota: O tamanho será 4 para todos, pois "Linux" duplicado foi descartado.
        System.out.println("Tamanho do conjunto (Duplicados ignorados): " + hashSet.size());
        System.out.println("-----------------------------------------");

        // HASHSET: Ordem imprevisível / caótica
        System.out.println("HashSet (Sem ordem garantida):");
        System.out.println(hashSet); 
        
        // LINKEDHASHSET: Respeita rigorosamente a sequência de inserção
        System.out.println("\nLinkedHashSet (Ordem de inserção):");
        System.out.println(linkedHashSet); 
        
        // TREESET: Organiza automaticamente em ordem alfabética (A-Z)
        System.out.println("\nTreeSet (Ordem natural / alfabética):");
        System.out.println(treeSet);
        
        // 4. Teste de Verificação Rápida com Contains
        if (hashSet.contains("Fedora")) {
            System.out.println("\nO elemento 'Fedora' existe no conjunto! (Verificado em O(1))");
        }
    }
}
```

## Links relacionados

- [[Java - Programação Orientada a Objetos]]
    
- [[Java - Loop Enhanced For (Aprimorado)]]
    
- [[Java - Collections Framework (ArrayList e Vector)]]