# Histórico de Prompts e Orientações — Sessão de Análise (Itapema/SC)

Registro completo dos prompts e orientações fornecidos pelo usuário ao longo
da sessão de análise do **Hackathon Seazone — Jovens Talentos AI Builder 2026**.
Os prompts estão preservados na íntegra, em ordem cronológica, com um breve
resumo da entrega/resultado de cada etapa.

---

## 1. Criação do script inicial de análise

> OpenCode, na pasta 'data', tem 5 arquivos '.csv' com dados do mercado imobiliário de Itapema (SC): 'Details_Itapema.csv (detalhes dos anúncios do Airbnb), Hosts_ids_Itapema.csv (dados do anfitrião, liga por owner_id com a Details), Mesh_Ids_Data_Itapema.csv (coordenadas e bairro, liga por ID do listing), Price_AV_Itapema.csv (preços, ocupação/ disponibilidade por data, liga por ID do listing), VivaReal_Itapema.csv (anúncios de venda - mercado de compra). Por favor, crie um script em python (usando pandas) para: carregar todas as bases e inspecionar os tipos de dados e valores nulos; Fazer a junção (merge) das bases do Airbnb (Details, Hosts, Mesh_Ids e Price_AV) em um único DataFrame consolidado; Calcular métricas-chave por anúncio a partir do Price_AV: Diária Média (ADR), Taxa de Ocupação, Receita Média Estimada (Receita = Diária Média x Dias Ocupados ou projeção anual); Exibir um resumo descritivo desse DataFrame consolidado e a estrutura do dataset de venda (VivaReal_Itapema.csv).

**Entrega:** `analise_imobiliaria.py` — carga/inspeção, merge, métricas por
anúncio (ADR, ocupação, receita), resumo descritivo e estrutura do VivaReal.
Correções de dados identificadas: duplicatas em `Hosts_ids` (snapshots por
owner) e em `Price_AV` (anúncio+data) — tratadas na agregação.

---

## 2. Resumo estatístico e contagem de registros

> opencode, com o cálculo das métricas agregadas por imóvel na base de diárias, como: receita total estimada, taxa de ocupação aproximada e preço médio da diária (ADR), apresente um resumo estatítico e a quantidade total de registros em cada base. Atualize os arquivos criados, se for necessário.

**Entrega:** adicionados ao script os blocos de *quantidade total de registros
por base* e *resumo estatístico dedicado das métricas agregadas* (ADR, ocupação,
dias ocupados, receita da janela e receita anual), incluindo totais somados.

---

## 3. Validação da tese "Compactos no Centro"

> Uma análise premiliminar interna sugeriu que apartamentos compactos (studios/ 1 quarto) na região do Centro seriam a aposta mais eficiente para a Seazone em Itapema. Escreva um script em python para validar ou refutar essa tese com os dados cruzados: agrupe a receita estimada, a taxa de ocupação e o valor da diária por bairro/ região (usando Mesh_Ids_Data_Itapema.csv) e por último de quartos/ tipologia (usando Details_Itapema.csv); Compare os resultados do Centro x Outros Bairros (ex: Meia Praia, Castelo Branco, etc.); Compare imóveis compactos (studio/ 1 quarto) x maiores (2+ quartos). Exiba tabelas comparativas com a receita média e a ocupação média de cada combinação de bairro + tipologia.

**Entrega:** `validacao_tese.py` — tabelas por bairro, por tipologia,
Centro × demais, matrizes bairro × tipologia (receita média, ocupação média,
nº de anúncios) e veredito numérico da tese.

---

## 4. Cruzamento com VivaReal e Gross Yield

> Agora cruze os achados de receita de aluguel por temporada com os dados de venda em 'VivaReal_Itapema.csv': Calcule o preço médio por m^2 de compra por bairro e tipologia na base do VivaReal; Estime o Gross Yield (Receita Anual Estimada de Temporada/ Preço Médio de Aquisição) para cada tipologia de imóvel e bairro em Itapema; Idenfique a combinação (Bairro + Tipologia) que apresenta a melhor relação entre retorno percentual (Yield) e facilidade de operação/ demanda.

**Entrega:** `analise_yield.py` — preço médio por m² (bairro e bairro ×
tipologia), Gross Yield por grupo, score composto retorno × demanda ×
liquidez e combinação vencedora (Tabuleiro dos Oliveiras 3q; Morretes 2q como
alternativa robusta).

---

## 5. Correlações e perfil dos top performers

> OpenCode, com base na base do Airbnb/ temporada cruzada: Quais atributos do imóvel (ex: nota de avaliação/ star rating, tempo/ status do host como superhost, taxa de resposta, tipo de anúncio, nº de banheiros/ quartos) possuem maior correlação com a alta receita e alta taxa de ocupação?; Mostre quais fatores diferenciam os 10% imóveis que mais faturam (top performes) do restante do mercado.

**Entrega:** `correlacoes_top.py` — matriz de correlação (Spearman) entre
atributos e alvos de receita/ocupação/ADR; perfil Top 10% × restante
(porte, ADR, ocupação, localização, superhost, reviews). Observação de dados:
`response_rate_shown`/`response_time_shown` 100% nulos (descartados).

---

## 6. Estruturação da decisão final

> Com base em todas as análises anteriores, me ajude a estruturar a decisão final: Tese: A tese de 'compactos no Centro' é sustentada ou refutada pelos dados? Justifique numericamente; Perfil ideal: Qual o melhor perfil para investir (bairro, tipologia, nº de quartos e tipo de anúncio)?; Simulação de Compra: Selecione uma opção representativa de imóvel à venda na base do VivaReal que atenda a esse perfil ideal, apresente o preço de compra e faça uma estimativa simples de retorno financeiro (Receita Anual Estimada x Custo de Aquisição). Monte a resposta em tópicos claros e objetivos, por favor, para fundamentar minha decisão no README.

**Entrega:** seção de decisão adicionada ao `README.md` — veredito da tese
(refutada por retorno; apoiada por ocupação), perfil ideal (Morretes 2q +
anúncio profissional/instant book) e simulação com imóvel real (listing
`2770039942`, R$ 750.000, Gross Yield 14,3% / Net 12,3%, payback ~8,1 anos).

---

## 7. Reescrita do README em formato profissional

> Preciso que você reescreva completamente o arquivo README.md da raiz do projeto para que ele fique em um formato profissional de documentação de ciência de dados/ negócios. Use as ferramentas de escrita para atualizar o README.md contendo a seguinte estrutura e conteúdos baseados nas análises que realizamos: 1. Link do Vídeo (Adicione a linha: [video de apresentação do desafio (até 2 min)], link_do_video_no_google_drive); 2. visão geral do projeto & Problema de Negócio: Explique o objetivo do repositório (Hackathon Seazone Jovens Talentos AI Builder 2026), o desafio de investimento imobiliário em Itapema (SC) e o propósito da recomendação final; 3. Metodologia e Tecnologias Utilizadas: Liste as linguagens, bibliotecas (ex: python, pandas, matplotlib...) e ferramentas de IA (opencode, gemini, chatgpt) utilizadas para a formulação de um plano de execução do desafio. Explique brevemente a limpeza de dados e o cruzamento das 5 bases presentes na pasta 'data/'; 4. Posição Sobre a Tese Interna (Compactos no Centro): responda claramente: os dados sustentam a hipótese de que apartamentos compactos no Centro são a aposta mais eficiente? Apresente números (médias de diária, ocupação e receita) que provem essa posição; 5. Recomendação de Investimento Seazone: Perfil Ideal: Defina o tipo de imóvel (tipologia, nº de quartos, tipo de anúncio); melhor localização: Indique o bairro/ região ideal e justifique com critérios de receita/ demanda; Fatores Explicativos: Destaque o que impulsiona a receita (ex: Superhost, avaliações, comodidades); 6. Simulação do Imóvel Selecionado: Escolha um anúncio real da base 'VivaReal_Itapema.csv' que atenda a esse perfil, apresente o preço de compra e calcule uma estimativa simples de retorno financeiro (Gross Yield = Receita Anual Estimada/ Preço de Compra); 7. Como executar o projeto: Crie um passo a passo claro para que qualquer avaliador possa rodar a análise no ambiente local (ex: dependências, ordem de execução dos scripts em python); 8. Estrutura do Repositório: Inclua um mapa de pastas explicando brevemente a função da pasta 'data/', da pasta 'ai-log/' e de quaisquer scripts ou notebooks criados. Certifique-se de formatar a resposta em Markdown limpo e estruturado, com tabelas e marcadores quando apropriado. mantenha o texto objetivo e voltado para tomada de decisão de negócios.

**Entrega:** `README.md` reescrito integralmente com as 8 seções solicitadas
(link do vídeo com placeholder, visão geral, metodologia/limpeza/cruzamento,
posição da tese com números, recomendação, simulação, execução e estrutura).

---

## 8. Consolidação em um único Jupyter Notebook

> Opencode, em vez dos arquivos arquivos '.py' padrão, estruture todas as análises e códigos em um único arquivo Jupyter Notebook com a extensão '.ipynb'. Organize e estruture o jupyter notebook separando os códigos em células bem documentadas, utilizando células de texto em markdown para explicar cada etapa da análise, os insights extraídos e as conclusões antes de cada bloco de código. Certifique-se de que o python tenha o pacote nbformat ou ipykernel instalado, caso for preciso gerar ou manipular o arquivo notebook. Ou seja, substitua todos os arquivos '.py' por um único arquivo '.ipynb' contendo todas as análises dos arquivos '.py', por favor. Atualize o README.md com as mudanças necessárias e indique como manipular o arquivo notebook.

**Entrega:** `analise_itapema.ipynb` (46 células — 20 código + 26 markdown,
seções 0 a 6) substituindo os 4 scripts `.py`; instalação de `nbformat`/
`ipykernel`/`nbclient`; notebook validado de ponta a ponta (sem erros);
README atualizado com instruções de execução e manipulação do notebook.

---

## 9. Solicitação atual

> Crie um arquivo chamado prompts_analise.md dentro da pasta 'ai-log/' e salve nele todo o histórico de prompts e orientações que usamos até agora nesta sessão, por favor.

**Entrega:** este arquivo — `ai-log/prompts_analise.md`.

---

*Fim do histórico de prompts da sessão.*