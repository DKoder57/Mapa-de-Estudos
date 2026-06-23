---
tags: [java, io, streams, fluxos-de-dados, filereader, filewriter, bufferedreader] 
área: Desenvolvimento de Sistemas / Java
status: draft
---
# 🌊 Java - Fluxos de Dados (I/O Streams)

> Fonte: _Introdução à Linguagem de Programação Java_

## O Conceito de Stream em I/O

Em Java, a manipulação de dados de entrada e saída (Input/Output - I/O) baseia-se no conceito de **Stream** (Fluxo de Dados). Uma Stream representa uma sequência contínua e unidirecional de dados que flui entre uma **fonte** (disco, teclado, rede) e um **destino** (ecrã, ficheiro, memória).

Ao contrário da classe `File`, que lida apenas com os metadados do sistema, as Streams são utilizadas para **ler e escrever o conteúdo real** dos ficheiros.

- **Input Stream (Fluxo de Entrada):** Abre um canal para **ler** dados de uma fonte para a aplicação.
    
- **Output Stream (Fluxo de Saída):** Abre um canal para **escrever** dados da aplicação para um destino.
    

## Classificação dos Fluxos: Bytes vs. Caracteres

O Java divide o seu ecossistema de I/O (no pacote `java.io`) em duas grandes árvores hierárquicas, dependendo da forma como os dados são transmitidos.

### 1. Fluxos baseados em Bytes (Byte Streams)

Processam os dados individualmente, byte a byte (8 bits). São indicados para manipular **ficheiros binários**, tais como imagens, vídeos, áudios, ficheiros compactados (.zip) ou classes compiladas (.class).

- **Superclasses Abstratas:** `InputStream` e `OutputStream`.
    
- **Implementações Comuns:** `FileInputStream` e `FileOutputStream`.
    

### 2. Fluxos baseados em Caracteres (Character Streams)

Processam os dados caractere a caractere (16 bits), adaptando-se automaticamente ao mapa de codificação de texto do sistema (como UTF-8 ou Unicode). São as ferramentas ideais para manipular **ficheiros de texto** (.txt, .csv, .json).

- **Superclasses Abstratas:** `Reader` e `Writer`.
    
- **Implementações Comuns:** `FileReader` e `FileWriter`.
    

## Fluxos de Processamento (Buffered Streams)

Aceder diretamente ao disco rígido a cada byte ou caractere lido consome muitos recursos do processador e torna a aplicação extremamente lenta. Para otimizar a performance, o Java utiliza o padrão de projeto _Decorator_ através das classes de **Buffer** (memória intermédia).

Classes como o **`BufferedReader`** e o **`BufferedWriter`** envolvem um fluxo básico e criam um buffer interno de memória. Em vez de ler um caractere de cada vez do disco, o sistema lê um bloco massivo de dados para a memória e entrega-o instantaneamente à aplicação à medida que ela solicita.

- _Exemplo prático:_ O método `readLine()` do `BufferedReader` permite ler uma linha de texto inteira de uma só vez, até encontrar uma quebra de linha (`\n`).
    

## O Padrão `try-with-resources`

As Streams consomem recursos diretamente do Sistema Operacional. Se um fluxo não for explicitamente fechado após o uso através do método `.close()`, o ficheiro pode ficar bloqueado na memória, gerando vazamentos de recursos (_resource leaks_).

Desde o Java 7, a melhor prática arquitetural para gerir fluxos é o **`try-with-resources`**. Qualquer classe que implemente a interface `AutoCloseable` declarada dentro dos parênteses do `try` será **fechada automaticamente** pelo Java assim que o bloco terminar, mesmo que ocorra uma exceção no processo.

## Exemplo Prático Completo: Cópia e Processamento de Texto

O programa unificado abaixo demonstra como abrir um ficheiro de texto existente, ler o seu conteúdo linha por linha de forma performática através de um buffer, aplicar uma transformação no texto e escrever o resultado num novo ficheiro de destino:

Java

```java
package br.com.java.aula.io;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;

public class StreamProcessingDemo {
    public static void main(String[] args) {
        String arquivoOrigem = "entrada.txt";
        String arquivoDestino = "saida_processada.txt";

        System.out.println("A iniciar o processamento do fluxo de dados...");

        // Gerenciamento robusto com Try-With-Resources (Auto-Close)
        try (
            FileReader fr = new FileReader(arquivoOrigem);
            BufferedReader leitor = new BufferedReader(fr); // Acopla o buffer de leitura
            
            FileWriter fw = new FileWriter(arquivoDestino);
            BufferedWriter escritor = new BufferedWriter(fw) // Acopla o buffer de escrita
        ) {
            String linha;
            int contadorLinhas = 1;

            // Loop de leitura: lerLinha() retorna 'null' quando o ficheiro chega ao fim
            while ((linha = leitor.readLine()) != null) {
                // Modificação dos dados em tempo de execução
                String linhaModificada = "[Linha " + contadorLinhas + "] " + linha.toUpperCase();
                
                // Gravação no fluxo de saída
                escritor.write(linhaModificada);
                escritor.newLine(); // Adiciona a quebra de linha nativa do S.O.
                
                contadorLinhas++;
            }

            // Força a descarga de dados que possam ter restado no buffer para o disco
            escritor.flush(); 
            
            System.out.println("Processamento concluído com sucesso!");
            System.out.println("Total de linhas processadas: " + (contadorLinhas - 1));

        } catch (IOException e) {
            System.err.println("Erro crítico no fluxo de I/O: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

## Links relacionados

- [[Java - Manipulação de Arquivos (Classe File)]]
    
- [[Java - Manipulação de Strings]]
    
- [[Java - StringBuilder e Otimização]]
    
- [[Java - Programação Orientada a Objetos]]