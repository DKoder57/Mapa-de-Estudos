---
tags: [java, plataforma, jvm, bytecode, fundamentos]
área: Desenvolvimento de Sistemas / Java
status: draft
---

# ☕ Java - Introdução e Plataforma

> Fonte: _Introdução à Linguagem de Programação Java_

---

## O que é o Java?

O **Java** é uma das linguagens de programação mais populares do mundo, amplamente utilizada em aplicações críticas. Sua versatilidade permite o desenvolvimento de sistemas para os mais diversos ambientes:

- Aplicações desktop
- Sistemas para web
- Dispositivos móveis
- Cartões de crédito
- Televisões digitais e eletrodomésticos inteligentes (IoT)

Mais do que apenas uma linguagem de programação, o Java é uma **plataforma completa de desenvolvimento e execução**. Sua tecnologia é totalmente independente de sistema operacional e de hardware, estando presente nativamente no Windows, Linux, Unix, Mac e Solaris.

---

## Os três pilares do ecossistema

A infraestrutura e o funcionamento do Java são sustentados por três pilares essenciais:

| Pilar | Descrição |
| --- | --- |
| **JVM (Java Virtual Machine)** | A Máquina Virtual Java é o motor que executa o código compilado. |
| **APIs (Bibliotecas)** | Um conjunto completo de bibliotecas contendo classes prontas para uso. |
| **A Linguagem Java** | A sintaxe, as regras gramaticais e a estrutura da linguagem. |

---

## Histórico e objetivos

O Java foi desenvolvido por **James Gosling** na *Sun Microsystems* em 1995. Ele foi projetado como uma linguagem orientada a objetos para aplicativos de negócios de uso geral e aplicações interativas baseadas na Web. 

O principal objetivo do Java era fornecer uma alternativa ao C++ que fosse **independente de plataforma**. Por ser arquitetonicamente neutro, um programa escrito em Java pode ser executado em qualquer dispositivo ou sistema operacional que possua a máquina virtual instalada.

> [!NOTE] Como funciona a portabilidade?
> O programa Java não executa suas instruções diretamente no processador físico do computador. Em vez disso, ele roda de forma isolada sobre a **Java Virtual Machine (JVM)**, que traduz o código para o sistema operacional hospedeiro.

---

## O ciclo de vida do programa Java

O Java adota um modelo híbrido: o código-fonte precisa ser compilado primeiro, sendo convertido em um código intermediário chamado **código de bytes (bytecode)**. Durante esse processo, o compilador verifica erros de sintaxe e vincula outras bibliotecas necessárias ao programa.

O fluxo de desenvolvimento e execução segue quatro etapas fundamentais:

| Etapa | Ação | Descrição |
| :---: | :--- | :--- |
| **1** | **Criação do código** | O desenvolvedor escreve o código-fonte em um editor de texto ou IDE e salva o arquivo com a extensão `.java` (ex: `abc.java`). |
| **2** | **Compilação** | O arquivo `.java` é compilado usando o comando `javac` no terminal (ou automaticamente pela IDE). |
| **3** | **Geração de Bytecode** | O compilador gera um arquivo intermediário com a extensão `.class` (ex: `abc.class`) contendo os *bytecodes*. |
| **4** | **Execução** | O utilitário `java.exe` aciona a JVM, que lê o *bytecode* e o converte em linguagem de máquina nativa do dispositivo atual. |

---

## Links relacionados

- [[Java - Terminologias Fundamentais]]
- [[Java - Configuração de Ambiente e IDEs]]
- [[Java - Estrutura do Programa e HelloWorld]]