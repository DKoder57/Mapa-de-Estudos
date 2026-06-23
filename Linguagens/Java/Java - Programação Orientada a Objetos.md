---
tags: [java, poo, orientacao-a-objetos, classes, objetos] 
área: Desenvolvimento de Sistemas / Java 
status: draft
---
# 🧩 Java - Programação Orientada a Objetos

> Fonte: _Introdução à Linguagem de Programação Java_

## O Paradigma Orientado a Objetos (POO)

Java foi desenhado desde a sua génese em 1995 por James Gosling como uma linguagem puramente **Orientada a Objetos**. O paradigma da POO visa aproximar a estrutura do código ao mundo real, organizando o sistema em unidades autónomas chamadas **Objetos**, que agrupam características (dados) e comportamentos (rotinas/funções).

Em vez de focar numa execução linear e procedural, o desenvolvimento em Java estrutura-se na interação entre estes objetos através do envio de mensagens (chamadas de métodos).

## 1. Os Conceitos Fundamentais: Classe vs. Objeto

A relação entre uma classe e um objeto é a base de todo o ecossistema Java.

- **Classe:** É o molde, planta (_blueprint_) ou especificação técnica. A classe define quais os atributos (características) e métodos (comportamentos) que os objetos daquele tipo possuirão. Ela não ocupa espaço em memória para dados reais, apenas dita as regras de estrutura.
    
- **Objeto:** É a instância física e real de uma classe. Quando criamos um objeto utilizando a palavra-chave `new`, o Java aloca espaço na memória Heap para armazenar os valores específicos daquela instância.
    

Java

```java
// A Classe (O Molde)
class Caneta {
    String cor;
    boolean tampada;

    void rabiscar() {
        if (tampada) {
            System.out.println("Erro: Não posso escrever com a caneta tampada.");
        } else {
            System.out.println("A rabiscar em " + cor);
        }
    }
}

// Instanciação (A criação do Objeto)
Caneta minhaCaneta = new Caneta();
minhaCaneta.cor = "Azul";
minhaCaneta.tampada = false;
minhaCaneta.rabiscar(); // Executa o comportamento
```

## 2. Os Quatro Pilares da POO em Java

Para que um sistema seja considerado genuinamente orientado a objetos, ele deve implementar quatro pilares arquiteturais.

### A. Abstração

Consiste em isolar e extrair apenas as propriedades essenciais de um elemento do mundo real para dentro do sistema, descartando detalhes irrelevantes para o contexto do negócio.

- _Exemplo:_ Numa classe `Carro` para um sistema de Oficina, precisamos de atributos como `quilometragem` e `historicoDeRevisoes`. Num sistema para um simulador de corrida, precisamos de `aerodinamica` e `pressaoDosPneus`.
    

### B. Encapsulamento

É o mecanismo de segurança que esconde os detalhes internos do funcionamento de uma classe e protege os seus dados contra acessos diretos e indevidos de componentes externos.

- **Modificadores de Acesso:** Usam-se as palavras-chave `private` para blindar os atributos e `public` para expor os métodos de controlo.
    
- **Métodos de Acesso (Getters e Setters):** Fornecem uma interface pública segura para ler (`get`) ou modificar (`set`) os atributos privados, permitindo aplicar validações de dados.
    

Java

```java
public class ContaBancaria {
    private double saldo; // Protegido contra manipulação direta externa

    // Getter seguro
    public double getSaldo() {
        return this.saldo;
    }

    // Setter com validação (Garante consistência do estado)
    public void depositar(double valor) {
        if (valor > 0) {
            this.saldo += valor;
        } else {
            System.out.println("Valor de depósito inválido.");
        }
    }
}
```

### C. Herança (`extends`)

Permite que uma nova classe (subclasse ou classe filha) reutilize, estenda e modifique os atributos e comportamentos definidos numa classe existente (superclasse ou classe mãe). Promove fortemente a reutilização de código e evita a duplicidade.

Java

```java
// Superclasse
public class Funcionario {
    String nome;
    double salario;

    public double getBonificacao() {
        return this.salario * 0.1; // 10% de bónus padrão
    }
}

// Subclasse
public class Gerente extends Funcionario {
    String senhaAcesso;

    // Sobrescrita de Método (Overriding)
    @Override
    public double getBonificacao() {
        return super.getBonificacao() + 1000.0; // Reaproveita a lógica mãe e adiciona valor
    }
}
```

### D. Polimorfismo

Significa "muitas formas". É a capacidade de um objeto de uma superclasse referenciar uma instância de qualquer uma das suas subclasses em tempo de execução, permitindo que a mesma mensagem invoque comportamentos diferentes baseados no tipo real do objeto instanciado.

O polimorfismo subdivide-se principalmente em:

1. **Polimorfismo de Sobrescrita (_Method Overriding_):** Ocorre com herança, onde o método da subclasse possui a mesma assinatura do método da superclasse, mas implementação diferente (como demonstrado na classe `Gerente`).
    
2. **Polimorfismo de Sobrecarga (_Method Overloading_):** Ocorre na mesma classe, onde vários métodos possuem o mesmo nome, mas assinaturas com parâmetros diferentes (tipos ou quantidades distintas).
    

## Exemplo Prático Completo: Ecossistema POO

O exemplo unificado abaixo demonstra o fluxo de herança, encapsulamento e polimorfismo dinâmico em Java:

Java

```java
package br.com.java.aula.poo;

// 1. Definição da Superclasse Abstrata
abstract class Animal {
    private String nome;

    public Animal(String nome) {
        this.nome = nome;
    }

    public String getNome() { return nome; }
    
    // Método abstrato: força as subclasses a implementarem o seu próprio som
    public abstract void emitirSom();
}

// 2. Criação das Subclasses com Polimorfismo de Sobrescrita
class Cao extends Animal {
    public Cao(String nome) { super(nome); }

    @Override
    public void emitirSom() {
        System.out.println(getNome() + " diz: Cão a ladrar -> Au Au!");
    }
}

class Gato extends Animal {
    public Gato(String nome) { super(nome); }

    @Override
    public void emitirSom() {
        System.out.println(getNome() + " diz: Gato a miar -> Miau!");
    }
}

// 3. Classe Executável demonstrando o Polimorfismo Dinâmico
public class SistemaPet {
    public static void main(String[] args) {
        // Polimorfismo: Variáveis do tipo genérico 'Animal' apontando para objetos específicos
        Animal meuPet1 = new Cao("Rex");
        Animal meuPet2 = new Gato("Whiskers");

        // O mesmo método produz resultados completamente diferentes dependendo da instância real
        emitirSomDoAnimal(meuPet1); // Executa o latido
        emitirSomDoAnimal(meuPet2); // Executa o miado
    }

    // Método genérico que aceita qualquer tipo de Animal
    public static void emitirSomDoAnimal(Animal animal) {
        animal.emitirSom(); // Ligação dinâmica em tempo de execução
    }
}
```

## Links relacionados

- [[Java - Tipos de Dados Primitivos]]
    
- [[Java - Diretrizes de Programação e Convenções]]
    
- [[Java - Estruturas de Repetição (Loops)]]
    
- [[Java - Instruções de Ramificação]]