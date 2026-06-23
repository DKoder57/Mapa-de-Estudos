---
tags: [java, io, file, arquivos, ficheiros, manipulacao-de-dados] 
área: Desenvolvimento de Sistemas / Java 
status: draft
---
# 📂 Java - Manipulação de Arquivos (Classe File)

> Fonte: _Introdução à Linguagem de Programação Java_

## A Classe `java.io.File`

A classe **`File`** (pertencente ao pacote original de entrada e saída `java.io`) é a representação abstrata de caminhos de arquivos (arquivos) e diretórios no sistema operacional.

É fundamental compreender que a classe `File` **não manipula o conteúdo interno** do arquivo (ou seja, ela não lê bytes ou escreve textos). A sua utilidade está estritamente ligada ao gerenciamento de **metadados** e propriedades estruturais do sistema de arquivos, permitindo verificar a existência de itens, criar diretórios, deletar arquivos, consultar permissões e listar caminhos.

## Caminhos Absolutos vs. Relativos

Ao instanciar um objeto da classe `File`, precisamos de passar uma string que representa o caminho alvo:

- **Caminho Absoluto:** Fornece a rota completa a partir da raiz do sistema operacional.
    
    - _Exemplo Windows:_ `new File("C:\\workspace\\dados.txt");` (Nota: Usa-se barras duplas `\\` para escapar a barra invertida).
        
    - _Exemplo Linux/Mac:_ `new File("/home/usuario/workspace/dados.txt");`
        
- **Caminho Relativo:** Fornece a rota baseada no diretório de execução atual da aplicação (geralmente a raiz do projeto).
    
    - _Exemplo:_ `new File("logs/output.txt");`
        

> 💡 **Boa Prática:** Para garantir a portabilidade do código entre diferentes sistemas operacionais (Windows, Linux, macOS), utilize a constante estática `File.separator` no lugar de barras fixas. Ela adapta-se automaticamente ao caractere divisor do sistema onde o programa está rodando.

## Principais Métodos da Classe `File`

A tabela abaixo compila as operações mais relevantes utilizadas para inspecionar e gerenciar caminhos físicos:

|**Método**|**Tipo de Retorno**|**Descrição**|
|---|---|---|
|`exists()`|`boolean`|Verifica se o arquivo ou diretório realmente existe no disco.|
|`createNewFile()`|`boolean`|Cria fisicamente um novo arquivo vazio. Lança `IOException`.|
|`mkdir()`|`boolean`|Cria o diretório especificado pelo caminho.|
|`mkdirs()`|`boolean`|Cria o diretório especificado, incluindo todos os diretórios pais inexistentes na rota.|
|`delete()`|`boolean`|Exclui o arquivo ou diretório (o diretório deve estar vazio para ser deletado).|
|`isFile()`|`boolean`|Retorna `true` se o caminho apontar especificamente para um arquivo.|
|`isDirectory()`|`boolean`|Retorna `true` se o caminho apontar para um diretório/pasta.|
|`getName()`|`String`|Retorna apenas o nome do arquivo ou diretório (sem a rota completa).|
|`getAbsolutePath()`|`String`|Retorna o caminho completo (absoluto) do item.|
|`length()`|`long`|Retorna o tamanho do arquivo em bytes.|
|`listFiles()`|`File[]`|Retorna um array de objetos `File` contidos dentro de um diretório.|

## Exemplo Prático Completo

O programa abaixo demonstra o ciclo de vida de manipulação estrutural: verifica a existência de um diretório, cria-o se necessário, gera um arquivo interno, exibe as suas propriedades de metadados e lista o conteúdo da pasta:

Java

```java
package br.com.java.aula.io;

import java.io.File;
import java.io.IOException;

public class FileManagementDemo {
    public static void main(String[] args) {
        // 1. Definindo caminhos usando o separador dinâmico do sistema
        String caminhoDiretorio = "meu_projeto" + File.separator + "workspace";
        File diretorio = new File(caminhoDiretorio);
        
        // 2. Criação controlada de diretórios
        if (!diretorio.exists()) {
            boolean diretorioCriado = diretorio.mkdirs(); // Cria a árvore completa de pastas
            System.out.println("Diretório criado com sucesso? " + diretorioCriado);
        }

        // 3. Definição do arquivo dentro do diretório criado
        File arquivo = new File(diretorio, "relatorio.txt");

        try {
            // 4. Criação física do arquivo de texto
            if (!arquivo.exists()) {
                boolean arquivoCriado = arquivo.createNewFile();
                System.out.println("Arquivo físico gerado? " + arquivoCriado);
            } else {
                System.out.println("O arquivo já existe no destino.");
            }

            // 5. Exibição dos Metadados do Objeto File
            System.out.println("\n====== METADADOS DO ARQUIVO ======");
            System.out.println("Nome do arquivo: " + arquivo.getName());
            System.out.println("Caminho Absoluto: " + arquivo.getAbsolutePath());
            System.out.println("É um arquivo válido? " + arquivo.isFile());
            System.out.println("Tamanho atual: " + arquivo.length() + " bytes");
            System.out.println("Pode ser lido? " + arquivo.canRead());
            System.out.println("Pode ser modificado? " + arquivo.canWrite());

            // 6. Listagem do conteúdo do diretório pai
            System.out.println("\n====== CONTEÚDO DO DIRETÓRIO ======");
            File[] conteudo = diretorio.listFiles();
            if (conteudo != null) {
                for (File item : conteudo) {
                    String tipo = item.isDirectory() ? "[Diretório]" : "[Arquivo]";
                    System.out.println(tipo + " " + item.getName());
                }
            }

        } catch (IOException e) {
            System.err.println("Erro de E/S ao manipular o arquivo: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

## Nota Arquitetural: O Advento do Java NIO.2

Embora a classe `java.io.File` continue a ser amplamente utilizada e seja totalmente funcional, o **Java 7** introduziu uma nova e mais robusta API de manipulação chamada **NIO.2** (localizada no pacote `java.nio.file`).

Para novos projetos e sistemas corporativos modernos, recomenda-se a substituição gradual de `File` pelas interfaces:

- **`Path`**: Substitui o mapeamento de strings de caminho da classe `File`.
    
- **`Files`**: Uma classe utilitária massiva que realiza operações de cópia, movimentação, leitura e escrita direta de strings com melhor tratamento de erros e suporte a atributos avançados de sistemas de arquivos (como links simbólicos e permissões POSIX).
    

Java

```java
// Equivalência moderna em NIO.2
import java.nio.file.Path;
import java.nio.file.Paths;
import java.nio.file.Files;

Path caminhoModerno = Paths.get("pasta/arquivo.txt");
boolean existe = Files.exists(caminhoModerno);
```

## Links relacionados

- [[Java - Programação Orientada a Objetos]]
    
- [[Java - Modificadores de Acesso]]
    
- [[Java - Manipulação de Strings]]
    
- [[Java - Collections Framework (ArrayList e Vector)]]