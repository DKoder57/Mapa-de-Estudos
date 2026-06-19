---

tags: [python, modulos, pacotes, import, namespace]
área: Python / Conceitos Gerais
status: draft

---
# 📦 Python - Modularização

> Fonte: _Programação Intermediária com Python — Módulo 1_ (Prof. Camila Laranjeira / UFMG / SEBRAE)

---

## O que é modularização?

Dividir um sistema em partes menores e mais gerenciáveis, cada qual responsável por um conjunto de tarefas relacionadas. Facilita manutenção, reutilização e colaboração.

No Python, a modularização existe em três níveis:

|Nível|Definição|
|---|---|
|**Função**|Bloco de código reutilizável dentro de um arquivo|
|**Módulo**|Um único arquivo `.py` com funções e estruturas relacionadas|
|**Pacote**|Uma pasta com múltiplos módulos organizados hierarquicamente|

---

## Criando um módulo

Um módulo é simplesmente um arquivo `.py`. Para importá-lo, o arquivo deve estar em um caminho reconhecido pelo interpretador.

```python
# pokedex.py
NUMERO_MAXIMO = 150
TIPOS = ('Normal', 'Fogo', 'Água', 'Planta')

def verificar_tipo(tipo):
    """Verifica se um tipo de Pokémon é válido."""
    return tipo in TIPOS
```

---

## Formas de importar

```python
# importar o módulo inteiro
import pokedex
pokedex.verificar_tipo('Fogo')

# importar com apelido
import pokedex as dex
dex.verificar_tipo('Água')

# importar elementos específicos
from pokedex import TIPOS, verificar_tipo
verificar_tipo('Normal')

# importar com apelido de membro
from pokedex import TIPOS as TIPOS_POKEMON

# importar tudo (não recomendado — polui o namespace)
from pokedex import *
```

> [!NOTE] Prefira importações explícitas `from modulo import *` dificulta rastrear a origem de cada elemento e pode causar conflitos de nome. Use apenas em casos específicos.

---

## Caminho de busca (`search path`)

O interpretador busca módulos nesta ordem:

1. Mesmo diretório do script que está importando
2. Diretórios em `PYTHONPATH` (variável de ambiente do sistema)
3. Diretórios padrão da instalação do Python (inclui `site-packages`)

```python
import sys
print(sys.path)   # lista todos os caminhos de busca

# adicionar caminho temporariamente (só para a sessão atual)
sys.path.append('/caminho/para/meus_modulos')
```

---

## Namespace e escopos

Ao importar um módulo com `import modulo`, apenas o **nome do módulo** entra no namespace atual — não seus membros internos. Isso evita conflitos.

```python
import pokedex           # 'pokedex' entra no namespace
pokedex.TIPOS            # acesso pelo nome do módulo

from pokedex import TIPOS  # 'TIPOS' entra diretamente no namespace
```

> [!TIP] `dir()` para inspecionar namespaces `dir()` sem argumentos lista os nomes do escopo atual. `dir(modulo)` lista os membros de um módulo.

---

## Criando pacotes

Um pacote é uma pasta contendo módulos e um arquivo `__init__.py`, que é executado ao importar o pacote.

```
meu_pacote/
├── __init__.py       ← inicialização do pacote
├── modulo1.py
└── modulo2.py
```

```python
# __init__.py
import meu_pacote.modulo1, meu_pacote.modulo2

# script.py
import meu_pacote
meu_pacote.modulo1.minha_funcao()
```

---

## Links relacionados

- [[Python - Ambientes Virtuais]]
- [[Python - Docstrings e Documentação]]
- [[Python - Escopo e Funções]]