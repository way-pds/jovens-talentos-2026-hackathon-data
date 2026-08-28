# **Plano de Ação Hackathon Seazone**

[https://gemini.google.com/app/0a469d41696164ec](https://gemini.google.com/app/0a469d41696164ec)

*User prompt: Gemini, me ajuda a me organizar para realizar a seguinte tarefa, por favor? Pode ser um lista passo a passo do que preciso fazer.*

Response: **Plano de Ação: Hackathon Seazone 2026**

| Etapa | Ação | Detalhes / Checklist |
| :---- | :---- | :---- |
| **1\. Preparação** | Ler o regulamento completo | Acessar o link do desafio completo ou abrir o arquivo index.html para entender todos os detalhes, critérios de avaliação e o prazo final. |
|  | Criar o Fork | Fazer o *fork* do repositório oficial para a sua conta do GitHub e garantir que a visibilidade do seu repositório seja **pública**. |
| **2\. Análise dos Dados** | Entender as bases em data/ | Mapear e relacionar as 5 tabelas (Details, Hosts, Mesh\_Ids, Price\_AV e VivaReal) usando as chaves de conexão indicadas (owner\_id e IDs dos listings). |
|  | Executar a análise | Utilizar ferramentas de dados (como Python/Pandas) para cruzar as informações de aluguel de temporada com as de mercado de venda em Itapema (SC). |
| **3\. Documentação com IA** | Salvar logs de IA | Salvar todos os históricos de conversas em texto com as ferramentas de IA utilizadas dentro da pasta ai-log/ no repositório. |
| **4\. Entrega Final** | Gravar o vídeo | Gravar um vídeo demonstrativo de no máximo **3 minutos**, subir no Google Drive (com permissão de acesso liberada) e colar o link na **primeira linha** do seu README.md. |
|  | Redigir o README.md | Escrever a recomendação final no README.md e incluir as instruções claras de como rodar a sua análise. |
|  | Submeter o projeto | Confirmar que todas as alterações foram commitadas/enviadas ao GitHub e preencher o formulário oficial de entrega. |

---

*User prompt: estou no passo 2, no opencode eu começo pedindo pra ele cruzar as informações contidas nas planilhas na pasta de dados e me retornar insights? Pode me ajudar com os prompts que mando pra ele? Acredito que preciso pedir pra ele cruzar as informações das planilhas disponíveis e me retornar análises que possam me ajudar a entender se a região se trata de um bom investimento para a Seazone. Assim: com base neles, preciso entregar uma recomendação de investimento para a Seazone, respondendo: Qual o melhor perfil de imóvel para investir na cidade? (tipologia, nº de quartos, tipo de anúncio) Qual a melhor localização em termos de receita? Quais características explicam as melhores receitas? Se a Seazone fosse investir hoje, o que eu compraria e por quê? Tenho que fazer uma estimativa simples de retorno e defender a decisão. Um dado a mais. Uma análise preliminar interna — ainda não validada — sugeriu que apartamentos compactos (studio/1 quarto) na região do Centro seriam a aposta mais eficiente para a Seazone. Minha recomendação final deve tomar posição sobre essa tese: os dados a sustentam ou não? Os termos "melhor", "perfil" e "localização" são propositalmente abertos — eu defino o critério e justifica. Não existe uma única resposta certa; querem ver como eu pensa e decido. Use as orientações contidas nesse arquivo.html como guia: https://seazone-tech.github.io/jovens-talentos-2026-hackathon-data/*

Response: Sim, o OpenCode (ou qualquer assistente de IA/código) pode te ajudar a fazer esse cruzamento, mas para obter os melhores resultados, o ideal é **guiar a IA em etapas estratégicas** em vez de pedir tudo de uma vez.

Aqui está uma estrutura de prompts dividida em passos lógicos que você pode copiar, ajustar e enviar sequencialmente para o OpenCode.

### **Passo 1: Entendimento e Limpeza dos Dados (Data Wrangling)**

Antes de pedir os insights, você precisa garantir que as tabelas estão conectadas e tratadas corretamente.

**Prompt 1:** "Estou analisando dados de mercado imobiliário em Itapema (SC) na pasta data/ para uma tese de investimento da Seazone. Crie um script em Python (usando Pandas) para ler os arquivos Details\_Itapema.csv, Hosts\_ids\_Itapema.csv, Mesh\_Ids\_Data\_Itapema.csv, Price\_AV\_Itapema.csv e VivaReal\_Itapema.csv.

> 1. Conecte os dados de aluguel por temporada usando as chaves owner\_id (para Hosts) e a chave do listing (para Mesh e Price).  
> 2. Verifique dados nulos, duplicados e tipos de colunas.  
> 3. Calcule métricas agregadas por imóvel na base de diárias (Price\_AV\_Itapema.csv), como: receita total estimada, taxa de ocupação aproximada e preço médio da diária (ADR). Apresente um resumo estatístico e a quantidade total de registros em cada base."

### **Passo 2: Teste da Tese Interna (Compactos no Centro vs. Mercado)**

Agora você direciona a IA para testar a hipótese levantada pela equipe interna da Seazone.

**Prompt 2:** "Uma análise preliminar interna sugeriu que **apartamentos compactos (studios/1 quarto) na região do Centro** seriam a aposta mais eficiente para a Seazone em Itapema. Escreva um script para validar ou refutar essa tese com os dados cruzados:

> 1. Agrupe a receita estimada, a taxa de ocupação e o valor da diária por **bairro/região** (usando Mesh\_Ids\_Data\_Itapema.csv) e por **número de quartos/tipologia** (usando Details\_Itapema.csv).  
> 2. Compare os resultados do Centro x outros bairros (ex: Meia Praia, Castelo Branco, etc.).  
> 3. Compare imóveis compactos (studio/1 quarto) x maiores (2+ quartos). Exiba tabelas comparativas com a receita média e a ocupação média de cada combinação de bairro \+ tipologia."

### **Passo 3: Identificar Alavancadores de Receita (O que explica o sucesso?)**

Entenda quais atributos do imóvel impulsionam os ganhos acima da média.

**Prompt 3:** "Com base na base do Airbnb/temporada cruzada:

> 1. Quais atributos do imóvel (ex: nota de avaliação/star rating, tempo/status do host como superhost, taxa de resposta, tipo de anúncio, nº de banheiros/quartos) possuem maior correlação com a alta receita e alta taxa de ocupação?  
> 2. Mostre quais fatores diferenciam os 10% imóveis que mais faturam (top performers) do restante do mercado."

### **Passo 4: Oportunidade de Compra x Retorno (Cruzamento com VivaReal)**

Para recomendar um investimento real, você precisa cruzar a receita de temporada com o preço de aquisição dos imóveis à venda.

**Prompt 4:** "Agora cruze os achados de receita de aluguel por temporada com os dados de venda em VivaReal\_Itapema.csv:

> 1. Calcule o preço médio por *m*2 de compra por bairro e tipologia na base do VivaReal.  
> 2. Estime o **Gross Yield** (Receita Anual Estimada de Temporada / Preço Médio de Aquisição) para cada tipologia de imóvel e bairro em Itapema.  
> 3. Identifique a combinação (Bairro \+ Tipologia) que apresenta a melhor relação entre **retorno percentual (Yield)** e **facilidade de operação/demanda**."

### **Passo 5: Definição da Recomendação e Seleção de Imóvel**

Peça para a IA sintetizar a decisão e simular a compra.

**Prompt 5:** "Com base em todas as análises anteriores, me ajude a estruturar a decisão final:

> 1. **Tese:** A tese de 'compactos no Centro' é sustentada ou refutada pelos dados? Justifique numericamente.  
> 2. **Perfil Ideal:** Qual o melhor perfil para investir (bairro, tipologia, nº de quartos e tipo de anúncio)?  
> 3. **Simulação de Compra:** Selecione uma opção representativa de imóvel à venda na base do VivaReal que atenda a esse perfil ideal, apresente o preço de compra e faça uma estimativa simples de retorno financeiro (Receita Anual Estimada x Custo de Aquisição). Monte a resposta em tópicos claros e objetivos para fundamentar minha decisão no README."

💡 **Dicas para esta etapa:**

> * **Grave as conversas:** Não se esqueça de copiar todas as suas interações (perguntas e respostas em texto) com o OpenCode/IA e salvar na pasta ai-log/ do seu projeto.  
> * **Defina os critérios:** Termos como "melhor" dependem do critério escolhido (ex: maior *yield* percentual vs. maior receita absoluta em R$). Deixe claro nos prompts qual critério você prioriza ao defender a escolha.

---

*User prompt: Como eu posso gerar um arquivo. txt com todos os meus prompts de comando no opencode? Eu posso pedir pra ele fazer isso?*

Response: Não é necessário solicitar ao assistente que gere o arquivo .txt manualmente por prompt. Por padrão, a própria ferramenta OpenCode salva automaticamente todo o histórico das interações e comandos no seu ambiente local ou na própria interface, dependendo do modo como você a está utilizando.

Você tem duas formas simples de gerar e salvar esse arquivo .txt para a pasta ai-log/:

### **Método 1: Exportar via Interface do OpenCode (Recomendado)**

Se você estiver utilizando o OpenCode via extensão ou interface web/desktop:

> 1. Acesse o histórico da conversa ou o painel lateral de sessões.  
> 2. Clique no menu de opções da conversa (ícone de três pontos ... ou engrenagem).  
> 3. Selecione **Export Chat** ou **Save Log** e escolha a extensão .txt ou .markdown.  
> 4. Mova o arquivo baixado para dentro da pasta ai-log/ do seu repositório.

### **Método 2: Copiar o Histórico e Criar o Arquivo via Terminal/VS Code**

Você pode pedir para o assistente formatar o histórico, mas o envio/salvamento final no disco deve ser feito por você ou pelo ambiente:

> 1. Abra um arquivo novo no seu editor de código (VS Code/OpenCode).  
> 2. Cole o texto completo das suas perguntas e das respostas recebidas.  
> 3. Salve o arquivo na pasta do seu projeto com o caminho:  
>    ai-log/prompts\_e\_respostas.txt

### **Posso pedir diretamente ao OpenCode para criar o arquivo?**

**Sim, se você estiver usando o OpenCode com permissão de execução de código/arquivos locais.**

Caso o assistente tenha acesso para executar comandos de sistema ou modificar o projeto no seu computador, você pode enviar o seguinte comando:

*"Crie um arquivo chamado prompts\_analise.txt dentro da pasta ai-log/ e salve nele todo o histórico de prompts e orientações que usamos até agora nesta sessão."*

Se a ferramenta tiver permissão de gravação direta na pasta do projeto, ela criará o arquivo automaticamente. Caso contrário, ela exibirá o texto na tela para você copiar e colar.

---

*User prompt: No arquivo README.md eu preciso deixar as informações em padrão desse tipo de arquivo em projetos, como: explicar certinho como usar, o que foi feito e o que foi preciso para desenvolver as análises, qual era o problema e o que foi decidido, etc. Como eu posso pedir pro OpenCode atualizar o arquivo pra mim?*

Response: Para pedir ao OpenCode que atualize o seu README.md com o padrão profissional completo do repositório, o segredo é fornecer uma **estrutura de seções bem definida** e pedir que ele preencha essa estrutura utilizando **os dados reais das suas análises**.

O OpenCode tem a capacidade de ler o código que você já rodou (arquivos em Python, resultados, gráficos e logs) e sobrescrever o arquivo README.md automaticamente.

### **O Prompt de Comando para o OpenCode**

Copie, ajuste os detalhes entre colchetes com os resultados reais da sua análise e envie este comando no OpenCode:

**Prompt:** "Preciso que você reescreva completamente o arquivo README.md da raiz do projeto para que ele fique em um formato profissional de documentação de ciência de dados / negócios.

Use as ferramentas de escrita para atualizar o README.md contendo a seguinte estrutura e conteúdos baseados nas análises que realizamos:

**1\. Link do Vídeo (Primeira Linha OBRIGATÓRIA):** Adicione a linha: \[Vídeo de Apresentação do Desafio (Até 3 min)\](LINK\_DO\_SEU\_GOOGLE\_DRIVE\_AQUI)

**2\. Visão Geral do Projeto & Problema de Negócio:** Explique o objetivo do repositório (Hackathon Seazone Jovens Talentos AI Builder 2026), o desafio de investimento imobiliário em Itapema (SC) e o propósito da recomendação final.

**3\. Metodologia e Tecnologias Utilizadas:** Liste as linguagens, bibliotecas (ex: Python, Pandas, Matplotlib) e ferramentas de IA (OpenCode) utilizadas. Explique brevemente a limpeza de dados e o cruzamento das 5 bases presentes na pasta data/.

**4\. Posição Sobre a Tese Interna (Compactos no Centro):** Responda claramente: Os dados sustentam a hipótese de que apartamentos compactos no Centro são a aposta mais eficiente? Apresente números (médias de diária, ocupação e receita) que provem essa posição.

**5\. Recomendação de Investimento Seazone:**

> * **Perfil Ideal:** Defina o tipo de imóvel (tipologia, nº de quartos, tipo de anúncio).  
> * **Melhor Localização:** Indique o bairro/região ideal e justifique com critérios de receita/demanda.  
> * **Fatores Explicativos:** Destaque o que impulsiona a receita (ex: Superhost, avaliações, comodidades).

**6\. Simulação do Imóvel Selecionado:** Escolha um anúncio real da base VivaReal\_Itapema.csv que atenda a esse perfil, apresente o preço de compra e calcule uma estimativa simples de retorno financeiro (Gross Yield \= Receita Anual Estimada / Preço de Compra).

**7\. Como Executar o Projeto:** Crie um passo a passo claro para qualquer avaliador rodar a análise no ambiente local (ex: dependências, ordem de execução dos scripts em Python).

**8\. Estrutura do Repositório:** Inclua um mapa de pastas explicando brevemente a função da pasta data/, da pasta ai-log/ e de quaisquer scripts ou notebooks criados.

Certifique-se de formatar a resposta em **Markdown limpo e estruturado**, com tabelas e marcadores quando apropriado. Mantenha o texto objetivo e voltado para tomada de decisão de negócios."

### **Dicas para a execução:**

> 1. **Ative a referência de arquivos no OpenCode:** Caso precise referenciar diretamente arquivos no seu projeto durante a digitação, você pode usar a sintaxe @README.md ou @data/ no terminal/TUI para garantir que o OpenCode considere o contexto correto.  
> 2. **Substitua o Link do Vídeo:** Lembre-se de substituir o texto LINK\_DO\_SEU\_GOOGLE\_DRIVE\_AQUI no arquivo final pelo link do seu vídeo gravado (com acesso público/liberado via link).  
> 3. **Revisão:** Após o OpenCode salvar o arquivo, abra o README.md no seu editor, verifique se os cálculos batem com suas análises prévias e faça o commit para o GitHub:  
>    `git add README.md`  
>    `git commit -m "docs: atualiza README.md com recomendacao final e instrucoes"`  
>    `git push origin main`

---

*User prompt: gostaria que os arquivos '.py' fossem em formato jupyter notebook (.'ipynb'). É melhor de visualizar. Como posso pedir para o opencode fazer isso pra mim?*

Response: Para pedir ao OpenCode para converter ou criar análises diretamente em formato Jupyter Notebook (.ipynb), o ideal é especificar que a execução seja estruturada em células de código e markdown.

### **Prompt de Comando para o OpenCode**

Envie o comando abaixo para a ferramenta:

**Prompt:**

"Em vez de criar arquivos .py padrão, estruture todas as análises e códigos em um arquivo Jupyter Notebook com a extensão .ipynb (por exemplo, analise\_seazone.ipynb).

Organize o arquivo separando o código em células bem documentadas, utilizando células de texto em Markdown para explicar cada etapa da análise, os insights extraídos e as conclusões antes de cada bloco de código. Caso já existam arquivos .py criados na pasta, converta-os para este formato .ipynb."

### **Dicas para a execução:**

> * **Bibliotecas necessárias:** Certifique-se de que o seu ambiente Python tenha o pacote nbformat ou ipykernel instalado caso o assistente precise gerar ou manipular o arquivo do notebook localmente. Se necessário, rode:  
>   `pip install jupyter nbformat`

> * **Salvar na pasta correta:** Ao finalizar a geração do notebook, confirme se o arquivo .ipynb está na raiz do repositório ou em uma pasta apropriada (ex: notebooks/) e lembre-se de atualizar a instrução de execução no seu README.md indicando como abrir e rodar o notebook.

---

*User prompt: Agora quero pedir pro opencode commitar tudo o que foi feito para o repositório no git.*

Response: Para pedir ao OpenCode que faça o commit e o *push* de todas as alterações para o seu repositório remoto no GitHub, envie o seguinte comando:

**Prompt:**

"Por favor, execute os comandos do Git para salvar e enviar todas as nossas alterações para o repositório remoto:

> 1. Adicione todos os arquivos criados e modificados (.ipynb, README.md, arquivos na pasta ai-log/, etc.).  
> 2. Faça um commit com uma mensagem clara e estruturada no padrão Conventional Commits (ex: feat: adiciona analise em notebook e atualiza readme com recomendacao).  
> 3. Envie (*push*) as alterações para a branch principal do repositório no GitHub.

Mostre a saída dos comandos para confirmar que o envio foi concluído com sucesso."

### **Verificação Pós-Commit**

Após o OpenCode executar os comandos, você pode validar se deu tudo certo conferindo no terminal com:

`git status`

Se a resposta for nothing to commit, working tree clean, significa que todas as suas análises, notebooks, logs de IA e o README.md atualizado já estão salvos e visíveis no seu repositório do GitHub.

---

*User prompt: assim ficou o meu jupyter notebook em anexo. Senti falta de análises visuais, o que você acha?*

Response: Seu Jupyter Notebook está **muito bem estruturado**, organizado e defensável do ponto de vista analítico. As etapas de dados, deduplicação, cruzamento de métricas (ADR, Ocupação, Gross/Net Yield) e até a simulação financeira ficaram muito claras e corretas.

No entanto, **sua percepção está coberta de razão**: para um projeto de Hackathon (especialmente focado em apresentação de negócios para tomada de decisão), a **ausência de visualizações gráficas faz falta**. Gráficos ajudam os avaliadores a bater o olho e absorver os números cruciais em segundos (o que é vital no vídeo de 3 minutos e na leitura do repositório).

### **O que incluir para enriquecer o Notebook com Análises Visuais?**

Adicionar **4 a 5 gráficos estratégicos** espalhados pelas seções transformará seu notebook em um relatório completo. Abaixo estão as sugestões visuais ideais e como pedir para o OpenCode implementá-las:

> 1. **Seção 3 (Validação da Tese):**  
   * **Gráfico de Barras / Dispersão:** Comparativo de **Receita Anual x Taxa de Ocupação** por Bairro e Tipologia (mostrando visualmente como o Centro/Compacto tem alta ocupação, mas fica atrás em receita total).  
> 2. **Seção 4 (Correlações & Top Performers):**  
   * **Heatmap de Correlação (Seaborn):** Matriz de cores ilustrando as correlações de Spearman (destacando que número de quartos/banheiros e gestão profissional se destacam frente ao *superhost* ou nota).  
   * **Gráfico de Barras Duplo (Top 10% vs Restante):** Comparativo visual dos atributos (ex: ADR R$ 1.508 x R$ 689\) para explicitar a diferença dos imóveis que mais faturam.  
> 3. **Seção 5 (Gross Yield):**  
   * **Gráfico de Dispersão (Scatter Plot):** **Preço de Venda x Receita Anual** com o tamanho dos pontos representando o *Yield (%)* e as cores representando as regiões. Isso deixa evidente por que Morretes e Centro 2q vencem.

### **Como pedir para o OpenCode atualizar o Notebook?**

Você pode mandar o seguinte prompt no OpenCode para que ele insira as visualizações usando matplotlib e seaborn diretamente no seu .ipynb:

**Prompt para o OpenCode:** "Análisei o arquivo .ipynb criado e notei a falta de visualizações gráficas. Por favor, atualize o notebook adicionando células de código com gráficos usando matplotlib e seaborn para enriquecer a apresentação visual dos dados:

> 1. **Na Seção 3 (Validação da Tese):** Crie um gráfico de barras comparando a Receita Média Anual e a Taxa de Ocupação Média entre 'Compactos no Centro' vs 'Outras Tipologias e Bairros'.  
> 2. **Na Seção 4 (Correlações):** Gere um sns.heatmap colorido e legível para a matriz de correlação de Spearman entre os atributos do imóvel/host e a receita/ocupação. Adicione também um gráfico de barras comparando os atributos do **Top 10% Performers vs Restante**.  
> 3. **Na Seção 5 (Gross Yield):** Crie um gráfico de dispersão (scatter plot) ou de barras ordenado mostrando o **Gross Yield (%) por Bairro x Tipologia**, destacando visualmente as opções com melhor retorno sobre o capital (ex: Morretes 2q).

Configure um estilo limpo (sns.set\_theme(style='whitegrid')), títulos claros e rotule os eixos para que os gráficos fiquem com aspecto profissional. Após editar o notebook, execute o commit das alterações no Git."

---

*User prompt: No README eu havia pedido pra colocar o chatgpt como fonte de modelo de IA, junto com o Gemini. Mas verifiquei que não fiz nenhuma pergunta sobre o hackathon pro chatgpt pra você. Então, quero pedir pro opencode atualizar o readme.md e remover onde diz que usei o chatgpt.*

Response: Você pode pedir essa alteração diretamente no OpenCode com o comando abaixo. Ele fará a varredura no seu README.md, removerá as citações ou menções ao ChatGPT e atualizará o arquivo.

### **Prompt para o OpenCode**

**Prompt:**

"Por favor, leia o arquivo README.md da raiz do repositório e remova qualquer menção ao **ChatGPT** na seção de ferramentas de IA ou tecnologia utilizada. Mantenha apenas as menções às ferramentas reais que utilizamos para a análise (como Gemini / OpenCode).

Após a alteração, faça um commit no Git com a mensagem docs: remove mencao ao chatgpt no README.md e faça o push para o repositório remoto."

Isso garante que a documentação do seu projeto fique **100% precisa** e alinhada com os logs que você enviará na pasta ai-log/ (evitando divergências durante a avaliação do hackathon).

---

*User prompt: Ah\! Gostaria de acrescentar ao readme.md que, caso eu tivesse mais tempo para resolver o desafio, eu teria feito um dashboard iterativo das análises.*

Response: Você pode incluir essa melhoria na seção de **Próximos Passos**, **Melhorias Futuras** ou **Considerações Finais** do seu README.md. Essa adição é muito bem avaliada pelos examinadores, pois demonstra visão de produto, maturidade de engenharia/análise e clareza sobre o escopo do projeto.

### **Prompt para enviar ao OpenCode:**

**Prompt:**

"Por favor, atualize o arquivo README.md adicionando um tópico chamado **'Próximos Passos & Melhorias Futuras'** (ou incluindo nas considerações finais).

Escreva de forma profissional que, com mais tempo de desenvolvimento disponível para o desafio, o próximo passo seria **construir um dashboard interativo das análises** (utilizando ferramentas como *Streamlit*, *Dash* ou *Power BI*). Explique que o dashboard permitiria aos tomadores de decisão da Seazone filtrar interativamente os imóveis por bairro, faixa de preço, tipologia e premissas financeiras para simulações em tempo real.

Após atualizar o arquivo README.md, faça o commit e envie (*push*) para o repositório no GitHub."

### **Exemplo de como ficará o texto no README.md:**

`## 🚀 Próximos Passos & Melhorias Futuras`

`Caso houvesse mais tempo de execução para o desafio, as seguintes melhorias seriam implementadas:`  
`* **Dashboard Interativo:** Construção de um painel web interativo (via *Streamlit* ou *Dash*) para permitir a filtragem dinâmica de imóveis por bairro, tipologia e faixas de preço, com simulação flexível de *Yield* em tempo real.`  
`* **Modelo Preditivo de Precificação:** Treinamento de um algoritmo de *Machine Learning* para estimar a receita diária de novos imóveis a partir de suas características específicas.`

---

*User prompt: Gemini, você acha que alguma pergunta ficou sem resposta ou algo ficou faltando ser feito de acordo com o que é pedido no desafio? https://seazone-tech.github.io/jovens-talentos-2026-hackathon-data/*

Response: Cruzando **todas as perguntas obrigatórias do enunciado oficial** com a estrutura do seu Jupyter Notebook e com o seu README.md, o seu projeto cobre a essência do desafio, **mas há 3 pontos cruciais que exigem atenção** para garantir nota máxima na avaliação:

### **1\. Checklist dos Requisitos do Desafio (O que está 100% Ok)**

| Requisito do Desafio | Status | Onde está tratado |
| :---- | :---- | :---- |
| **Melhor perfil de imóvel** (tipologia, nº quartos, tipo de anúncio) | ✅ Coberto | Seções 3, 4 e 6 do Notebook |
| **Melhor localização em receita** | ✅ Coberto | Seções 3 e 5 |
| **Características que explicam a receita** | ✅ Coberto | Seção 4 (Correlação & Top 10%) |
| **Simulação de compra e estimativa de retorno** | ✅ Coberto | Seção 6 (Morretes 2q com Gross/Net Yield) |
| **Posicionamento sobre a tese "Compactos no Centro"** | ✅ Coberto | Seção 3 (Validou ocupação, refutou Yield) |
| **Uso de IA documentado em texto** | ✅ Coberto | Pasta ai-log/ |

### **2\. O que FICA FALTANDO ou precisa de ajuste urgente?**

#### **⚠️ Ponto 1: Link do Vídeo no README (CRÍTICO)**

No enunciado oficial do desafio, a regra exige que a **primeira linha do README.md** seja o link do vídeo de até 3 minutos no Google Drive.

> * **O que fazer:** Assim que gravar o vídeo, certifique-se de que a permissão de visualização no Drive esteja aberta ("Qualquer pessoa com o link") e cole o link no topo do README.md.

#### **⚠️ Ponto 2: Definição Explícita dos Seus Critérios de Decisão**

O enunciado destaca:

*"Os termos 'melhor', 'perfil' e 'localização' são propositalmente abertos — você define o critério e justifica."*

No notebook você justificou muito bem utilizando o **Gross/Net Yield (%)** e o **Score Composto (Retorno \+ Demanda \+ Liquidez)**.

> * **O que ajustar:** Garanta que essa justificativa fique **explícita no README.md** em uma frase como:  
>   *"Definimos 'melhor investimento' sob o critério do maior Yield Líquido sobre o capital investido ajustado pela liquidez/risco de vacância (e não apenas a maior receita bruta total)."*

#### **⚠️ Ponto 3: A Pasta ai-log/ em texto simples**

O desafio exige explicitamente que as conversas com a IA estejam salvas em **arquivos de texto** dentro da pasta ai-log/.

> * **O que ajustar:** Certifique-se de que os seus prompts e interações estejam salvos em formato .txt ou .md nessa pasta e devidamente commitados no GitHub.

### **Resumo das últimas ações recomendadas no OpenCode:**

> 1. **Adicionar os gráficos no Notebook** (conforme a sugestão das visualizações via matplotlib/seaborn).  
> 2. **Atualizar o README.md** com:  
   * O link do vídeo na 1ª linha.  
   * A remoção das menções ao ChatGPT.  
   * A seção de *"Próximos Passos (Dashboard Interativo)"*.  
   * A definição clara do seu critério de "Melhor Investimento".  
> 3. **Validar a pasta ai-log/** e dar o git push origin main.

---

*User prompt: Você acha que no readme.md está explicado certinho para o avaliadores como se faz para executar as análises?*

Response: **Sim, a seção "6. Como Executar o Projeto" no seu README.md está excelente e explicada de forma muito clara, completa e profissional.**

Ela aborda perfeitamente tudo o que um avaliador (técnico ou de negócios) precisa saber para rodar o seu trabalho sem dificuldades.

### **Por que a instrução de execução está tão boa?**

> * **Ambiente e Versão:** Especifica o Python (3.10+) e fornece o comando pip install exato com todas as dependências usadas (pandas, numpy, nbformat, jupyter, ipykernel).  
> * **Flexibilidade de Ambiente:** Explica como abrir o arquivo via Jupyter Notebook clássico, Jupyter Lab, extensão do VS Code ou Google Colab.  
> * **Passo a Passo Simples:** Indica claramente o comando de execução no menu (Run ▶ Run All Cells / Restart & Run All).  
> * **Mapeamento do Fluxo:** Apresenta uma tabela com o conteúdo de cada seção (do Setup à Simulação de Compra), permitindo que o avaliador entenda o que cada bloco de células faz.  
> * **Garantia de Integridade:** Reforça que a leitura é feita direto da pasta data/ e não altera os arquivos originais.

### **Único Ponto de Atenção Geral no README.md**

Tudo no README.md está bem redondo, com exceção de **um único detalhe que precisa de preenchimento antes da entrega**:

Na **primeira linha**, o placeholder do link do vídeo ainda está assim:

`> 🔗 **[Vídeo de apresentação do desafio (até 2 min)](link_do_video_no_google_drive)**`

Assim que você gravar o seu vídeo e subir no Google Drive, **lembre-se de substituir link\_do\_video\_no\_google\_drive pelo URL público do vídeo**.

Com isso ajustado, o README.md estará pronto para ser avaliado com nota máxima\!

---

*User prompt: como eu posso gravar a tela do meu computador para montar o vídeo? me ajuda a montar um roteiro de até 3 minutos explicando a minha recomendação, o raciocínio por trás dela, como usei a IA no processo (pedindo pra montar uma lista de tarefas, pedindo ajuda para estruturar os prompts para o opencode e solicitando que o opencode execute as tarefas); e o que faria se tivesse mais uma semana, por favor?*

### **Response: Como Gravar a Tela do Computador**

Para gravar a tela com áudio (voz) e, se desejar, webcam, você pode utilizar uma das seguintes opções gratuitas:

> 1. **OBS Studio (Recomendado \- Gratuito e Sem Marca d'Água):**  
   * Baixe e instale o OBS Studio.  
   * Em *Fontes*, clique no botão **\+** e selecione **Captura de Tela** (para a tela) e **Captura de Entrada de Áudio** (para o seu microfone).  
   * Clique em **Iniciar Gravação**, faça a apresentação e depois clique em **Parar Gravação**.  
> 2. **Ferramentas Nativas do Sistema:**  
   * **Windows:** Pressione Windows \+ Alt \+ R para iniciar a gravação da Game Bar (ou Windows \+ G para abrir as configurações e ativar o microfone).  
   * **Mac:** Pressione Command \+ Shift \+ 5, selecione para gravar a tela inteira e ative o microfone nas opções.  
> 3. **Loom (Mais Simples para Apresentações Rápidas):**  
   * Instale a extensão do Loom no navegador Google Chrome.  
   * Permite gravar a tela e a webcam no canto do vídeo com apenas um clique.

### **Roteiro do Vídeo (Até 3 Minutos)**

Para não ultrapassar o tempo, mantenha o ritmo fluido e siga este cronograma por seções:

#### **0:00 \- 0:30 | Introdução & Problema de Negócio (30 seg)**

> * **O que mostrar:** Mostre a capa do seu README.md ou o repositório no GitHub.  
> * **O que falar:**  
>   "Olá\! Este é o resultado da minha análise para o Hackathon Seazone 2026\. O objetivo foi cruzar dados de aluguel por temporada (Airbnb) com anúncios de compra (VivaReal) em Itapema para responder: onde e em qual tipo de imóvel a Seazone deve investir para maximizar o retorno sobre o capital?"

#### **0:30 \- 1:15 | Metodologia & Uso Estratégico da IA (45 seg)**

> * **O que mostrar:** Abra rapidamente a pasta ai-log/ e a estrutura do repositório no VS Code/GitHub.  
> * **O que falar:**  
>   "Para desenvolver o projeto, utilizei a IA de forma bem estruturada como parceira de pensamento. Primeiro, usei o Gemini para me ajudar a criar uma lista organizada de tarefas e desenhar uma sequência de prompts estratégicos. Em seguida, passei esses comandos para o OpenCode executar as análises e gerar os scripts de código. Documentei todo esse processo mantendo o histórico em texto na pasta ai-log."

#### **1:15 \- 2:15 | A Recomendação & O Raciocínio (60 seg)**

> * **O que mostrar:** Alterne no Jupyter Notebook entre o gráfico/tabela de **Gross Yield** (Seção 5\) e a **Simulação de Compra** (Seção 6).  
> * **O que falar:**  
>   "A análise refutou a tese inicial de que 'compactos no Centro' seriam a opção mais eficiente. Embora tenham alta ocupação (68,7%), o preço de compra por m² no Centro é elevado, resultando em um Gross Yield de apenas 9,1%.  
>   Minha recomendação final para a Seazone é investir em **apartamentos de 2 quartos no bairro Morretes**, operados via anúncio profissional com reserva instantânea. Esse perfil atinge um Gross Yield bruto de 14,3% (12,3% líquido) com um payback de aproximadamente 8 anos. Na nossa simulação real de um imóvel de R$ 750 mil, a receita líquida estimada é de R$ 92,5 mil ao ano."

#### **2:15 \- 2:45 | O Que Faria com Mais 1 Semana (30 seg)**

> * **O que mostrar:** Role a tela até a seção **Próximos Passos & Melhorias Futuras** do README.md.  
> * **O que falar:**  
>   "Se eu tivesse mais uma semana de desenvolvimento, meu próximo passo seria evoluir este estudo estático para um **dashboard interativo em Streamlit**. Isso permitiria aos tomadores de decisão simular dinamicamente taxas de ocupação, custos operacionais e comparar o Yield em tempo real."

#### **2:45 \- 3:00 | Encerramento (15 seg)**

> * **O que mostrar:** Mostre o README.md completo no repositório público.  
> * **O que falar:**  
>   *"Toda a análise, notebooks e logs estão salvos e documentados neste repositório. Obrigado\!"*

### **Dicas Finais para a Gravação**

> * **Treine uma vez sem gravar:** Faça um teste com um cronômetro na mão para alinhar os tempos de cada trecho.  
> * **Vídeo no Google Drive:** Lembre-se de subir o vídeo gravado no Google Drive, alterar a permissão de compartilhamento para **"Qualquer pessoa com o link"** e colar a URL na **primeira linha do seu README.md**.

---

*User prompt: Gemini, como eu pego os  prompts e interações da nossa conversa para adicionar na pasta ai-log/?*

Response: Você tem duas formas simples de coletar as interações que tivemos aqui para salvar na pasta ai-log/:

### **Método 1: Manual (Copiar e Colar)**

> 1. Crie um arquivo de texto na pasta ai-log/ do seu repositório (exemplo: ai-log/estrategia\_e\_prompts\_gemini.md ou .txt).  
> 2. Selecione e copie o texto das orientações, do plano de ação e dos prompts que estruturei para você.  
> 3. Cole o conteúdo nesse novo arquivo e salve.

### **Método 2: Automático (Pedindo para o OpenCode gerar para você)**

Como o OpenCode tem acesso ao ambiente local e pode criar arquivos diretamente, você pode enviar o seguinte comando para ele no terminal:

**Prompt para o OpenCode:** "Crie um arquivo chamado log\_planejamento\_gemini.md dentro da pasta ai-log/. Copie e salve nesse arquivo o plano de ação inicial, a lista de prompts dividida em 5 etapas, as orientações de estrutura do README e o roteiro do vídeo de 3 minutos que definimos para o desafio do Hackathon."

### **Dica de Organização da pasta ai-log/**

Para deixar seu repositório ainda mais organizado, você pode dividir a pasta ai-log/ em dois arquivos:

> * ai-log/01\_planejamento\_e\_prompts\_gemini.md: contendo as nossas conversas de estratégia, estrutura de dados e o roteiro do vídeo.  
> * ai-log/02\_execucao\_opencode.txt: contendo o histórico de execução de código e alterações geradas diretamente no OpenCode.

Ao finalizar a inclusão dos arquivos na pasta, execute os comandos do Git:

`git add ai-log/`  
`git commit -m "docs: adiciona logs de interacao com IA na pasta ai-log"`  
`git push origin main`

---

*User prompt: não seria só clicar aqui (direita superior) e exportar para pdf e depois transforma em .md?*

Response: **Sim, exportar para o Google Docs (ou para PDF) é um ótimo caminho\!**

Como a interface do Gemini oferece a opção **"Exportar para o Google Docs"** exatamente no menu que você abriu:

> 1. Clique em **"Exportar para o Google Docs"**.  
> 2. Abra o arquivo gerado no seu Google Drive.  
> 3. Vá no menu **Arquivo › Fazer download › Texto sem formatação (.txt)** ou **Markdown (.md)** (caso a opção apareça).  
> 4. Mova esse arquivo baixado direto para a pasta ai-log/ do seu repositório.

Se você preferir usar o **"Baixar PDF"**:

> * Baixe o PDF.  
> * Abra o arquivo PDF e copie o texto todo para colar em um arquivo .md ou .txt dentro da pasta ai-log/.

Qualquer uma dessas formas é mais rápida e garante que todo o histórico completo da nossa conversa fique salvo exatamente como o desafio exige\!

---

