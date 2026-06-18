---

tags: [ui-ux, projeto, figma, drawio, mobile, desktop, responsividade, apresentação]

área: UI/UX

status: draft

---
# Apresentação de Projeto UX

[[UI-UX]] → Módulo 5 

## Fluxo Completo de um Projeto UX

```
1. Pesquisa (Google Forms → 20 usuários)
2. Análise das respostas
3. Construção do fluxo (Draw.io)
4. Design visual (Figma — Desktop)
5. Adaptação mobile (Figma — Mobile)
6. Refinamentos e responsividade
7. Apresentação e entrega
```

---

## 1 — Interpretação das Respostas de Entrevista

### Análise das Respostas (exemplo — app de saúde, 20 usuários)

Dados coletados:

- Perfil e frequência de uso (idade, profissão, uso diário ou semanal)
- Satisfação e facilidade de uso (escala 1–5)
- Funcionalidades mais e menos apreciadas
- Sugestões de melhoria e feedback geral

> [!NOTE] Exemplo de insight Média de satisfação 3,6 → avaliação razoável com margem significativa para melhoria. Menu com 15% de rejeição → área prioritária para simplificação.

---

## 2 — Construção de Fluxo com Draw.io

Mapear como o usuário interage com a aplicação e identificar áreas de otimização.

### Estrutura do Fluxo (exemplo — app de saúde)

```
Tela Inicial
  ↓
Decisão: Usuário tem login?
  ├── Sim → Tela de Login → Dashboard
  └── Não → (loop para Login até autenticar)

Dashboard
  └── Escolha de Atendimento (ex.: clínica geral)
        └── Informação de tempo de espera
```

**Elementos usados no Draw.io:**

- **Elipse** — início/fim (tela de splash)
- **Losango** — decisão ("Usuário tem login?")
- **Retângulo** — processo ("Coletar dados do usuário")
- **Setas** — fluxo entre etapas

---

## 3 — Construção Visual no Figma — Desktop

**Objetivo:** traduzir o fluxo de navegação em design que ofereça clareza e acesso fácil às funcionalidades.

### Elementos criados

|Elemento|Descrição|
|---|---|
|**Frame**|Tela desktop padrão — resolução otimizada para visualização|
|**Menu**|Fundo semitransparente; botões em tons de verde e branco (identidade visual de saúde)|
|**Dashboard**|Cards de atendimento com informações essenciais de forma clara e organizada|
|**Sliders horizontais**|Navegação entre opções de atendimento|
|**Ícones visuais**|Orientam o usuário na interface|

---

## 4 — Construção Visual no Figma — Mobile

**Objetivo:** adaptar a interface para telas menores preservando usabilidade e identidade do desktop.

### Ajustes para Mobile

|Ajuste|Como foi feito|
|---|---|
|**Frame**|Smartphone — elementos redimensionados corretamente|
|**Menu overlay**|Ocupa a tela inteira quando ativado; não interfere no conteúdo principal|
|**Conteúdo verticalizado**|Dashboard com rolagem vertical para acesso facilitado|
|**Slider horizontal**|Rolagem horizontal; apresenta opções de atendimento de forma compacta|

---

## 5 — Refinamentos e Responsividade

**Foco dos ajustes:**

- **Espaçamento e alinhamento** — distribuição harmônica, navegação intuitiva
- **Paleta de cores e acessibilidade** — contraste conforme WCAG; componentes visíveis e utilizáveis
- **Interações e animações** — comportamento do menu overlay e slider refinado para navegação agradável

### Testes de Responsividade

Implementação de **breakpoints em CSS** para adaptação automática a diferentes dispositivos:

```css
/* Mobile first */
@media (min-width: 768px) { /* tablet */ }
@media (min-width: 1024px) { /* desktop */ }
```

Bootstrap agiliza a responsividade com classes pré-definidas.

---

## 6 — Colaboração e Entrega Final

**Figma para colaboração:**

- Compartilhamento em tempo real com outros designers para feedback
- Comunidade Figma e plugins para experimentação
- Conversão de design em código HTML/CSS via plugins

**Documentação entregue ao time de dev:**

- Fluxo de navegação (Draw.io)
- Protótipos interativos (Figma)
- Especificações técnicas (cores, fontes, espaçamentos)
- Breakpoints e regras de responsividade

---

## Diretrizes para Projetos UX (Como trabalhar em um projeto)

1. **Objetivo claro e mensurável** — ex.: aumentar taxa de conversão em 20% em 6 meses
2. **Escopo definido** — evita atrasos; use Scrum/Kanban para dividir em tarefas menores
3. **KPIs definidos desde o início** — monitorar impacto das melhorias
4. **Cronograma realista** — margem para imprevistos; Gantt para visualização
5. **Protótipos e documentação antes do dev** — alinhamento de toda a equipe

### Ferramentas Recomendadas por Área

|Área|Ferramentas|
|---|---|
|**Design**|Figma, Adobe XD, Sketch|
|**Desenvolvimento**|React + Bootstrap/Tailwind|
|**Gestão**|Trello, Jira|
|**Versionamento**|Git + GitHub (Wiki, issues, pull requests)|

> [!TIP] GitHub para UX/UI
> 
> - Wiki → documentar decisões e orientações de design
> - Issues → discutir tarefas e detectar melhorias
> - Pull requests → revisão contínua do código
> - Protótipos armazenados → acesso à versão mais recente sempre

_Fonte: Material complementar — Apresentação de um Projeto de UX / Como trabalhar em um projeto (disciplina)_