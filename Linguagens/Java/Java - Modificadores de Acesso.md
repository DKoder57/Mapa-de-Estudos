---
tags: [java, modificadores-de-acesso, encapsulamento, visibilidade, classes, poo] 
área: Desenvolvimento de Sistemas / Java 
status: draft
---
# 🔑 Java - Modificadores de Acesso

> Fonte: _Introdução à Linguagem de Programação Java_

## O que são Modificadores de Acesso?

Os **modificadores de acesso** (_access modifiers_) são palavras-chave da linguagem Java que definem o **nível de visibilidade e acessibilidade** que outras classes terão em relação a uma classe, construtor, atributo ou método.

Eles representam a ferramenta prática para implementar o pilar do **Encapsulamento**, permitindo ao programador blindar o estado interno de um objeto e expor apenas as interfaces estritamente necessárias para o funcionamento seguro do sistema.

Java disponibiliza quatro níveis de visibilidade, definidos por três palavras-chave explícitas e um estado padrão (omissão):

## Tabela Comparativa de Visibilidade

|**Modificador**|**Dentro da própria Classe**|**Dentro do mesmo Pacote**|**Subclasses (Herança)**|**Resto do Sistema (Geral)**|
|---|---|---|---|---|
|**`public`**|Sim|Sim|Sim|Sim|
|**`protected`**|Sim|Sim|Sim|Não|
|**`default`** _(Sem modificador)_|Sim|Sim|Não|Não|
|**`private`**|Sim|Não|Não|Não|

## Detalhe dos Quatro Níveis de Acesso

### 1. `public` (Acesso Público)

A classe ou membro declarado como `public` fica totalmente exposto e acessível a **qualquer outra classe** em qualquer pacote dentro do projeto.

- _Uso comum:_ Classes principais, interfaces e métodos de controlo geral (ex: os métodos `getters` e `setters`, ou o método `main`).
    

### 2. `protected` (Acesso Protegido)

O modificador `protected` torna o membro acessível a todas as classes que pertencem ao **mesmo pacote** e também por todas as **subclasses (classes filhas)** que herdam da superclasse, mesmo que essas subclasses estejam localizadas em pacotes totalmente diferentes.

- _Uso comum:_ Métodos e atributos de suporte arquitetural que as classes filhas precisam de customizar ou reaproveitar via herança (`super`).
    

### 3. `default` / _Package-Private_ (Acesso por Omissão)

Ocorre quando **nenhum modificador de acesso é explicitamente escrito** antes da declaração. O Java define automaticamente o escopo como "nível de pacote". Isso significa que apenas as classes contidas no **mesmo pacote** podem ler ou invocar esse membro.

- _Uso comum:_ Componentes internos de um módulo que operam juntos dentro de uma mesma pasta de projeto, mas não devem ser exportados para o resto da aplicação.
    

### 4. `private` (Acesso Privado)

É o nível de restrição mais severo. Membros declarados como `private` são visíveis e acessíveis **exclusivamente de dentro da própria classe** onde foram criados. Nenhuma outra classe, nem mesmo as subclasses herdadas, conseguem interagir diretamente com eles.

- _Uso comum:_ Atributos de estado (variáveis de instância) para prevenir a corrupção de dados por manipulação externa direta.
    

## Exemplo Prático de Implementação

O exemplo estrutural abaixo demonstra como os diferentes modificadores coexistem e delimitam as fronteiras de acesso num objeto:

Java

```java
package br.com.java.aula.seguranca;

public class Conta {
    // 1. PRIVATE: Ninguém fora desta classe pode alterar ou ler o saldo diretamente
    private double saldo;
    
    // 2. DEFAULT: Classes dentro do pacote 'br.com.java.aula.seguranca' podem gerir o ID
    String idIdentificacao;
    
    // 3. PROTECTED: Esta classe e qualquer classe filha (ex: ContaCorrente) têm acesso directo
    protected String tipoConta;
    
    // Construtor Público
    public Conta(String idIdentificacao, String tipoConta) {
        this.idIdentificacao = idIdentificacao;
        this.tipoConta = tipoConta;
        this.saldo = 0.0;
    }

    // 4. PUBLIC: Qualquer parte do sistema pode invocar para efetuar um depósito válido
    public void depositar(double valor) {
        if (valor > 0) {
            this.saldo += valor; // Operação interna controlada
        }
    }
    
    // Getter público para expor o valor sob consulta segura
    public double getSaldo() {
        return this.saldo;
    }
}
```

### Tentativa de Acesso Externo:

Java

```java
package br.com.java.aula.externo;

import br.com.java.aula.seguranca.Conta;

public class SistemaExterno {
    public static void main(String[] args) {
        Conta minhaConta = new Conta("CNT-101", "Poupança");
        
        minhaConta.depositar(500.00); // OK! O método é público.
        System.out.println(minhaConta.getSaldo()); // OK! O método é público.
        
        // COMPILAÇÃO FALHA - ERROS DE LOGICA DE ACESSO:
        // minhaConta.saldo = 10000.0;    -> Erro: 'saldo' tem acesso privado.
        // minhaConta.idIdentificacao;    -> Erro: Não está no mesmo pacote (Default).
        // minhaConta.tipoConta;          -> Erro: Esta classe não herdou de Conta (Protected).
    }
}
```

## Regras Importantes sobre Classes Top-Level

Para classes declaradas diretamente no arquivo de código fonte (fora de outras classes):

- Elas só podem receber os modificadores **`public`** ou **`default`** (sem modificador).
    
- Uma classe top-level **nunca** pode ser declarada como `private` ou `protected`, pois isso impediria a máquina virtual ou o compilador de interagir com a estrutura base.
    
- Se uma classe for declarada como `public`, o nome do arquivo `.java` deve ser estritamente idêntico ao nome da classe.
    

## Links relacionados

- [[Java - Programação Orientada a Objetos]]
    
- [[Java - Diretrizes de Programação e Convenções]]
    
- [[Java - Variáveis e Tipos de Dados Primitivos]]