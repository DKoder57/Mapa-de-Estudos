---

tags: [ui-ux, prototipagem, handoff, drawio, figma, acessibilidade, documentação]

área: UI/UX

status: draft

---
# Prototipagem Detalhada, Handoff e Feedback

[[UI-UX]] → Módulo 3 

## Tipos de Protótipo

|Tipo|Características|Ferramenta|
|---|---|---|
|**Baixa fidelidade**|Simples, rápido; transmite ideia geral; sem preocupação com detalhes|Papel, Figma, Excalidraw|
|**Alta fidelidade**|Detalhado, próximo ao produto final; testa funcionalidades e interações|Figma, Flutterflow|

**Quando usar cada um:**

- **Baixa fidelidade** → primeiras etapas, validação rápida de conceito
- **Alta fidelidade** → fases avançadas; ideia bem definida; precisão em cores, fontes e interatividade

---

## Draw.io — Diagramas e Fluxos

Ferramenta para criar **diagramas** que planejam e organizam o fluxo de um projeto. Funciona offline; interface drag-and-drop; colaboração em tempo real.

**Aplicações práticas:**

- Fluxogramas de navegação
- Arquiteturas de sistemas (nuvem, banco de dados, servidores)
- Diagramas de casos de uso

### Como criar um fluxo de navegação no Draw.io

```
Elipse    → Tela de Splash (início)
Losango   → Decisão: "Usuário tem login?"
           ↳ Sim → Tela de Login
           ↳ Não → Tela de Cadastro
Retângulo → Processo: "Coletar dados do usuário"
           → Tela Principal → Decisão: "Escolher tipo de produto"
           → Telas específicas por escolha
```

> [!NOTE] Draw.io ≠ Figma Draw.io é para **planejamento e fluxos**. O Figma transforma esses fluxos em **design visual e interativo**.

---

## Princípios de Design Interativo

### Interações Simples e Eficazes (via JavaScript)

- `on hover` — elemento muda de cor ao passar o mouse
- `on click` — botão executa ação ao ser clicado
- `on drag` — objeto arrastado

> [!TIP] Menos é mais Interações devem ter propósito claro. Se um botão muda de cor no hover, **todos os botões similares** devem ter o mesmo comportamento (consistência visual).

### Coerência Visual

- Todos os ícones devem seguir o mesmo estilo
- Misturar estilos de ícones compromete a identidade visual

### Acessibilidade no Design Interativo

Responsabilidade dos desenvolvedores ao implementar o design:

- **Contraste e cor** — atender às diretrizes WCAG
- **Alt text** — descrições alternativas para leitores de tela
- **Navegação por teclado** — tabulações e atalhos
- **Suporte a leitores de tela** — botões, formulários e elementos interativos corretamente identificados

---

## Documentação do Design (para Handoff)

A documentação serve como **guia para todos os envolvidos no desenvolvimento**.

### O que incluir

```
✅ Wireframes detalhados de cada tela
✅ Paleta de cores com códigos hexadecimais e onde cada cor é aplicada
✅ Tipografia — fontes, tamanhos, pesos por contexto
✅ Especificações de espaçamento e alinhamento
✅ Diagramas de fluxo de navegação (Draw.io)
✅ Protótipos interativos (links do Figma)
✅ Informações de integração (APIs, banco de dados, permissões)
✅ Plano de coleta de feedback dos usuários
```

> [!TIP] Ferramentas para documentar
> 
> - **Notion** — organização de cores, telas, componentes com imagens e capturas
> - **GitHub Wiki** — centraliza decisões e orientações de design para equipes
> - **Figma** — protótipos interativos compartilhados com o time de dev

---

## Handoff — Entrega para Desenvolvimento

Etapa em que design finaliza protótipo e documentação, repassando ao time de dev para implementação.

### Boas Práticas no Handoff

**Organização clara** — todos os arquivos acessíveis: links para protótipos, arquivos de design (Figma), diagramas (Draw.io).

**Comunicação contínua** — design deve estar disponível após a entrega para esclarecer dúvidas.

**Documentos atualizados** — manter versionamento; todos trabalhando com a versão mais recente.

---

## Ferramentas do Ecossistema

|Ferramenta|Uso|
|---|---|
|**Figma**|Protótipos interativos de alta fidelidade; colaboração em tempo real|
|**Draw.io**|Diagramas de fluxo e arquitetura de sistema|
|**Flutterflow**|Plataforma low-code para protótipos funcionais sem muito código|
|**GitHub**|Controle de versão; Wiki; issues e pull requests para revisão|

---

## Colaboração Design × Desenvolvimento

O time de dev tem papel essencial na prototipagem:

- Valida **viabilidade técnica** das ideias
- Identifica limitações técnicas e sugere ajustes
- Transforma protótipos em **interações funcionais** (cliques, animações, transições)
- Evita problemas futuros ao colaborar desde o início

> [!NOTE] Feedback entre equipes Cada nova funcionalidade pode requerer mais tempo de desenvolvimento. Diálogo constante é essencial para ajustar expectativas e prioridades.

_Fonte: Material complementar — Prototipagem Detalhada (disciplina)_