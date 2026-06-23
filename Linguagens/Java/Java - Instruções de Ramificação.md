---
tags: [java, instrucoes-de-ramificacao, break, continue, return, controlo-de-fluxo] 
área: Desenvolvimento de Sistemas / Java 
status: draft
---
# 🔀 Java - Instruções de Ramificação

> Fonte: _Introdução à Linguagem de Programação Java_

## O que são Instruções de Ramificação?

As **instruções de ramificação** (_branching statements_) são palavras-chave que alteram o fluxo normal de execução de um programa. Elas permitem que o interpretador realize desvios ou saltos imediatos na execução do código, sendo amplamente utilizadas para controlar o comportamento interno de estruturas de repetição (loops) e blocos condicionais.

O Java fornece três instruções de ramificação estruturais:

1. **`break`**: Interrompe e sai imediatamente de uma estrutura de repetição ou de um bloco `switch`.
    
2. **`continue`**: Salta o restante do código na iteração atual de um loop e passa para a próxima iteração.
    
3. **`return`**: Finaliza a execução do método atual e devolve o controlo ao ponto onde o método foi chamado.
    

## 1. A Instrução `break`

A instrução `break` possui duas aplicações fundamentais em Java: terminação de casos dentro de uma estrutura `switch-case` (evitando a execução em cascata) e interrupção forçada de loops (`for`, `while`, `do-while`).

Quando o `break` é executado dentro de um loop, o corpo de repetição é imediatamente encerrado. O controlo do programa salta de forma abrupta para a linha de código posicionada logo após a estrutura do loop.

## 2. A Instrução `continue`

Ao contrário do `break`, que destrói e encerra o loop por completo, a instrução `continue` atua de forma mais cirúrgica, interrompendo apenas a **iteração atual**. Ela faz com que o programa ignore todas as instruções restantes que estejam abaixo dela dentro do corpo do loop, forçando-o a saltar diretamente para a próxima iteração.

O comportamento do `continue` varia de acordo com a estrutura onde é inserido:

- No loop **`while`** e **`do-while`**, o fluxo vai direto para a revalidação da expressão booleana de controlo.
    
- No loop **`for`**, o fluxo salta primeiro para a seção de atualização (ex: `i++`) e só depois avalia a condição de teste.
    

## Exemplo Prático: `BreakContinueDemo`

O programa abaixo demonstra o uso prático de `break` e `continue` na sua forma padrão (não rotulada). O algoritmo percorre uma matriz numérica realizando a soma dos números pares e interrompe o fluxo caso encontre um valor igual ou menor que zero:

Java

```java
package br.com.java.aula;

public class BreakContinueDemo {
    public static void main(String[] args) {
        int[] numbers = {10, 23, 19, 34, 54, 23, 76, 39, 65, 24, 8, 0, 12, 55};
        int sum = 0;

        for (int i = 0; i < numbers.length; i++) {
            // Se encontrar 0 ou número negativo, interrompe o loop por completo
            if (numbers[i] <= 0) {
                System.out.println("Break porque número = " + numbers[i]);
                break;
            } 
            
            // Se o número for ímpar, ignora as linhas abaixo e passa para o próximo índice
            if (numbers[i] % 2 != 0) {
                System.out.println("Número ímpar encontrado na matriz, ignorando o número " + numbers[i]);
                continue;
            }
            
            // Apenas números pares positivos chegam a esta linha
            sum = sum + numbers[i];
        }
        
        System.out.println("Soma de todos os números pares acumulados = " + sum);
    }
}
```

## 3. Instruções Rotuladas (_Labeled Statements_)

Tanto o `break` quanto o `continue` podem ser aplicados de forma **não rotulada** (comportamento padrão que afeta apenas o loop mais interno e imediato) ou **rotulada**.

Os rótulos (_labels_) consistem num identificador válido seguido por dois pontos (`:`), posicionado imediatamente antes de uma instrução de loop. Eles são úteis exclusivamente em cenários de **loops aninhados** (um loop dentro do outro), onde se precisa de especificar de qual nível da estrutura se deseja sair ou continuar.

Java

```java
public class ExemploRotulado {
    public static void main(String[] args) {
        
        loopExterno: // Definição de um rótulo para o loop de fora
        for (int i = 1; i <= 3; i++) {
            for (int j = 1; j <= 3; j++) {
                if (i == 2 && j == 2) {
                    break loopExterno; // Rompe o loop externo, encerrando tudo
                }
                System.out.println("i = " + i + ", j = " + j);
            }
        }
    }
}
```

## 4. A Instrução `return`

A última instrução de controlo de ramificação é o `return`. Ele é usado para realizar um retorno explícito de um método, fazendo com que a execução da rotina atual termine imediatamente e o controlo do programa retorne para o **chamador do método**.

- **Em métodos com retorno específico (`int`, `boolean`, objetos, etc.):** É obrigatório usar `return` acompanhado de um valor ou expressão compatível com o tipo de dados declarado.
    
- **Em métodos sem retorno (`void`):** A instrução `return;` pode ser usada sozinha, servindo unicamente para forçar uma saída antecipada do bloco antes de atingir a chave de encerramento do método.
    

### Exemplo Prático: `ReturnDemo`

Java

```java
package br.com.java.aula;

public class ReturnDemo {
    public static void main(String[] args) {
        ReturnDemo demo = new ReturnDemo();
        
        // Loop que invoca o método de validação para múltiplos valores
        for (int k = 25; k < 31; k++) {
            demo.checaPar(k);
        }
    }

    public boolean checaPar(int a) {
        if (a % 2 == 0) {
            System.out.println(a + " é par");
            return true; // Finaliza o método aqui e devolve true ao main
        }
        
        System.out.println(a + " é ímpar");
        return false; // Finaliza o método aqui e devolve false ao main
    }
}
```

## Links relacionados

- [[Java - Estruturas de Repetição (Loops)]]
    
- [[Java - Estruturas Condicionais]]
    
- [[Java - Operadores e Atribuição]]
    
- [[Java - Loop Enhanced For (Aprimorado)]]