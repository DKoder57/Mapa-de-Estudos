---

tags: [python, venv, ambiente-virtual, pip]

área: Python / Conceitos Gerais

status: draft

---
# 🧪 Python - Ambientes Virtuais

> Fonte: _Programação Intermediária com Python — Módulo 1_ (Prof. Camila Laranjeira / UFMG / SEBRAE)

---

## Por que isolar ambientes?

Quando instalamos pacotes com `pip`, eles vão para o **ambiente global** do Python — compartilhado entre todos os projetos. Isso gera conflitos: um pacote atualizado para o Projeto B pode quebrar o Projeto A silenciosamente.

**Ambientes virtuais** criam espaços independentes com suas próprias versões de pacotes, sem interferir no sistema global.

> [!NOTE] Ferramenta nativa O módulo `venv` é nativo do Python (3.3+). Não é necessário instalar nada adicional.

---

## Fluxo completo com `venv`

### 1. Criar o ambiente

```bash
python -m venv nome_do_ambiente
```

Cria uma pasta com a estrutura do ambiente. O Python utilizado será o mesmo que executou o comando.

### 2. Ativar

```bash
# Linux / Mac
source nome_do_ambiente/bin/activate

# Windows
nome_do_ambiente\Scripts\activate
```

Após ativação, o nome do ambiente aparece entre parênteses no terminal: `(nome_do_ambiente)`.

### 3. Instalar pacotes

```bash
pip install pandas
pip install numpy==1.26.4      # versão específica
pip install "requests>=2.28"   # versão mínima
```

Todas as instalações ficam no ambiente local, em `nome_do_ambiente/lib/site-packages/`.

### 4. Exportar dependências

```bash
pip freeze > requirements.txt
```

Gera um arquivo listando todos os pacotes e versões do ambiente ativo.

### 5. Reproduzir em outro ambiente

```bash
pip install -r requirements.txt
```

Instala todas as dependências listadas de uma vez.

### 6. Desativar

```bash
deactivate
```

---

## Estrutura interna do ambiente

```
nome_do_ambiente/
├── bin/ (ou Scripts/ no Windows)
│   ├── activate        ← script de ativação
│   ├── python          ← link para o interpretador
│   └── pip             ← gerenciador de pacotes local
├── lib/
│   └── python3.x/
│       └── site-packages/  ← pacotes instalados
└── pyvenv.cfg              ← configurações do ambiente
```

> [!TIP] Um ambiente por projeto Crie um arquivo `.gitignore` com a pasta do ambiente (ex: `venv/`) para não versionar os binários. Versionar apenas o `requirements.txt` é a prática correta.

---

## `pip freeze` vs. `pip list`

|Comando|Saída|
|---|---|
|`pip freeze`|`pacote==versão` — formato pronto para `requirements.txt`|
|`pip list`|Lista legível de pacotes instalados|

---

## Links relacionados

- [[Python - Modularização]]
- [[Python - Docstrings e Documentação]]