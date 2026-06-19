---

tags: [python, ciência-de-dados, perfis, pandas, numpy]

área: Python

status: draft

---
# Python - Introdução à Ciência de Dados

> [!NOTE] Fonte: _Programação Intermediária com Python — Módulos 3 e 4_ — Prof. Camila Laranjeira / UFMG / SEBRAE (Módulo 3, seção 3.1)

## O que é Ciência de Dados?

Ciência de dados é uma área extremamente **horizontal** que combina conhecimento tecnológico e conhecimento especialista de domínio para extrair conhecimento e tomar decisões baseadas em dados. Não é uma profissão desempenhada por uma única pessoa — envolve um time com perfis complementares.

> "Modelar os acontecimentos passados para prever ocorrências futuras permite economizar tempo e dinheiro, e aumentar a efetividade de uma intervenção."

---

## Perfis Profissionais na Área de Dados

### Engenharia de Dados

Responsável por desenvolver e manter a arquitetura que comporta os dados e os torna acessíveis ao restante do time. Participa ativamente da **limpeza e integração** de dados, especialmente em contextos de Big Data.

**Habilidades gerais:** Programação, bancos de dados (estruturados e não estruturados), ferramentas de ETL (Extract, Transform, Load), sistemas distribuídos, cloud.

---

### Análise de Dados / Ciência de Dados

Grande parte do tempo é gasta na **limpeza de dados** — remover duplicatas, tratar dados faltantes, lidar com inconsistências. Depois, vem a exploração, transformação, modelagem e geração de _insights_.

**Habilidades gerais:** Programação, estatística, processamento de dados, visualização, aprendizado de máquina.

---

### Análise de Negócios

Possui experiência de negócio inigualável e serve de ponte entre tecnologia e negócio. Usa ferramentas como Power BI, Tableau e Python/R.

**Habilidades gerais:** Conhecimento do negócio, estatística, ferramentas de visualização, habilidades interpessoais.

---

## Python como Ferramenta Principal

Python destaca-se como a **linguagem mais usada** em ciência de dados pela sua versatilidade e vasto ecossistema de bibliotecas:

|Biblioteca|Função|
|---|---|
|`NumPy`|Arrays numéricos, operações vetorizadas|
|`Pandas`|Manipulação e análise de dados tabulares|
|`Matplotlib`|Visualização de dados base|
|`Seaborn`|Visualização estatística (built on Matplotlib)|
|`Plotly`|Visualizações interativas e dashboards|
|`scikit-learn`|Aprendizado de máquina|
|`SQLAlchemy`|ORM e acesso a bancos de dados|

---

## Tipos de Dados

|Tipo|Descrição|Exemplos|
|---|---|---|
|**Dados estruturados**|Estrutura bem definida, organizáveis em tabelas|CSV, bancos relacionais, planilhas|
|**Dados não estruturados**|Sem padrão rígido, mais complexos de analisar|Imagens, vídeos, áudio, texto livre|

> [!NOTE] Dados não estruturados geralmente exigem extração de características para serem transformados em dados estruturados antes da análise.

---

## Tipologia de Variáveis

Antes de qualquer análise, é essencial caracterizar os dados. O tipo de variável determina quais análises e métricas fazem sentido:

```
Variáveis
├── Numéricas (operações aritméticas fazem sentido)
│   ├── Discretas — valores inteiros, enumeráveis (ex: número de filhos)
│   └── Contínuas — qualquer valor num intervalo real (ex: temperatura)
└── Categóricas (rótulos de categorias)
    ├── Nominais — sem ordem natural (ex: cor dos olhos, spam/ham)
    └── Ordinais — com ordem natural (ex: tamanho P < M < G < GG)
```

---

## Casos de Uso Reais

- Triagem inteligente no atendimento ao consumidor
- Mapeamento de epidemias para intervenções de saúde pública
- Previsão de demanda em empresas de varejo
- Detecção de fraudes em transações financeiras
- Sistemas de recomendação (streaming, e-commerce)

---

## Links Relacionados

- [[Python - Estatística com Python]]
- [[Python - NumPy]]
- [[Python - Pandas]]
- [[Python - Visualização de Dados]]
- [[Python - SQL com Python]]
- [[Python - SQLAlchemy e ORM]]