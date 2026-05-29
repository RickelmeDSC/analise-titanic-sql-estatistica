# Análise do Titanic — SQL + Estatística em Python puro

Análise exploratória do dataset do Titanic combinando **SQL (SQLite)** para consultar e agrupar os dados com **estatística descritiva implementada em Python puro** — média, mediana, moda, variância e desvio-padrão calculados na mão, sem usar funções prontas (`.mean()`, `.median()` etc.), para entender o que cada medida significa por dentro.

## Objetivo

Praticar, num único projeto de ponta a ponta:

- modelagem e carga de dados num banco **SQLite** (com `connection`/`cursor` explícitos);
- **10 queries SQL** de análise (`GROUP BY`, `CASE`, agregações, cruzamentos);
- as **5 métricas estatísticas** implementadas manualmente e validadas contra o pandas;
- interpretação dos resultados com narrativa, não só números.

## Stack

- **Python 3.14**
- **SQLite3** (módulo nativo) — banco de dados
- **pandas** — apenas para carregar/organizar dados e validar os cálculos
- **Matplotlib** — visualizações
- **Jupyter** — notebook

## Dataset

Titanic (público): 891 passageiros, 12 colunas (classe, sexo, idade, tarifa, porto de embarque, sobrevivência etc.).

## Principais achados

A taxa de sobrevivência geral foi de **38,4%** — a maioria morreu. O que mais influenciou quem viveu:

### Sexo foi o fator mais forte
Mulheres sobreviveram a **74%**, homens a **19%** — o protocolo "mulheres e crianças primeiro".

### A classe veio logo atrás

![Taxa de sobrevivência por classe](images/g1_sobrevivencia_classe.png)

1ª classe **63%**, 2ª **47%**, 3ª apenas **24%**. A classe se refletia na tarifa (1ª pagava ~6x mais), na idade (1ª ~13 anos mais velha) e até no porto de embarque.

### Classe e sexo juntos contam a história completa

![Sobrevivência por classe e sexo](images/g2_classe_sexo.png)

Nos extremos: **mulher de 1ª classe (97%)** vs **homem de 3ª classe (14%)**. E um achado marcante — uma **mulher da 3ª (50%) tinha mais chance que um homem da 1ª (37%)**: o sexo pesou mais que a classe.

### A média pode enganar (tarifas)

![Distribuição das tarifas](images/g3_distribuicao_tarifas.png)

A tarifa média foi **£32,20**, mas a mediana foi só **£14,45** — menos da metade. A distribuição é fortemente **assimétrica à direita**: a maioria pagou pouco, mas algumas tarifas altíssimas (até £512) puxam a média para cima. Em casos assim, a **mediana** representa melhor o passageiro típico.

## Lições de análise de dados

1. **Correlação não é causa** — Cherbourg "sobreviveu mais", mas só porque concentrava 1ª classe.
2. **A média pode enganar** — em distribuições assimétricas, prefira a mediana para o "típico".
3. **Cuidado com dados faltando** — as 177 idades ausentes concentravam-se na 3ª classe; ignorá-las distorceria a análise.

## Estrutura

```
analise-titanic-sql-estatistica/
├── README.md
├── requirements.txt
├── data/
│   └── titanic.csv          # dataset (o titanic.db é gerado pelo notebook)
├── images/                  # gráficos exportados
└── notebooks/
    └── analise_titanic.ipynb
```

## Como executar

```bash
# instalar dependências
py -m pip install -r requirements.txt

# abrir o notebook
py -m jupyter notebook notebooks/analise_titanic.ipynb
```

Rode as células de cima para baixo: o notebook cria o banco `data/titanic.db` a partir do CSV, executa as análises e regenera os gráficos em `images/`.
