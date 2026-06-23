---
tags: [java, ambiente, jdk, path, ide]
área: Desenvolvimento de Sistemas / Java
status: draft
---

# 🛠️ Java - Configuração de Ambiente e IDEs

> Fonte: _Introdução à Linguagem de Programação Java_

---

## Instalação do JDK

Para desenvolver e compilar qualquer programa na linguagem Java, o primeiro passo obrigatório é realizar a instalação do **JDK (Java Development Kit)** no seu sistema operacional.

### Fluxo básico de instalação:
1. Faça o download da versão estável ou mais recente do Java através do site oficial da Oracle.
2. Na página de downloads, selecione a plataforma correspondente ao seu sistema (Windows, Linux, Mac, etc.) e descarregue o instalador adequado.
3. Após a conclusão do download, execute o ficheiro e siga as etapas padrão do assistente de instalação até ao fim.

---

## Configuração da variável de ambiente PATH

Após concluir a instalação do JDK, o sistema operacional precisa saber onde localizar as ferramentas de desenvolvimento (como o compilador `javac` e o executor `java`). Para que estes utilitários fiquem acessíveis globalmente a partir de qualquer diretório via terminal, é necessário configurar o **PATH** permanentemente.

### Configuração no Windows:
1. Escolha o menu **Iniciar** $\rightarrow$ **Configurações** $\rightarrow$ **Painel de Controle** e clique duas vezes em **Sistema**.
2. Selecione as configurações avançadas do sistema e clique no botão para editar as **Variáveis de Ambiente** (ou Variáveis do Sistema).
3. Procure pela variável chamada **Path** na lista de variáveis do sistema e selecione a opção de edição.
4. Adicione o caminho completo até à pasta `bin` da instalação do seu JDK (onde se encontram os ficheiros executáveis).
5. Salve e confirme todas as alterações antes de fechar as janelas.

> [!TIP] Testando a variável PATH
> Lembre-se de que a alteração só surtirá efeito em novas janelas de comando. Abra um novo Prompt de Comando (Terminal) após a configuração e digite o comando `javac -version` para garantir que o compilador foi reconhecido corretamente pelo sistema.

---

## Ambientes de Desenvolvimento Integrados (IDEs)

Embora qualquer programa Java possa ser escrito utilizando apenas um editor de texto simples (como o Bloco de Notas) e compilado manualmente através da Linha de Comando, a produção de aplicações profissionais exige a utilização de **IDEs**. Estas ferramentas automatizam tarefas, destacam erros de sintaxe e aumentam a produtividade.

O mercado possui excelentes opções de ambientes integrados populares:

| IDE | Características principais |
| --- | --- |
| **Eclipse** | Uma IDE totalmente gratuita que conta com uma longa lista de *plugins* e um excelente suporte por parte da comunidade. Possui um sistema de compilação automática em background que compila o código assim que o desenvolvedor salva o ficheiro. |
| **NetBeans** | Outro ambiente de desenvolvimento integrado gratuito de grande destaque no ecossistema, oferecendo ferramentas nativas robustas para a criação de aplicações estruturadas. |

---

## Links relacionados

- [[Java - Introdução e Plataforma]]
- [[Java - Terminologias Fundamentais]]
- [[Java - Estrutura do Programa e HelloWorld]]