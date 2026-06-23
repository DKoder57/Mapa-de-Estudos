---
tags: [java, jdbc, banco-de-dados, sql, persistencia, poo] 
área: Desenvolvimento de Sistemas / Java 
status: draft
---
# 🗄️ Java - Banco de Dados com JDBC

> Fonte: _Introdução à Linguagem de Programação Java_

## O que é o JDBC?

O **JDBC (Java Database Connectivity)** é uma API padrão do ecossistema Java (localizada nos pacotes `java.sql` e `javax.sql`) que fornece um conjunto de interfaces e classes para permitir a ligação entre aplicações Java e os mais diversos sistemas de gestão de bases de dados relacionais (SGBDR), como PostgreSQL, MySQL, Oracle, SQL Server e SQLite.

O grande benefício do JDBC é a **abstração**. Em vez de escrever códigos específicos para cada fabricante de banco de dados, o programador escreve código Java padrão baseado em interfaces. O fabricante do banco fornece uma biblioteca externa chamada **Driver**, que traduz as chamadas da API JDBC para a linguagem nativa do banco de dados específico.

## Os Componentes Principais do JDBC

O funcionamento do JDBC assenta em cinco interfaces e classes fundamentais:

1. **`DriverManager`:** Classe responsável por gerir a lista de drivers de bases de dados disponíveis e estabelecer a ligação física (através da URL de conexão) com o banco de dados.
    
2. **`Connection`:** Interface que representa a sessão de comunicação ativa com o banco de dados. É a partir dela que controlamos transações (`commit`, `rollback`) e criamos comandos SQL.
    
3. **`Statement` / `PreparedStatement`:** Interfaces utilizadas para enviar e executar comandos SQL (DML, DDL) na base de dados.
    
4. **`ResultSet`:** Interface que atua como uma tabela virtual de dados, armazenando o resultado de uma consulta SQL (`SELECT`) para ser percorrida pela aplicação.
    
5. **`SQLException`:** Classe de exceção verificada (_checked exception_) que captura qualquer falha de sintaxe SQL, falha de autenticação ou quebra de comunicação com o banco.
    

## Comparações Críticas: Statement vs. PreparedStatement

Para enviar instruções SQL ao banco, o JDBC oferece duas abordagens principais. A escolha entre elas é um fator crítico de segurança e performance:

|**Característica**|**Statement**|**PreparedStatement**|
|---|---|---|
|**Execução**|O SQL é compilado e avaliado pelo banco a cada execução.|O SQL é **pré-compilado** e guardado em cache pelo banco.|
|**Parâmetros**|Valores são concatenados diretamente na String do SQL.|Usa marcadores de posição (parâmetros `?`) dinâmicos.|
|**Performance em Loops**|Lenta (recompila o SQL repetidamente).|**Rápida** (reutiliza o plano de execução compilado).|
|**Segurança**|**Vulnerável a ataques de SQL Injection**.|**Seguro** (trata os parâmetros como dados puros, neutralizando injeções).|

### O Perigo do SQL Injection com `Statement`:

Java

```java
// VULNERÁVEL: Se o usuário digitar no input: "1 OR 1=1", terá acesso a todos os registros
String query = "SELECT * FROM usuarios WHERE id = " + inputUsuario;
```

### A Solução Segura com `PreparedStatement`:

Java

```java
// SEGURO: O caractere '?' blinda a estrutura da consulta SQL
String query = "SELECT * FROM usuarios WHERE id = ?";
PreparedStatement ps = conexao.prepareStatement(query);
ps.setInt(1, Integer.parseInt(inputUsuario)); // O dado é tratado estritamente como valor
```

## O Ciclo de Execução JDBC

O fluxo de trabalho padrão para interagir com uma base de dados via JDBC segue os seguintes passos estruturais:

1. Definir os dados de conexão (URL JDBC, Usuário e Senha).
    
2. Abrir a conexão (`Connection`).
    
3. Criar a estrutura do comando (`PreparedStatement`).
    
4. Atribuir os parâmetros (se houver) e executar (`executeQuery` para buscas ou `executeUpdate` para inserções/alterações).
    
5. Processar os resultados varrendo o cursor do `ResultSet`.
    
6. Garantir o encerramento seguro de todos os recursos abertos na memória (via `try-with-resources`).
    

## Exemplo Prático Completo: Operações CRUD

O programa unificado abaixo demonstra como estabelecer a ligação com um banco de dados fictício, criar uma tabela, inserir dados com proteção contra injeções e listar os registros usando as melhores práticas de fechamento automático de conexões:

Java

```java
package br.com.java.aula.jdbc;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class JdbcDatabaseDemo {

    // 1. Configurações da Base de Dados (Exemplo com banco em memória H2 ou SQLite)
    private static final String URL = "jdbc:h2:mem:testdb;DB_CLOSE_DELAY=-1"; 
    private static final String USER = "sa";
    private static final String PASSWORD = "";

    public static void main(String[] args) {
        System.out.println("Iniciando rotina de Banco de Dados com JDBC...");

        // 2. Criação da Estrutura Inicial (Tabela) usando Statement
        try (Connection conn = DriverManager.getConnection(URL, USER, PASSWORD);
             Statement stmt = conn.createStatement()) {
            
            String sqlCreate = "CREATE TABLE IF NOT EXISTS programadores (" +
                               "id INT AUTO_INCREMENT PRIMARY KEY, " +
                               "nome VARCHAR(100) NOT NULL, " +
                               "linguagem VARCHAR(50) NOT NULL)";
            stmt.execute(sqlCreate);
            System.out.println("Tabela 'programadores' verificada/criada com sucesso.");
            
        } catch (SQLException e) {
            System.err.println("Erro na criação da tabela: " + e.getMessage());
        }

        // 3. Inserção Segura de Dados (CREATE) usando PreparedStatement
        String sqlInsert = "INSERT INTO programadores (nome, linguagem) VALUES (?, ?)";
        
        try (Connection conn = DriverManager.getConnection(URL, USER, PASSWORD);
             PreparedStatement pstmt = conn.prepareStatement(sqlInsert)) {
            
            // Inserindo Registro 1
            pstmt.setString(1, "Carlos");
            pstmt.setString(2, "Java");
            pstmt.executeUpdate(); // Retorna o número de linhas afetadas

            // Inserindo Registro 2
            pstmt.setString(1, "Ana");
            pstmt.setString(2, "Python");
            pstmt.executeUpdate();

            System.out.println("Registros inseridos com sucesso via PreparedStatement.");

        } catch (SQLException e) {
            System.err.println("Erro na inserção de dados: " + e.getMessage());
        }

        // 4. Consulta e Navegação de Dados (READ) usando ResultSet
        String sqlSelect = "SELECT id, nome, linguagem FROM programadores ORDER BY id ASC";

        try (Connection conn = DriverManager.getConnection(URL, USER, PASSWORD);
             PreparedStatement pstmt = conn.prepareStatement(sqlSelect);
             ResultSet rs = pstmt.executeQuery()) { // O ResultSet é fechado automaticamente aqui

            System.out.println("\n====== LISTAGEM DE REGISTROS (RESULTSET) ======");
            
            // O método rs.next() move o cursor para a próxima linha. Retorna false quando chega ao fim.
            while (rs.next()) {
                // Recuperação dos dados informando o nome da coluna ou o índice do campo
                int id = rs.getInt("id");
                String nome = rs.getString("nome");
                String linguagem = rs.getString("linguagem");

                System.out.println("ID: " + id + " | Nome: " + nome + " | Linguagem Principal: " + linguagem);
            }
            System.out.println("------------------------------------------------");

        } catch (SQLException e) {
            System.err.println("Erro na consulta de dados: " + e.getMessage());
        }
    }
}
```

## Transações Manuais: Controlando o `ACID`

Por padrão, a interface `Connection` do JDBC vem configurada com o comportamento de `autoCommit = true`. Isto significa que cada comando executado é imediatamente salvo de forma definitiva no banco de dados.

Para operações complexas de negócio que exigem atomicidade (como uma transferência bancária, onde é preciso debitar de uma conta e creditar em outra, e ambas devem funcionar juntas ou falhar juntas), devemos desativar o autoCommit e controlar a transação manualmente:

Java

```java
try (Connection conn = DriverManager.getConnection(URL, USER, PASSWORD)) {
    // Desativa o salvamento automático para iniciar uma transação manual
    conn.setAutoCommit(false); 

    try (PreparedStatement debitar = conn.prepareStatement("UPDATE contas SET saldo = saldo - ? WHERE id = 1");
         PreparedStatement creditar = conn.prepareStatement("UPDATE contas SET saldo = saldo + ? WHERE id = 2")) {
        
        debitar.setDouble(1, 200.00);
        debitar.executeUpdate();

        creditar.setDouble(1, 200.00);
        creditar.executeUpdate();

        // Se ambos os comandos funcionarem perfeitamente, confirma as alterações no banco
        conn.commit(); 
        System.out.println("Transação concluída e consolidada!");

    } catch (SQLException e) {
        // Se houver qualquer falha em qualquer uma das partes, desfaz tudo o que foi feito nesta sessão
        conn.rollback(); 
        System.err.println("Falha na transação. Rollback executado com sucesso: " + e.getMessage());
    }
} catch (SQLException e) {
    e.printStackTrace();
}
```

## Links relacionados

- [[Java - Tratamento de Exceções]]
    
- [[Java - Modificadores de Acesso]]
    
- [[Java - Fluxos de Dados (Streams)]]
    
- [[Java - Collections Framework (ArrayList e Vector)]]