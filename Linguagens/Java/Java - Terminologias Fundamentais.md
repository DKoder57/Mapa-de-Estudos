---
tags: [java, terminologia, jdk, jre, jvm, api]
área: Desenvolvimento de Sistemas / Java
status: draft
---

# ⚙️ Java - Terminologias Fundamentais

> Fonte: _Introdução à Linguagem de Programação Java_

---

## Componentes essenciais do ecossistema

Para programar e compreender o funcionamento do ecossistema Java, é fundamental dominar quatro siglas que representam os pilares da sua infraestrutura: **JDK**, **JRE**, **JVM** e **API**.

| Componente | Definição Geral |
| --- | --- |
| **JDK (Java Development Kit)** | Kit de Desenvolvimento Java (ferramentas para o programador). |
| **JRE (Java Runtime Environment)** | Ambiente de Execução Java (necessário para rodar o programa). |
| **JVM (Java Virtual Machine)** | Máquina Virtual Java (o executor do código de bytes). |
| **API Java (Application Programming Interface)** | Interface de Programação de Aplicações (bibliotecas prontas). |

---

## Detalhamento técnico das terminologias

### JDK (Java Development Kit)
O **JDK** é o Kit de Desenvolvimento Java. Trata-se de um superconjunto de software que todo programador precisa instalar para criar aplicações. Ele contém a JRE embutida, juntamente com várias ferramentas de desenvolvimento cruciais, tais como:
- Compilador Java (`javac`)
- Depuradores (*debuggers*)
- Ferramentas de empacotamento e implementação

### JRE (Java Runtime Environment)
O **JRE** é o Ambiente de Execução Java. Faz parte integrante do JDK, mas pode ser distribuído e usado de forma independente pelo usuário final para executar qualquer programa Java já compilado (código de bytes). Na prática, funciona como a implementação física e concreta da especificação da JVM.

### JVM (Java Virtual Machine)
A **JVM** é a Máquina Virtual Java. É um ambiente de software portátil adaptado para as mais diversas plataformas de hardware. 
- No tempo de execução de um programa, a JVM torna-se uma instância ativa do JRE na memória.
- Os **códigos de bytes (bytecodes)** funcionam como o idioma de máquina nativo e exclusivo para a JVM.
- Tal como um computador real, a JVM possui um conjunto próprio de instruções e manipula dinamicamente várias áreas de memória em tempo de execução.
- Para cada sistema e arquitetura de hardware (Windows, Linux, Mac), existe uma implementação correspondente da JVM fornecida pelos distribuidores.

### API Java (Application Programming Interface)
A **API Java** é o conjunto completo de classes utilitárias pré-escritas na linguagem Java que são executadas diretamente sobre a JVM. Estas estruturas auxiliam os programadores ao fornecer métodos padronizados para rotinas comuns, como:
- Realizar leitura e gravação no console do sistema (`System.out`)
- Armazenar e organizar objetos em estruturas de dados (coleções)
- Manipular arquivos, fluxos de dados e comunicações

---

> [!NOTE] Vantagens integradas da linguagem Java
> O ecossistema Java destaca-se por trazer recursos nativos e avançados de engenharia de software diretamente na sua plataforma:
> - **Multithreading:** Suporte interno para a execução de múltiplos fluxos de processamento simultâneos em paralelo.
> - **Gerenciamento de Memória:** Coleta automática de lixo (*Garbage Collector*) que desaloca objetos sem referências ativas e previne vazamentos de memória.
> - **Orientação a Objetos (OO):** Estrutura modular focada na representação de elementos do mundo real.
> - **Aplicações Distribuídas e Web:** Suporte integrado a ecossistemas baseados na Web (Applets, Servlets, JSP), comunicação por *sockets*, arquiteturas distribuídas (RMI, EJB) e protocolos de rede (HTTP, JRMP).

---

## Links relacionados

- [[Java - Introdução e Plataforma]]
- [[Java - Configuração de Ambiente e IDEs]]
- [[Java - Estrutura do Programa e HelloWorld]]