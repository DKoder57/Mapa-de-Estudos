---
tags: [java, estrutura, helloworld, oo, classes, sintaxe]
área: Desenvolvimento de Sistemas / Java
status: draft
---

# ☕ Java - Estrutura do Programa e HelloWorld

> Fonte: _Introdução à Linguagem de Programação Java_

---

## O Programa HelloWorld

Para compreender a estrutura fundamental de um programa em Java, analisa-se o clássico exemplo `HelloWorld`. A única função deste programa é exibir a mensagem `"Hello World! Oi mundo!"` diretamente no console do sistema.

```java
package br.com.java.aula;

/**
 * Exemplo de programa Java clássico.
 * Demonstração da estrutura básica de uma classe.
 */
public class HelloWorld {
    
    // O método main é o ponto de partida do programa
    public static void main(String[] args) {
        System.out.println("Hello World! Oi mundo!");
    }
}

```

## Anatomia do Código (Análise Linha a Linha)

O funcionamento interno e as regras de sintaxe deste programa baseiam-se em cinco componentes essenciais:

| **Componente** | **Elemento**                              | **Descrição**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| -------------- | ----------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **1**          | `package br.com.java.aula;`               | **Declaração de pacote.** A instrução `package` define um espaço de nomes (_namespace_) no qual as classes são armazenadas e organizadas com base na sua funcionalidade. Se omitida, os nomes das classes entram no pacote padrão (sem nome). Deve ser obrigatoriamente a primeira linha útil do programa.                                                                                                                                                                                                                                                   |
| **2**          | `public class HelloWorld`                 | **Declaração da classe.**<br><br>• `public`: Modificador de acesso que informa ao compilador que a classe é acessível globalmente.<br><br>• `class`: Palavra-chave reservada usada para declarar uma classe, seguida pelo identificador/nome (`HelloWorld`).                                                                                                                                                                                                                                                                                                 |
| **3**          | Comentários                               | Textos de documentação ignorados pelo compilador. Podem ser de duas formas:<br><br>• **Linha:** Começa com duas barras (`//`) e estende-se até ao fim da linha atual.<br><br>• **Bloco:** Começa com `/*` e termina com `*/`, podendo cobrir várias linhas.                                                                                                                                                                                                                                                                                                  |
| **4**          | `public static void main (String[] args)` | **Método principal (Função).** Ponto de partida síncrono para a execução.<br><br>• `public`: Modificador de acesso.<br><br>• `static`: Palavra-chave reservada que torna o método acessível e utilizável diretamente, mesmo que não exista nenhum objeto instanciado da classe.  <br><br>• `void`: Declaração de tipo de retorno que indica que o método não devolve nenhum valor. <br><br>• `String[] args`: Matriz (array) de strings que serve como argumento de entrada do método.<br><br>• `{}`: Chaves que delimitam todo o conteúdo/escopo do método. |
| **5**          | `System.out.println(...)`                 | **Instrução utilitária de saída.**<br><br>• `System`: Nome da classe nativa utilitária do Java.<br><br>• `out`: Objeto de fluxo padrão que pertence à classe `System`.<br><br>• `println`: Nome do método utilitário utilizado para enviar qualquer cadeia de caracteres (_String_) para o console, adicionando uma quebra de linha ao fim.                                                                                                                                                                                                                  |

## Classes e Objetos em Java

O Java é uma linguagem puramente **orientada a objetos**, possuindo construções nativas para representar elementos do mundo real. Todo programa Java possui, no mínimo, uma classe que define regras, estados e comportamentos.

As classes em Java são compostas fundamentalmente por:

- **Campos:** Atributos, propriedades ou variáveis que representam as características do objeto.
    
- **Métodos:** Funções que representam as ações ou comportamentos do objeto.
    

### Exemplo Conceitual: O Objeto Carro

Pense num carro do mundo real: ele possui propriedades (como cor e velocidade máxima) e funções (como correr e parar). No ecossistema Java, estruturamos essa abstração da seguinte forma:

Java

```java
public class Carro {
    // Atributos (Propriedades / Campos)
    String cor;
    int velocidadeMaxima;

    // Método (Função / Comportamento)
    public void infoCarro() {
        System.out.println("Cor do carro: " + cor);
        System.out.println("Velocidade Máxima: " + velocidadeMaxima + " km/h");
    }
}
```

Para executar e testar essa estrutura, criamos uma classe de teste contendo o método de entrada (`main`) responsável por instanciar a estrutura do objeto na memória:

Java

```java
public class TesteCarro {
    public static void main(String[] args) {
        // Instanciação de um objeto real a partir do molde da classe Carro
        Carro meuCarro = new Carro();
        meuCarro.cor = "Vermelho";
        meuCarro.velocidadeMaxima = 200;

        // Chamada de método do objeto instanciado
        meuCarro.infoCarro();
    }
}
```

> [!NOTE] O Papel da JVM na Execução
> 
> Executar qualquer aplicação Java consiste em ordenar à Máquina Virtual Java (JVM) que carregue a classe especificada e inicie o processamento a partir do método `main()`. O programa continuará a ser executado em memória de forma contínua até que todo o código contido no escopo do `main` seja completamente concluído.

## Links relacionados

- [[Java - Introdução e Plataforma]]
    
- [[Java - Terminologias Fundamentais]]
    
- [[Java - Configuração de Ambiente e IDEs]]