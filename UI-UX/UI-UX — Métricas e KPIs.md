---

tags: [ui-ux, métricas, kpi, analytics, power-bi, dados]

área: UI/UX

status: draft

---
# Métricas e KPIs em UX

[[UI-UX]] → Módulo 5 

## O que são Métricas e KPIs?

**Métricas** — ferramentas para monitorar o desempenho de processos, produtos e serviços.

**KPIs** (Key Performance Indicators) — métricas principais que avaliam eficiência e sucesso de forma quantitativa. Facilitam a identificação de padrões, pontos críticos e melhorias necessárias.

---

## Tipos de Coleta de Dados

|Tipo|Descrição|Indicado para|
|---|---|---|
|**Streaming**|Processamento em tempo real; atualização contínua|Monitoramento de saúde, tráfego em tempo real|
|**Batch**|Coleta e processamento em intervalos regulares|Relatórios periódicos; mais econômico|

---

## Métricas Comuns em UX

|Métrica|O que mede|Como usar|
|---|---|---|
|**Taxa de Conversão**|% de usuários que completam uma ação desejada (compra, cadastro)|Baixa taxa → processo confuso ou design desmotivador|
|**Taxa de Retenção**|Usuários que continuam usando o produto após o primeiro contato|Baixa retenção → possíveis pontos de frustração|
|**Tempo de Tarefa**|Tempo para completar uma ação|Tempo > esperado → problemas na interface ou estrutura de conteúdo|
|**NPS** (Net Promoter Score)|Lealdade e disposição de recomendar (0–10)|Promotores (9–10), Neutros (7–8), Detratores (0–6)|
|**Tempo de Carregamento**|Rapidez de carregamento da página|Páginas lentas afastam usuários; otimizar imagens e layout|

---

## Ferramentas de Coleta e Análise

|Ferramenta|Capacidade|
|---|---|
|**Google Analytics**|Comportamento dos usuários, fluxo de navegação, testes A/B, engajamento|
|**Hotjar**|Mapas de calor, gravações de sessão — onde usuários clicam e interagem|
|**Crazy Egg**|Visualizações similares ao Hotjar|
|**Google Cloud Platform + BigQuery**|Processamento e análise de grandes volumes de dados; e-commerce em tempo real|
|**Power BI**|Relatórios detalhados, dashboards, visualizações dinâmicas|

---

## Visualização de Dados — Boas Práticas

- **Clareza** — simples e direto; destacar dados essenciais
- **Consistência** — padrão visual para facilitar comparações entre métricas
- **Interatividade** — filtros e ajustes que permitem ao usuário explorar os dados

---

## Power BI na Prática

### Fluxo básico de uso

```
1. Importar dados (Google Forms → Excel → Power BI)
2. Preparar no Power Query — limpeza e transformações
3. Criar medidas com DAX — ex.: média de satisfação dos usuários
4. Visualizar — gráficos de colunas clusterizadas, linhas, mapas de calor
5. Explorar — cruzar informações (ex.: idade × satisfação)
```

### Exemplos de Dashboards

**Dashboard de satisfação do usuário:** Gráficos de barras/linhas relacionando satisfação com aspectos específicos (atendimento, facilidade de uso, tempo de resposta).

**Dashboard de análise de usabilidade:** Dispersão e mapas de calor mostrando funcionalidades mais acessadas e onde usuários encontram dificuldades.

> [!TIP] Alertas automáticos no Power BI Configurar alertas para monitorar métricas críticas — ex.: queda na satisfação em aspecto importante — permite à equipe agir rapidamente.

---

## Python para Análise Personalizada

Para volumes maiores ou análises específicas:

```python
import pandas as pd
import matplotlib.pyplot as plt

# Carregar e analisar dados de satisfação
df = pd.read_csv("respostas_formulario.csv")
df["satisfacao"].hist()
plt.show()
```

Bibliotecas: **Pandas** (manipulação de dados), **Matplotlib** (visualização).

_Fonte: Material complementar — Métricas e KPIs (disciplina)_