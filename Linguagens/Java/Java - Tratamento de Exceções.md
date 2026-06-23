---
tags: [java, excecoes, tratamento-de-erros, try-catch, runtimeexception] 
área: Desenvolvimento de Sistemas / Java
status: draft
---
# ⚠️ Java - Tratamento de Exceções

> Fonte: _Introdução à Linguagem de Programação Java_

## O que é uma Exceção?

Uma **Exceção** (_Exception_) é um evento anormal que ocorre durante a execução de um programa (tempo de execução) e que interrompe o fluxo normal de instruções do código. O mecanismo de tratamento de exceções do Java serve para capturar estes erros de forma controlada, permitindo que a aplicação trate o problema ou termine de forma graciosa, em vez de crashar abruptamente.

Quando ocorre um erro dentro de um método, este método cria um objeto especial — o **objeto da exceção** — e entrega-o à máquina virtual (JVM). Este objeto contém o tipo do erro, o estado do sistema e a linha exata onde a falha aconteceu (_Stack Trace_).

## A Hierarquia de Exceções em Java

Em Java, todas as exceções e erros fazem parte de uma hierarquia de classes bem definida, cuja raiz é a classe **`Throwable`**.

### 1. `Error` (Erros do Sistema)

Representa falhas graves de infraestrutura, hardware ou da própria máquina virtual (JVM). São condições das quais a aplicação normalmente **não se consegue recuperar**.

- _Exemplos:_ `OutOfMemoryError` (falta de memória RAM) ou `StackOverflowError` (estouro da pilha devido a recursão infinita). Não devem ser capturados pelo programador.
    

### 2. `Exception` (Exceções da Aplicação)

Representa condições de erro que uma aplicação normal pode e deve capturar. Divide-se em duas categorias cruciais:

- **Exceções Não Verificadas (_Unchecked Exceptions_):** São todas as classes que herdam de **`RuntimeException`**. Ocorrem geralmente por falhas de lógica de programação. O compilador não obriga o programador a tratá-las.
    
- **Exceções Verificadas (_Checked Exceptions_):** São todas as outras subclasses de `Exception` (que não herdam de `RuntimeException`). Representam imprevistos fora do controlo direto do programa (ex: rede caída, ficheiro inexistente). **O compilador exige obrigatoriamente** que o programador trate ou declare estas exceções.
    

## Tabela Comparativa: Checked vs. Unchecked

|**Característica**|**Exceções Verificadas (Checked)**|**Exceções Não Verificadas (Unchecked)**|
|---|---|---|
|**Classe Base**|Subclasses de `Exception` (exceto `RuntimeException`)|Subclasses de `RuntimeException`|
|**Validação**|Verificadas em tempo de **compilação**.|Verificadas em tempo de **execução**.|
|**Obrigatoriedade**|Exige bloco `try-catch` ou declaração `throws`.|O tratamento é opcional (recomenda-se corrigir o código).|
|**Cenário Comum**|Fatores externos (Ficheiros, Banco de Dados, Rede).|Erros de lógica de programação (bugs).|
|**Exemplos**|`IOException`, `FileNotFoundException`, `SQLException`|`NullPointerException`, `ArrayIndexOutOfBoundsException`|

## As Cinco Palavras-Chave do Tratamento de Erros

O ecossistema de captura de falhas em Java opera com base em cinco palavras reservadas:

1. **`try`:** Delimita um bloco de código que será monitorizado. Se qualquer linha dentro deste bloco disparar uma exceção, a execução normal é imediatamente interrompida e desviada.
    
2. **`catch`:** Define o bloco de código responsável por capturar e tratar uma exceção específica gerada no bloco `try`. É possível empilhar múltiplos blocos `catch` para gerir diferentes tipos de erro.
    
3. **`finally`:** Bloco opcional que é **sempre executado**, independentemente de ter ocorrido uma exceção ou não. É utilizado para rotinas de limpeza de recursos (como fechar conexões ou ficheiros).
    
4. **`throw`:** Utilizado explicitamente pelo programador para instanciar e "lançar" uma exceção manualmente no fluxo do código.
    
5. **`throws`:** Utilizado na assinatura de um método para alertar quem o invoca de que aquele método pode vir a lançar uma exceção verificada, transferindo a responsabilidade do tratamento para o método chamador.
    

## Exemplo Prático Completo

O programa unificado abaixo demonstra a criação de uma exceção customizada, o uso de assinaturas com `throws`, a captura múltipla (_Multi-Catch_) e a garantia de execução do bloco `finally`:

Java

```java
package br.com.java.aula.excecoes;

// 1. Criação de uma Exceção Customizada (Regra de Negócio)
class SaldoInsuficienteException extends Exception {
    public SaldoInsuficienteException(double saldoActual, double valorTentado) {
        super("Erro: Saldo insuficiente! Saldo actual: €" + saldoActual + ". Tentou levantar: €" + valorTentado);
    }
}

// 2. Classe de Negócio que propaga exceções
class ContaBancaria {
    private double saldo = 100.0;

    // O uso de 'throws' avisa que este método é perigoso (Checked Exception)
    public void levantar(double valor) throws SaldoInsuficienteException {
        if (valor <= 0) {
            throw new IllegalArgumentException("O valor do levantamento deve ser positivo."); // Unchecked
        }
        if (valor > saldo) {
            throw new SaldoInsuficienteException(this.saldo, valor); // Checked
        }
        this.saldo -= valor;
        System.out.println("Levantamento efectuado! Novo Saldo: €" + this.saldo);
    }
}

// 3. Classe Executável com Tratamento Robusto
public class ExceptionDemo {
    public static void main(String[] args) {
        ContaBancaria conta = new ContaBancaria();

        System.out.println("A iniciar transação...");

        try {
            // Cenário A: Pode disparar SaldoInsuficienteException
            conta.levantar(150.0); 
            
            // Cenário B: Pode disparar IllegalArgumentException
            // conta.levantar(-20.0); 

        } catch (SaldoInsuficienteException e) {
            // Captura e tratamento do erro de negócio
            System.err.println("Aviso do Banco: " + e.getMessage());
            
        } catch (IllegalArgumentException e) {
            // Captura do erro de parâmetro inválido
            System.err.println("Erro de Parâmetro: " + e.getMessage());
            
        } finally {
            // Este bloco roda SEMPRE, garantindo o encerramento seguro da sessão
            System.out.println("Encerrando a ligação com o terminal bancário. Obrigado.");
        }

        System.out.println("Aplicação continua a rodar normalmente após o tratamento!");
    }
}
```

### Recurso Avançado: Multi-Catch (Java 7+)

Se o tratamento de dois erros for idêntico, pode agrupá-los no mesmo bloco `catch` utilizando o caractere pipe (`|`), reduzindo a duplicidade de código:

Java

```java
try {
    // Código de risco
} catch (IOException | SQLException e) {
    System.err.println("Erro crítico de infraestrutura: " + e.getMessage());
}
```

## Links relacionados

- [[Java - Programação Orientada a Objetos]]
    
- [[Java - Modificadores de Acesso]]
    
- [[Java - Fluxos de Dados (Streams)]]
    
- [[Java - Manipulação de Arquivos (Classe File)]]