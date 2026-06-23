---
tags: [java, concorrencia, threads, runnable, sincronizacao, multithreading] 
área: Desenvolvimento de Sistemas / Java 
status: draft
---

# 🧵 Java - Programação Concorrente (Threads)

> Fonte: _Introdução à Linguagem de Programação Java_

## O que é Concorrência e Multithreading?

No desenvolvimento de software moderno, a **concorrência** é a capacidade de executar múltiplos fluxos de lógica de forma simultânea ou pseudo-simultânea, otimizando o uso dos processadores multi-core modernos. O Java foi projetado desde as suas raízes com suporte nativo a **Multithreading**.

### Processo vs. Thread

- **Processo:** É um programa de computador em execução. Cada processo possui o seu próprio espaço de memória isolado e protegido alocado pelo Sistema Operacional.
    
- **Thread (Linha de Execução):** É um sub-fluxo leve dentro de um processo. Múltiplas threads criadas por uma aplicação Java compartilham o mesmo espaço de memória (a memória _Heap_ do processo), o que permite uma comunicação extremamente rápida entre elas, mas também introduz riscos de corrupção de dados.
    

## Como Criar Threads em Java

O Java fornece duas abordagens fundamentais para definir e executar um fluxo de código paralelo. Ambas exigem a implementação da lógica de execução dentro do método `public void run()`.

### 1. Herdando da Classe `Thread`

Consiste em criar uma subclasse que estende diretamente `java.lang.Thread` e sobrescrever o método `run()`.

Java

```java
class MeuTrabalhador extends Thread {
    @Override
    public void run() {
        System.out.println("Thread rodando via Herança: " + Thread.currentThread().getName());
    }
}
// Para iniciar: new MeuTrabalhador().start();
```

### 2. Implementando a Interface `Runnable` (Abordagem Recomendada)

Consiste em implementar a interface funcional `java.lang.Runnable` e passar essa instância como parâmetro para o construtor de um objeto `Thread`.

Java

```java
class MeuTrabalho Runnable implements Runnable {
    @Override
    public void run() {
        System.out.println("Thread rodando via Interface: " + Thread.currentThread().getName());
    }
}
// Para iniciar: new Thread(new MeuTrabalhoRunnable()).start();
```

> 💡 **Por que Runnable é a melhor prática?** Como o Java não suporta herança múltipla, estender a classe `Thread` impede que a sua classe herde qualquer outra regra de negócio. Implementar `Runnable` mantém a flexibilidade da arquitetura de classes e separa a tarefa (_Task_) do mecanismo de execução (_Worker_).

## O Ciclo de Vida de uma Thread

Uma Thread em Java passa por diferentes estados desde o momento em que é instanciada até a conclusão da sua execução. O gerenciamento desses estados é feito de forma conjunta entre a JVM e o agendador de tarefas (_Thread Scheduler_) do Sistema Operacional.

- **NEW (Nova):** A Thread foi instanciada (via `new`), mas o método `.start()` ainda não foi invocado.
    
- **RUNNABLE (Executável):** O método `.start()` foi chamado. A thread está pronta para rodar e aguarda que o processador lhe aloque tempo de execução.
    
- **BLOCKED (Bloqueada):** A thread está temporariamente impedida de rodar porque aguarda a liberação de um monitor/lock exclusivo (ex: esperando entrar num bloco `synchronized`).
    
- **WAITING (Em Espera):** A thread aguarda indefinidamente que outra thread execute uma ação específica (ativada por métodos como `object.wait()` ou `thread.join()`).
    
- **TIMED_WAITING (Espera por Tempo):** A thread dorme ou aguarda por um período de tempo predeterminado (ex: `Thread.sleep(milissegundos)`).
    
- **TERMINATED (Terminada):** O método `run()` concluiu a sua execução completa ou foi interrompido por uma exceção não tratada. A thread morreu e não pode ser reiniciada.
    

## O Perigo do Acesso Concorrente: Condição de Corrida

Quando duas ou mais threads tentam ler e modificar o mesmo recurso compartilhado (como uma variável ou um objeto na memória Heap) ao mesmo tempo, ocorre o que chamamos de **Condição de Corrida** (_Race Condition_). Como a alternância entre as threads é imprevisível, os dados podem ficar corrompidos ou inconsistentes.

Para evitar este problema, utilizamos o mecanismo de **Sincronização**. A palavra-chave **`synchronized`** do Java cria uma barreira (exclusão mútua), garantindo que apenas uma thread possa aceder a um bloco de código ou método de cada vez.

## Exemplo Prático Completo: Sincronização de Recursos

O programa unificado abaixo demonstra o impacto de múltiplas threads alterando um contador comum e como a palavra-chave `synchronized` corrige as inconsistências na memória compartilhada:

Java

```java
package br.com.java.aula.concorrencia;

// Classe que gerencia o recurso compartilhado pelas threads
class Contador {
    private int valor = 0;

    // Sem o modificador 'synchronized', as threads atropelam-se e o valor final falha
    public synchronized void incrementar() {
        this.valor++; 
    }

    public int getValor() {
        return this.valor;
    }
}

public class ConcurrencyDemo {
    public static void main(String[] args) {
        Contador contadorCompartilhado = new Contador();

        // Definição da tarefa paralela usando expressões Lambda (Java 8+)
        Runnable tarefa = () -> {
            for (int i = 0; i < 1000; i++) {
                contadorCompartilhado.incrementar();
            }
        };

        // Criando duas threads distintas para executar a mesma tarefa
        Thread t1 = new Thread(tarefa, "Thread-Alfa");
        Thread t2 = new Thread(tarefa, "Thread-Beta");

        System.out.println("Disparando as Threads...");
        t1.start();
        t2.start();

        try {
            // O método .join() faz com que a Thread Principal (main) aguarde
            // a conclusão dessas threads antes de avançar
            t1.join();
            t2.join();
        } catch (InterruptedException e) {
            System.err.println("A thread principal foi interrompida.");
        }

        // Se a sincronização funcionou, o resultado deve ser rigorosamente 2000
        System.out.println("\n====== RESULTADO DA CONCORRÊNCIA ======");
        System.out.println("Valor final do contador: " + contadorCompartilhado.getValor());
    }
}
```

## Evolução Arquitetural: Da Concorrência Clássica ao Java Moderno

Gerenciar a criação manual de objetos `Thread` com `new Thread()` torna-se inviável em sistemas corporativos de grande porte. A alocação de uma thread nativa consome cerca de 1MB de memória do S.O. Para otimizar esta arquitetura, o Java evoluiu o seu ecossistema concorrente:

1. **Framework de Executors (`java.util.concurrent`):** Introduzido no Java 5, ele gerencia pools de threads (`ThreadPoolExecutor`). Em vez de criar novas threads, as tarefas são enviadas para uma fila e processadas por um conjunto de threads preexistentes recicladas.
    
2. **Virtual Threads (Java 21+):** Representam uma mudança de paradigma histórica. As Virtual Threads são threads leves gerenciadas diretamente pela JVM, e não pelo Sistema Operacional. Elas permitem que uma única aplicação execute milhões de threads simultâneas com consumo mínimo de memória, eliminando a complexidade dos códigos reativos assíncronos tradicionais.
    

## Links relacionados

- [[Java - Programação Orientada a Objetos]]
    
- [[Java - Tratamento de Exceções]]
    
- [[Java - Collections Framework (ArrayList e Vector)]]
    
- [[Java - StringBuilder e Otimização]]