---
tags: [java, strings, manipulacao-de-strings, string-pool, imutabilidade] 
área: Desenvolvimento de Sistemas / Java 
status: draft
---
# 🧵 Java - Manipulação de Strings

> Fonte: _Introdução à Linguagem de Programação Java_

## O que é uma String em Java?

Em Java, uma **String** não é um tipo de dados primitivo (como `int` ou `char`), mas sim um **objeto** que representa uma sequência imutável de caracteres. A classe `String` pertence ao pacote `java.lang` (que é importado automaticamente em todos os ficheiros Java) e possui uma série de métodos integrados para a análise, comparação, extração e modificação de texto.

### O Conceito de Imutabilidade

Uma vez criado um objeto `String`, o seu valor **nunca pode ser alterado na memória**. Quando realiza uma operação que parece modificar uma String (como concatenar ou transformar em maiúsculas), o Java não altera a String original; em vez disso, ele cria um **novo objeto String** na memória com o resultado da modificação.

## O String Pool (Pool de Strings)

Para otimizar o uso da memória e aumentar a performance, o Java utiliza um mecanismo chamado **String Pool** (localizado dentro da memória Heap).

Quando uma String é criada de forma literal (usando aspas duplas), a JVM verifica primeiro se uma sequência idêntica já existe no Pool. Se existir, o Java reutiliza a referência existente em vez de alocar memória para um novo objeto.

- **Criação Literal:** `String s1 = "Java";` (Aponta para o String Pool)
    
- **Criação com `new`:** `String s2 = new String("Java");` (Força a criação de um novo objeto na memória Heap geral, fora do Pool)
    

## Principais Métodos de Manipulação

A tabela abaixo resume os métodos mais utilizados da classe `String` para manipulação de texto:

|**Método**|**Descrição**|**Exemplo**|
|---|---|---|
|`length()`|Retorna o número total de caracteres da String.|`"Java".length()` $\rightarrow$ `4`|
|`charAt(int index)`|Retorna o caractere na posição do índice especificado (base zero).|`"Java".charAt(2)` $\rightarrow$ `'v'`|
|`substring(int begin, int end)`|Extrai um pedaço da String, do índice inicial até o índice final (exclusivo).|`"Programação".substring(0, 4)` $\rightarrow$ `"Prog"`|
|`contains(CharSequence s)`|Verifica se a String contém a sequência de texto informada (retorna `boolean`).|`"Java".contains("av")` $\rightarrow$ `true`|
|`equals(Object anObject)`|Compara o conteúdo textual de duas Strings de forma exata.|`"Oi".equals("oi")` $\rightarrow$ `false`|
|`equalsIgnoreCase(String s)`|Compara o conteúdo textual ignorando maiúsculas e minúsculas.|`"Oi".equalsIgnoreCase("oi")` $\rightarrow$ `true`|
|`toUpperCase()` / `toLowerCase()`|Transforma todos os caracteres em maiúsculas ou minúsculas.|`"Java".toUpperCase()` $\rightarrow$ `"JAVA"`|
|`trim()`|Remove os espaços em branco em excesso no início e no fim da String.|`" Ola ".trim()` $\rightarrow$ `"Ola"`|
|`replace(char old, char new)`|Substitui todas as ocorrências de um caractere (ou subtexto) por outro.|`"Java".replace('a', 'o')` $\rightarrow$ `"Jovo"`|
|`split(String regex)`|Divide a String num array de sub-strings com base num delimitador.|`"A-B-C".split("-")` $\rightarrow$ `{"A", "B", "C"}`|

## Comparação de Strings: `==` vs `.equals()`

Um dos erros mais comuns no desenvolvimento Java é a utilização do operador de igualdade tradicional (`==`) para comparar o conteúdo de Strings.

- **Operador `==`:** Compara as **referências de memória** dos objetos. Ele apenas retorna `true` se as duas variáveis apontarem exatamente para o mesmo endereço físico na memória.
    
- **Método `.equals()`:** Compara o **conteúdo textual** (os caracteres reais) guardado dentro dos objetos.
    

Java

```java
String s1 = "Hello";
String s2 = "Hello";
String s3 = new String("Hello");

System.out.println(s1 == s2);      // true  (Apontam para a mesma instância no String Pool)
System.out.println(s1 == s3);      // false (s3 foi forçado para fora do Pool com 'new')
System.out.println(s1.equals(s3)); // true  (O conteúdo de texto é idêntico)
```

## Alternativas Mutáveis: `StringBuilder` e `StringBuffer`

Devido ao fator da imutabilidade, concatenar Strings consecutivamente dentro de um loop (utilizando o operador `+`) gera um grande desperdício de memória, pois múltiplos objetos intermediários são descartados pelo _Garbage Collector_.

Para cenários de modificações intensivas de texto, o Java fornece classes **mutáveis**:

1. **`StringBuilder`:** Altamente eficiente, ideal para uso local e mono-thread (não é sincronizada).
    
2. **`StringBuffer`:** Possui métodos sincronizados, sendo segura para uso em ambientes concorrentes multi-thread (Thread-Safe), porém ligeiramente mais lenta.
    

Java

```java
// Forma ineficiente em loops (Gera degradação de memória)
String texto = "";
for (int i = 0; i < 100; i++) {
    texto += i; 
}

// Forma otimizada usando StringBuilder
StringBuilder sb = new StringBuilder();
for (int i = 0; i < 100; i++) {
    sb.append(i);
}
String resultado = sb.toString(); // Converte de volta para String apenas no final
```

## Exemplo Prático Completo

O programa abaixo demonstra a aplicação integrada de várias operações de manipulação e análise de dados textuais em Java:

Java

```java
package br.com.java.aula.strings;

public class StringManipulationDemo {
    public static void main(String[] args) {
        String baseDados = "  ID_9987-PRODUTO_Teclado Mecânico-VALOR_250.50  ";
        
        // 1. Limpeza de espaços em branco nas extremidades
        String dadosLimpos = baseDados.trim();
        System.out.println("Texto Limpo: [" + dadosLimpos + "]");
        
        // 2. Fragmentação de dados usando Split
        String[] partes = dadosLimpos.split("-");
        System.out.println("\n--- Componentes Extraídos ---");
        for (String parte : partes) {
            System.out.println("Parte: " + parte);
        }
        
        // 3. Extração cirúrgica com Substring e IndexOf
        // Vamos extrair apenas o nome do produto dinamicamente
        int inicioProduto = dadosLimpos.indexOf("PRODUTO_") + "PRODUTO_".length();
        int fimProduto = dadosLimpos.indexOf("-VALOR");
        
        String nomeProduto = dadosLimpos.substring(inicioProduto, fimProduto);
        System.out.println("\nNome Isolado do Produto: " + nomeProduto);
        
        // 4. Transformação e Verificação
        String busca = "teclado";
        if (nomeProduto.toLowerCase().contains(busca.toLowerCase())) {
            System.out.println("Resultado da busca: O produto corresponde ao termo '" + busca + "'.");
        }
        
        // 5. Substituição de caracteres
        String nomeFormatado = nomeProduto.replace(" ", "_");
        System.out.println("Nome formatado para URL: " + nomeFormatado);
    }
}
```

## Links relacionados

- [[Java - Tipos de Dados Primitivos]]
    
- [[Java - Programação Orientada a Objetos]]
    
- [[Java - Estruturas de Repetição (Loops)]]