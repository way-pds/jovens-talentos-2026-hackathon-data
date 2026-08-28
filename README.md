# Hackathon Seazone — Jovens Talentos AI Builder 2026

**Tema:** Análise de dados para decisão de investimento imobiliário em Itapema (SC)

> 🔗 **[Vídeo de apresentação do desafio (até 2 min)](link_do_video_no_google_drive)**

---

## 1. Visão Geral do Projeto & Problema de Negócio

Este repositório é a entrega do **Hackathon Seazone Jovens Talentos AI Builder 2026**.
O objetivo é usar **ciência de dados** para responder a uma pergunta real de
negócio de gestão de aluguéis por temporada:

> **Onde e em qual tipo de imóvel a Seazone deveria expandir sua operação em
> Itapema (SC), para maximizar o retorno sobre o capital investido?**

### O desafio de investimento

Itapema é um mercado aquecido de **aluguéis de temporada (Airbnb)** e de
**compra/venda de imóveis (VivaReal)**. Para decidir bem, é preciso cruzar dois
lados do mesmo mercado:

- **Lado demanda (locação):** quanto um imóvel fatura por noite (ADR), por
  quanto tempo fica ocupado e qual a receita anual estimada.
- **Lado oferta (compra):** a quanto esse imóvel é adquirido (preço/m²,
  preço total) e qual o **retorno percentual** (Gross Yield) dessa compra.

### O propósito da recomendação

Responder objetivamente: que **bairro**, **tipologia** e **estratégia de
anúncio** entregam a melhor relação entre **retorno (%)**, **demanda
(ocupação)** e **facilidade de operação**. A decisão final está sintetizada nas
seções 4, 5 e 6 e materializada em uma **simulação de compra com um anúncio
real** da base.

---

## 2. Metodologia e Tecnologias Utilizadas

### Ferramentas e stack

| Categoria | Ferramentas |
|---|---|
| **Linguagem** | Python 3.13 |
| **Bibliotecas** | `pandas`, `numpy`, `re`, `unicodedata` (dados) — a base foi preparada para `matplotlib`/`seaborn` para versões gráficas (não obrigatórias para o entregável) |
| **Engenharia de dados** | Leitura de CSV, tratamento de datas, remoção de duplicatas, normalização de categorias, merges |
| **IA / assistência** | opencode (agente de codificação) e Gemini, para formulação do plano de execução e revisão |

### Limpeza de dados

- **Codificação UTF-8** e conversão de colunas de data (`datetime`).
- **Duplicação em `Hosts_ids`** (vários snapshots por `owner_id`): mantido o
  **snapshot mais recente** por host (4.440 → 3.057 anfitriões únicos),
  evitando multiplicação de linhas no merge.
- **Duplicação em `Price_AV`** por (anúncio, data): colapsado para a
  **diária média por dia** antes de agregar (a ocupação máxima fica em 100%).
- **Sentinela de nota `0`** em `star_rating`/`guest_satisfaction_overall`
  convertida para `NaN` (evita viés de correlação).
- Campos inutilizáveis (ex.: `response_rate_shown`/`response_time_shown` com
  100% de nulos) descartados da análise, com `number_of_reviews_host` como
  proxy de performance do anfitrião.
- **Normalização de bairros** (acentos, maiúsculas e variações como
  "Meia praia"/"Jardim Praia Mar") para permitir a junção Airbnb × VivaReal.

### Cruzamento das 5 bases (`data/`)

| Arquivo | Papel no cruzamento |
|---|---|
| `Details_Itapema.csv` | Atributos do imóvel (quartos, banheiros, nota, reviews, tipo de anúncio) — base principal |
| `Hosts_ids_Itapema.csv` | Dados do anfitrião (superhost, anos, nº reviews) — liga por `owner_id` |
| `Mesh_Ids_Data_Itapema.csv` | Bairro + coordenadas — liga por `airbnb_listing_id` |
| `Price_AV_Itapema.csv` | Diária por data → ADR, ocupação e receita — liga por `airbnb_listing_id` |
| `VivaReal_Itapema.csv` | Mercado de venda: preço, área, condomínio — mercado de compra |

**Métricas-chave computadas (janela 06/01 a 20/04/2025, 105 dias):**

- **ADR** = diária média de cada anúncio
- **Taxa de ocupação** = dias ocupados / 105 dias
- **Receita anual estimada** = ADR × 365 × taxa de ocupação
- **Gross Yield** = Receita anual estimada / Preço médio de aquisição (por bairro + tipologia)

> Apenas **999 dos 4.441** anúncios Airbnb possuem registro de diárias — toda a
> análise de receita baseia-se nesse subconjunto monitorado e na projeção
> linear acima.

---

## 3. Posição Sobre a Tese Interna (Compactos no Centro)

> **Os dados REFUTAM a tese de "apartamentos compactos no Centro como a aposta
> mais eficiente" — sob a ótica de retorno sobre o capital. A tese sobrevive
> apenas sob a ótica de ocupação e de valor por m².**

### Números que sustentam a posição

| Indicador | Centro + Compacto (0-1q) | Melhor alternativa | Leitura |
|---|---|---|---|
| **Diária média (ADR)** | R$ 480,05 | R$ 1.507 (top 10%) | Compacto tem ADR baixo |
| **Taxa de ocupação** | **68,7%** (5º de 26 pares) | ~69-79% | Ponto FORTE da tese |
| **Receita anual média** | R$ 124.417 | R$ 505.968 (Sertãozinho 4+q) | 2,5× menor |
| **Receita por quarto** | R$ 89.300 | R$ 104.936 (compacto geral) | Bom, porém não o top |
| **Preço de aquisição / m²** | R$ 19.307 (caro) | R$ 8.175 (Morretes) | Aquisição penalizante |
| **Gross Yield** | **9,1%** | **14,3-19,7%** (Morretes/Tabuleiro) | Retorno % inferior |

### Conclusão numérica

Os compactos no Centro têm a **maior ocupação** e **bom retorno por metro
quadrado**, mas a receita anual absoluta é **2,5× menor** que os top
performers e o preço de compra por m² é **~2× mais caro** que o de Morretes.
O resultado líquido é um **Gross Yield de 9,1% — abaixo** dos 14,3% de
Morretes 2q e dos 14,9-19,7% de Tabuleiro dos Oliveiras. **Para maximizar o
retorno sobre o capital investido, investir em compactos no Centro não é a
aposta mais eficiente.**

---

## 4. Recomendação de Investimento Seazone

### Definição explícita dos critérios de decisão

Defini **"melhor investimento"** sob o critério do **maior Yield Líquido sobre o
capital investido, ajustado pela liquidez e pelo risco de vacância** — e não
apenas pela maior receita bruta total.

### Perfil ideal (resumo)

| Dimensão | Recomendação | Justificativa |
|---|---|---|
| **Tipologia / nº de quartos** | **Apartamento de 2 quartos** (3 quartos como 2ª opção) | 2q concilia preço de entrada acessível com demanda; 4+ quartos têm yield de apenas 3-6% |
| **Tipo de anúncio** | **Anúncio profissional + reserva instantânea** | Correlação positiva com receita (+0,21) e ocupação (+0,21); profissional soma ~17 p.p. de ocupação e +14,7% de receita |
| **Melhor localização** | **Morretes** | Gross Yield 14,3%, ocupação 55,9%, e amostragem robusta (60 Airbnb / 1.250 anúncios de venda) = retorno superior e operação confiável |

> **Alternativa "prêmio urbano":** Centro, 2 quartos — yield 12,6%, ocupação
> 61,3%, amostra sólida (67/92). Indicada apenas se a prioridade for localização
> no mercado premium, aceitando menor retorno sobre o capital.

### Fatores explicativos (o que impulsiona a receita)

Com base nas correlações (Spearman) da análise de correlações do notebook
(`analise_itapema.ipynb`, Seção 4):

- **Porte físico domina a receita bruta:** nº de quartos (r=+0,31),
  banheiros (+0,30), capacidade (+0,26) e diária (ADR, +0,59).
- **Operação profissional impulsiona ocupação e receita:** `is_professional`
  (+0,21) e `reserva instantânea` (+0,09).
- **Evaluation `star_rating` / superhost têm correlação FRACA ou negativa**
  com receita/ocupação nesses dados — nota alta e selo "guest favorite"
  associam-se a imóveis menores/mais baratos, portanto **não são o driver
  decisivo** de retorno.

**Conclusão sobre o que importa:** para retorno percentual, o que pesa é
**porte moderado (2 quartos) + preço de aquisição baixo (Morretes)** e
**estratégia de anúncio profissional**. Notas e superhost ajudam na imagem,
mas não são o motor do yield.

---

## 5. Simulação do Imóvel Selecionado

**Perfil selecionado: Morretes — Apartamento de 2 quartos** (melhor equilíbrio
verificado). Para ilustrar, escolhemos o anúncio **representativo (mediana)**
da base `VivaReal_Itapema.csv`:

| Campo | Valor |
|---|---|
| **Anúncio (listing_id)** | `2770039942` |
| **Bairro** | Morretes |
| **Tipologia** | Apartamento, 2 quartos |
| **Área útil** | 68 m² |
| **Preço de compra** | **R$ 750.000** |
| **Condomínio médio (região 2q)** | R$ 1.181/mês |
| **IPTU médio** | R$ 510/ano |

### Estimativa simples de retorno

| Item | Valor |
|---|---|
| **Receita anual de temporada** (grupo Morretes 2q) | R$ 107.281 |
| (−) Condomínio (R$ 1.181 × 12) | − R$ 14.175 |
| (−) IPTU | − R$ 510 |
| **Receita líquida anual estimada** | **R$ 92.596** |
| **Gross Yield** (R$ 107.281 / R$ 750.000) | **14,3%** |
| **Net Yield** (R$ 92.596 / R$ 750.000) | **12,3%** |
| **Payback (preço / receita líquida)** | **~8,1 anos** |

> A simulação confirma: um 2-quartos em Morretes por R$ 750 mil gera ~R$ 92,6
> mil/ano líquidos (12,3%), bem acima do yield dos compactos premium do Centro
> (9,1%) e com operação muito mais confiável que Tabuleiro dos Oliveiras.

---

## 6. Como Executar o Projeto

O projeto é um **único Jupyter Notebook** (`analise_itapema.ipynb`) com todas
as análises em células documentadas (markdown + código). Basta executá-lo de
cima para baixo.

### Pré-requisitos

- **Python 3.10+** instalado na máquina.
- Instalar as dependências:

```bash
pip install pandas numpy nbformat jupyter ipykernel
```

### Como abrir e executar

1. Na raiz do repositório, inicie o Jupyter:

   ```bash
   # Jupyter Notebook clássico
   jupyter notebook

   # ou Jupyter Lab
   jupyter lab
   ```

   > Também é possível abrir o `.ipynb` no **VS Code** (extensão *Jupyter*)
   > ou no **Google Colab** (upload do arquivo ou abertura via GitHub).

2. Abra o arquivo `analise_itapema.ipynb`.
3. Execute **Run ▶ Run All Cells** (menu *Kernel* › *Restart & Run All*) —
   o notebook roda de ponta a ponta, seção por seção.

### Estrutura do notebook (ordem de execução)

| Seção | Conteúdo |
|---|---|
| **0. Setup** | Instala dependências, importa libs e funções auxiliares |
| **1. Carga e Inspeção** | Carrega as 5 bases e inspeciona tipos/nulos |
| **2. Consolidação Airbnb** | Métricas por anúncio (ADR, ocupação, receita) + merge |
| **3. Tese "Compactos no Centro"** | Comparação bairro × tipologia e veredito |
| **4. Correlações & Top Performers** | Atributos-chave e perfil dos 10% que mais faturam |
| **5. Gross Yield** | Preço/m² e yield por bairro × tipologia (Airbnb × Venda) |
| **6. Simulação de Compra** | Imóvel real + estimativa de retorno (Gross/Net Yield) |

Cada célula de texto explica a etapa, os **insights** e as **conclusões**
antes do código. O notebook lê diretamente da pasta `data/` e **não** modifica
os arquivos originais.

### Manipular/editar o notebook

- **Adicionar células:** botão `+` na barra superior do Jupyter/VS Code.
- **Alterar uma análise:** edite a célula de código e execute novamente
  (`Shift+Enter` executa apenas a célula atual).
- **Recriar o arquivo do zero** (se necessário): `nbformat` já permite ler e
  gravar `.ipynb` — ex.: `python -c "import nbformat; n=nbformat.read('analise_itapema.ipynb',4); nbformat.write(n,'analise_itapema.ipynb')"`.

---

## 7. Estrutura do Repositório

```
.
├── README.md                     # Este documento + recomendação final de negócio
├── index.html                    # Descrição completa do desafio (fonte da Seazone)
│
├── data/                         # Cinco bases CSV (mercado imobiliário de Itapema)
│   ├── Details_Itapema.csv       # Anúncios Airbnb (atributos do imóvel)
│   ├── Hosts_ids_Itapema.csv     # Dados de anfitrião (owner_id)
│   ├── Mesh_Ids_Data_Itapema.csv # Bairro + coordenadas (airbnb_listing_id)
│   ├── Price_AV_Itapema.csv      # Diárias/ocupação por data (airbnb_listing_id)
│   └── VivaReal_Itapema.csv      # Anúncios de venda (mercado de compra)
│
├── analise_itapema.ipynb         # NOTEBOOK ÚNICO: todas as análises do projeto
│                                 # em células markdown + código (Seções 0 a 6)
│
└── ai-log/                       # (Requisito do desafio) registros das conversas com IA em texto
```

> **Nota:** a pasta `ai-log/` deve conter os logs textuais das interações com a
> IA (opencode/Gemini), conforme pedido nas regras de entrega do desafio.

---

## Próximos Passos & Melhorias Futuras

Com mais tempo de desenvolvimento disponível para o desafio, o próximo passo
natural seria **evoluir a análise para um dashboard interativo** das soluções,
utilizando ferramentas como **Streamlit**, **Dash** ou **Power BI**.

Um dashboard permitiria aos tomadores de decisão da **Seazone** explorarem os
dados de forma dinâmica e autônoma, em vez de dependerem de tabelas e gráficos
estáticos do notebook. Entre as capacidades previstas:

- **Filtros interativos de imóveis** por **bairro**, **faixa de preço**,
  **tipologia** (nº de quartos) e outras variáveis do imóvel.
- **Simulações financeiras em tempo real:** ajuste de premissas (ex.: taxa de
  ocupação projetada, ADR, alíquota de comissão, condomínio e IPTU) para
  recalcular instantaneamente **Gross/Net Yield** e **payback**.
- **Rankings e visões comparativas** de yield por bairro × tipologia,
  atualizados conforme os filtros aplicados.
- **Exportação de relatórios e cenários** para apoio à decisão de expansão da
  operação em Itapema.

Essa evolução transformaria o estudo analítico em uma **ferramenta de decisão
operacional**, permitindo à Seazone reproduzir a metodologia para novas praças
e atualizar premissas conforme o mercado evolui.

---

## Resumo Executivo

**Invista em apartamentos de 2 quartos em Morretes, operados com anúncio
profissional e reserva instantânea** — a combinação de maior retorno
percentual (yield 14,3% bruto / 12,3% líquido) com operação confiável. A tese
de "compactos no Centro" deve ser reposicionada como aposta de **alta ocupação
e valor por m²**, e não de retorno sobre o capital.

---

*Seazone — Jovens Talentos AI Builder 2026*
