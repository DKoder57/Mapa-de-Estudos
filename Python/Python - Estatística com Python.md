---

tags: [python, ciência-de-dados, estatística,statistics, distribuição]

área: Python

status: draft

---
# Python - Estatística com Python

> [!NOTE] Fonte: _Programação Intermediária com Python — Módulos 3 e 4_ — Prof. Camila Laranjeira / UFMG / SEBRAE (Módulo 3, seção 3.2)

## O Módulo `statistics`

Módulo nativo do Python que oferece os resumos estatísticos mais fundamentais — equivalente a uma calculadora científica, sem pretensão de ser uma ferramenta de análise avançada.

```python
import statistics as st
```

---

## Tipologia de Variáveis

Antes de calcular qualquer métrica, caracterize seus dados:

|Tipo|Descrição|Exemplos|Métricas aplicáveis|
|---|---|---|---|
|**Numérica discreta**|Inteiros enumeráveis|nº de filhos, contagem|média, mediana, desvio padrão|
|**Numérica contínua**|Qualquer valor real|temperatura, percentual|média, mediana, variância|
|**Categórica nominal**|Rótulos sem ordem|spam/ham, cor dos olhos|contagem, frequência|
|**Categórica ordinal**|Rótulos com ordem|P < M < G < GG|frequência, mediana (às vezes)|

---

## Tendência Central

Estimam o "valor típico" de uma distribuição:

```python
dados = [15, 20, 20, 25, 30, 35, 200]   # note o outlier 200

st.mean(dados)          # média aritmética  — 49.3 (sensível a outliers)
st.median(dados)        # mediana           — 25   (resistente a outliers)
st.geometric_mean(dados)# média geométrica  — mais estável que aritmética
st.mode(dados)          # moda              — 20 (valor mais frequente)
```

> [!TIP] A **média aritmética é sensível a outliers** — um valor extremo a puxa para longe do centro. A **mediana** é mais estável para distribuições assimétricas ou com extremos.

### Quando usar cada uma

|Situação|Métrica recomendada|
|---|---|
|Dados simétricos sem outliers|Média aritmética|
|Dados com outliers ou assimetria|Mediana|
|Dados multiplicativos (taxas, crescimento)|Média geométrica|
|Dados categóricos|Moda|

---

## Espalhamento e Dispersão

Medem o quanto os dados se afastam da tendência central:

```python
st.variance(dados)   # variância — dispersão ao quadrado
st.stdev(dados)      # desvio padrão — raiz da variância, mesma unidade dos dados
```

**Interpretação do desvio padrão:**

- **Baixo** → dados concentrados em torno da média
- **Alto** → dados mais espalhados e variáveis

```python
# Exemplo prático
dados_sms = [80, 120, 45, 200, 65, 90]   # num_chars
media = st.mean(dados_sms)      # ≈ 100
dp    = st.stdev(dados_sms)     # ≈ 55

# "A maioria das mensagens varia entre 45 (100-55) e 155 (100+55) caracteres"
```

---

## Histograma (Conceito)

Gráfico de barras onde cada barra representa um intervalo de valores (**bin**) e a altura indica a frequência de dados naquele intervalo.

```python
import matplotlib.pyplot as plt

plt.hist(dados, bins=10)
plt.xlabel("Valores")
plt.ylabel("Frequência")
plt.title("Distribuição dos dados")
plt.show()
```

---

## Correlação entre Variáveis

Mede a relação conjunta entre dois atributos. Correlação ≠ causalidade.

```python
x = [1, 2, 3, 4, 5]
y = [2, 4, 5, 4, 5]

st.correlation(x, y)   # correlação de Pearson — entre -1 e 1
st.covariance(x, y)    # covariância — sem limite fixo, mais difícil de interpretar
```

|Valor de correlação|Interpretação|
|---|---|
|Próximo de **+1**|Correlação positiva forte|
|Próximo de **-1**|Correlação negativa forte|
|Próximo de **0**|Correlação fraca|

**Tipos de correlação:**

- **Positiva:** quando X aumenta, Y tende a aumentar
- **Negativa:** quando X aumenta, Y tende a diminuir
- **Fraca:** sem padrão claro entre X e Y

> [!NOTE] A **correlação de Pearson** é mais fácil de interpretar que a covariância porque seu resultado sempre está entre −1 e 1. A covariância pode assumir qualquer valor, tornando comparações difíceis.

---

## Resumo das Funções do `statistics`

```python
import statistics as st

# Tendência central
st.mean(x)           # média aritmética
st.median(x)         # mediana
st.geometric_mean(x) # média geométrica
st.mode(x)           # moda
st.multimode(x)      # todas as modas

# Dispersão
st.variance(x)       # variância amostral
st.pvariance(x)      # variância populacional
st.stdev(x)          # desvio padrão amostral
st.pstdev(x)         # desvio padrão populacional

# Correlação
st.correlation(x, y) # Pearson
st.covariance(x, y)  # covariância
```

---

## Links Relacionados

- [[Python - Introdução à Ciência de Dados]]
- [[Python - NumPy]]
- [[Python - Pandas]]
- [[Python - Visualização de Dados]]