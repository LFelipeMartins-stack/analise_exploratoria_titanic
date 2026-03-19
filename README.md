# Projeto Final SCTEC - Análise Exploratória de Dados (Titanic)

## 📌 Objetivo
Este projeto consiste em uma Análise Exploratória de Dados detalhada da base pública do Titanic. O objetivo principal é investigar o conjunto de dados através de técnicas de limpeza, tratamento, agrupamento e visualização em Python para identificar padrões e fatores associados gerando insights poderosos. Desenvolvido como etapa prática do processo seletivo SCTEC (Trilha de Análise de Dados).

## 🚀 Execução em Nuvem (Google Colab)
Para uma avaliação ágil e sem necessidade de configurações de ambiente local, este projeto foi totalmente otimizado para o **Google Colab**. 

1. Acesse o [Google Colab](https://colab.research.google.com/).
2. Faça o upload do arquivo `src/analise_exploratoria.ipynb`.
3. Na barra lateral esquerda (ícone de pasta), faça o upload do arquivo `dados/titanic_dataset.csv`.
4. Execute as células sequencialmente (`Shift + Enter`).

**Visualização Imediata:** Gráficos e tabelas já estão renderizados no arquivo `.ipynb`, garantindo a análise mesmo sem execução.
**Automação:** O notebook está configurado para buscar a base de dados automaticamente via GitHub, permitindo a execução total com apenas um clique.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/SEU_USUARIO/SEU_REPOSITORIO/blob/main/src/analise_exploratoria.ipynb)

## 💻 Execução Local (Ambiente de Desenvolvimento)

Caso prefira operar o projeto em sua máquina local para fins de teste e validação, siga as instruções abaixo:

Antes de começar, certifique-se de ter o [Python 3](https://www.python.org/) instalado. Você pode verificar a versão no seu terminal/prompt com o comando: `python --version`

* [Python 3](https://www.python.org/) - A linguagem principal.
* [Pandas](https://pandas.pydata.org/) - Utilizado para extração, limpeza, manipulação e agrupamento dos dados.
* [Matplotlib](https://matplotlib.org/) & [Seaborn](https://seaborn.pydata.org/) - Bibliotecas responsáveis pela construção das visualizações gráficas e distribuições.
* [Matplotlib.ticker]: Refinamento e formatação dinâmica de eixos (utilizado para exibição de dados em porcentagem)
* [Jupyter Notebook](https://jupyter.org/) - Ambiente interativo de desenvolvimento.

## 🔧 Instalação e Configuração

1. **Obtenha os arquivos do projeto:**
   Clone o repositório ou extraia a pasta compactada enviada no portal:
   `git clone https://github.com/LFelipeMartins-stack/analise_exploratoria_titanic.git`
 
2. **Navegue até o diretório raiz:**
   `cd analise_exploratoria_titanic`

3. **Instale as dependências exatas do projeto:**
   Utilizamos o pacote `notebook` para garantir um ambiente leve e totalmente compatível com o Colab:
   `pip install pandas matplotlib seaborn notebook`

4. **Inicie a interface do notebook:**
   `jupyter notebook`

**Nota:** Ao abrir o ambiente, navegue até a pasta `src/` e abra o arquivo `analise_exploratoria.ipynb`. Execute as células sequencialmente para observar o processo de limpeza e os insights gerados.

## ⚙️ Executando a Análise (Testes de Validação)

Por se tratar de um projeto focado em Análise Exploratória (Data Science), os "testes" consistem na execução sequencial e validação do pipeline de dados (Extract, Transform, Analyze).

## 🔍 Etapa de Compreensão de Dados

- Utilizado `df.info()`, `df.describe()` e `df.head()`para entender o Dataset e identificar as inconsistências que precisariam ser tratadas na etapa seguinte.

## 🧹 Etapa de Limpeza e Tratamento de Dados

1. **Valores Nulos:**
   - A coluna `Cabin` possuía 687 valores nulos e foi descartada por insuficiência de dados úteis para a análise.
   - A coluna `Age` possuía 177 valores nulos, que foram preenchidos com a mediana das idades. Optou-se pela mediana para evitar que valores extremos (outliers) distorcessem a distribuição das idades.
   - Foram removidas 2 linhas com valores nulos na coluna `Embarked`, pelo baixo quantitativo não valia a pena o tratamento de outra forma.
2. **Duplicatas:** Não foram encontradas linhas duplicadas no conjunto de dados.
3. **Seleção de Variáveis:** Colunas como `PassengerId`, `Ticket` e `Name` foram ignoradas na análise gráfica e excluídas, por não apresentarem correlação direta com a taxa de sobrevivência e para otimizar o processamento.
4. **Otimização de Tipagem:** As variáveis `Sex`, `Pclass` e `Embarked` foram convertidas para o tipo `category`, melhorando a eficiência de memória do *DataFrame*.

## 🧠 Etapa de Análises e Agrupamentos

1. **Taxa de Sobrevivência Geral (Baseline):** Cálculo da média geral de sobreviventes do navio para estabelecer uma "linha de base". Este valor serviu como principal ponto de comparação para entender se um grupo específico teve mais ou menos chances de sobreviver do que a média.
2. **Agrupamentos Simples (`groupby`):** Os dados foram segmentados pelas variáveis `Sex` (Gênero) e `Pclass` (Classe do Bilhete) cruzando-as com a coluna `Survived`. O objetivo foi extrair as taxas de sobrevivência específicas de cada grupo e entender o peso da classe social e do gênero no resgate.
3. **Engenharia de Variáveis:** Aplicação do método `pd.cut()` para transformar a coluna numérica contínua `Age` (Idade) em uma nova variável categórica chamada `Faixa_Etaria`. Os passageiros foram classificados de forma lógica em: Menores (0-17), Adultos (18-59) e Idosos (60+).

## 📈 Etapa de Visualização de Dados Graficamente 

1. **Distribuição Etária (Histograma):**
   - **Objetivo:** Compreender o perfil demográfico geral de todos os passageiros a bordo.
   - **Execução:** Foi gerado um histograma da variável `Age` com a adição de uma linha de estimativa de densidade. 
   - **Observação Visual:** O gráfico ilustra claramente uma distribuição assimétrica, evidenciando que a grande maioria dos passageiros era composta por jovens adultos na faixa dos 20 aos 30 anos.

2. **Taxa de Sobrevivência por Gênero (Gráfico de Barras):**
   - **Objetivo:** Comprovar de forma visual e impactante a forte correlação entre o gênero e a probabilidade de resgate.
   - **Execução:** Um gráfico de barras cruzando as variáveis categóricas para comparar as proporções.
   - **Refinamento de UX (Experiência do Usuário):** Para tornar o relatório mais executivo, o eixo Y foi formatado em percentual (0% a 100%) em vez de escala decimal padrão (0 a 1). Além disso, os rótulos nativos ("male" e "female") foram traduzidos e ordenados para o português.


## 📊 Principais Insights e Decisões

Com base nas análises de agrupamento (`GroupBy`) e visualizações gráficas, foi possível concluir que:
1. **Gênero:** As mulheres tiveram uma taxa de sobrevivência significativamente superior à dos homens (aproximadamente 74,20% contra 18,89%), evidenciando a prioridade no resgate.
2. **Faixa Etária (Crianças):** A análise revelou que menores de 18 anos tiveram uma taxa de sobrevivência superior (cerca de 54%) à média geral do navio (38%), validando a eficácia da regra histórica de "mulheres e crianças primeiro".
3. **Classe Social:** Passageiros da 1ª classe tiveram prioridade de resgate e, consequentemente, uma maior taxa de sobrevivência (cerca de 62,96%) em comparação com os passageiros da 3ª classe (apenas 24,24%).

## ⌨️ Testes de Estilo de Codificação

O código foi escrito seguindo as diretrizes PEP 8 para Python, priorizando a clareza analítica.
**Exemplo:** Uso de `display()` em vez de `print()` no ecossistema de notebooks para garantir a renderização adequada de DataFrames no formato HTML.

## ✒️ Autores

**Luis Felipe Martins** - *Estruturação, Limpeza de Dados e Análise Exploratória* - [GitHub](https://github.com/LFelipeMartins-stack)

## 🎁 Expressões de gratidão

* Agradecimento especial à organização do processo seletivo SCTEC pela oportunidade e pelo desafio enriquecedor proposto.
