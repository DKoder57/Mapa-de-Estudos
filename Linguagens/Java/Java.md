---
tags:
  - matriz
  - java
  - programação
área: Desenvolvimento de Sistemas / Java
status: draft
---

# ☕ Java — Matriz da Aba

> [!quote] Princípio: Documentar é transformar consumo em domínio.
> Arquivo de navegação central para todos os tópicos de Java do vault. Estruturado com base no conteúdo programático do guia de Introdução à Linguagem Java.

---

## 📚 Fontes

| Apostila / Documento                       | Cobertura                                                                      |
| :----------------------------------------- | :----------------------------------------------------------------------------- |
| Introdução à Linguagem de Programação Java | Módulos e tópicos de fundamentos, sintaxe, POO, Coleções, E/S, JDBC e Threads. |

---

## 🟢 Seção 1 — Introdução, Ambiente e Sintaxe Básica

> Conteúdos iniciais sobre a plataforma Java, configuração do ecossistema e regras de sintaxe.

| # | Nota | Tópicos |
| :--- | :--- | :--- |
| 1.1 | [[Java - Introdução e Plataforma]] | Pilares do Java (JVM, APIs, Linguagem), Histórico, Ciclo de vida (.java, bytecode, .class, java.exe) |
| 1.2 | [[Java - Terminologias Fundamentais]] | Compreensão e papéis do JDK, JRE, JVM e API Java |
| 1.3 | [[Java - Configuração de Ambiente e IDEs]] | Instalação do JDK, configuração permanente do PATH, e IDEs (Eclipse, NetBeans, IntelliJ IDEA, RAD) |
| 1.4 | [[Java - Estrutura do Programa e HelloWorld]] | Anatomia do código, declaração de pacotes (package), método main, classe System e comentários |
| 1.5 | [[Java - Diretrizes de Programação e Convenções]] | Regras de identificadores, diferenciação de maiúsculas/minúsculas, padrão camelCase e constantes |

---

## 🟡 Seção 2 — Tipos de Dados, Variáveis e Operadores

> Estudo dos tipos primitivos, escopo e inicialização de variáveis, além de operações aritméticas e de casting.

| # | Nota | Tópicos |
| :--- | :--- | :--- |
| 2.1 | [[Java - Tipos de Dados Primitivos]] | Os 8 tipos primitivos (byte, short, int, long, float, double, boolean, char) e alocação de memória |
| 2.2 | [[Java - Variáveis de Instância vs. Locais]] | Escopo de nível de classe versus variáveis locais de método, inicialização e valores padrão |
| 2.3 | [[Java - Operadores e Atribuição]] | Operador de atribuição (=), atribuição primitiva por literais e resultados de expressões |
| 2.4 | [[Java - Casting e Conversão de Tipos]] | Casting primitivo, tratamento de perda de precisão e regras de conversão automática pelo compilador |

---

<h2>🔵 Seção 3 — Estruturas de Controle e Repetição</h2>

> Controle de fluxo de execução utilizando estruturas de repetição (loops) e instruções de ramificação.

| # | Nota | Tópicos |
| :--- | :--- | :--- |
| 3.1 | [[Java - Estruturas de Repetição (Loops)]] | Estrutura tradicional do loop `for`, inicialização múltipla, expressões booleanas e incremento |
| 3.2 | [[Java - Loop Enhanced For (Aprimorado)]] | Iteração simplificada sobre matrizes e coleções, sintaxe `for (type itr-var : collection)` e tipos compatíveis |
| 3.3 | [[Java - Instruções de Ramificação]] | Uso dos comandos de desvio de fluxo no código: `break`, `continue` e `return` |

---

## 🟣 Seção 4 — Orientação a Objetos e Manipulação de Strings

> O núcleo do paradigma do Java: modelagem de entidades do mundo real, visibilidade e tratamento textual de alta performance.

| #   | Nota                                       | Tópicos                                                                                                         |
| :-- | :----------------------------------------- | :-------------------------------------------------------------------------------------------------------------- |
| 4.1 | [[Java - Programação Orientada a Objetos]] | Conceitos de Classes, Objetos, Métodos, Campos/Atributos e Instanciação (Exemplo Carro e TesteCarro)            |
| 4.2 | [[Java - Modificadores de Acesso]]         | Encapsulamento e níveis de visibilidade: public, protected, private e default (padrão)                          |
| 4.3 | [[Java - Manipulação de Strings]]          | A classe String, imutabilidade, sequência de caracteres e métodos essenciais (`length`, `replace`, `substring`) |
| 4.4 | [[Java - StringBuilder e Otimização]]      | Modificação dinâmica de strings eficiente utilizando a classe StringBuilder                                     |

---

## 🟤 Seção 5 — Coleções, E/S de Dados e Recursos Avançados

> Gerenciamento avançado de estruturas de dados, persistência em arquivos, conexão com bancos de dados e concorrência.

| #   | Nota                                                   | Tópicos                                                                                                         |
| :-- | :----------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------- |
| 5.1 | [[Java - Collections Framework (ArrayList e Vector)]]  | Matrizes expansíveis dinamicamente, indexação ordenada, iteração rápida e diferenças com a classe legada Vector |
| 5.2 | [[Java - Conjuntos (HashSet, TreeSet, LinkedHashSet)]] | Estruturas Set, eliminação de duplicatas, ordenação natural/customizada e iteração previsível                   |
| 5.3 | [[Java - Interfaces Comparable e Comparator]]          | Implementação do método `compare()` e ordenação customizada de objetos complexos                                |
| 5.4 | [[Java - Manipulação de Arquivos (Classe File)]]       | Verificação de existência, caminhos absolutos, leitura de propriedades e o pacote java.io                       |
| 5.5 | [[Java - Fluxos de Dados (Streams)]]                   | Leitura e escrita orientada a fluxos de bytes (`FileInputStream`) e fluxos de caracteres Unicode                |
| 5.6 | [[Java - Tratamento de Exceções]]                      | Blocos `try-catch-finally`, exceções verificadas (`IOException`, `FileNotFoundException`) e cláusula `throws`   |
| 5.7 | [[Java - Banco de Dados com JDBC]]                     | Conectividade JDBC 4.0, pacotes `java.sql` e `javax.sql`, e carregamento automático de drivers subjacentes      |
| 5.8 | [[Java - Programação Concorrente (Threads)]]           | Conceito de Multithreading, ciclo de vida de execução de uma Thread, estados e sincronização de processos       |


---
> [!NOTE] Padrão das notas filhas Todas as notas geradas a partir desta matriz devem seguir a estrutura padronizada: frontmatter YAML → conceito principal → callouts `[!NOTE]` / `[!TIP]` → exemplos práticos de código anotado → links de navegação de retorno.

## 📚 Referências Bibliográficas

- **BARNES, D. J.; KÖLLING, M.** _Programação orientada a objetos com java: uma introdução prática usando o bluej_. 4.ed. Pearson: 2009.
    
- **FELIX, R. (Org.).** _Programação orientada a objetos_. Pearson: 2017.
    
- **MEDEIROS, L. F. de.** _Banco de dados: princípios e prática_. Intersaberes: 2013.
    
- **ORACLE.** _Java Documentation_, 2021. Documentação oficial da plataforma Java. Disponível em: [https://docs.oracle.com/en/java/](https://docs.oracle.com/en/java/). 