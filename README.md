# Projeto Desafio Cientista de Dados - Lucas Sales

## Sumário
- [Introdução](#introdução)
- [Requisitos do Projeto](#requisitos-do-projeto)
- [Instalação](#instalação)
- [Execução](#execução)
- [Estrutura do Projeto](#estrutura-do-projeto)
- [Detalhamento das Etapas](#detalhamento-das-etapas)
- [Conclusões e Respostas às Perguntas de Negócio](#conclusões-e-respostas-à-perguntas-de-negócio)
- [Dependências](#dependências)
- [Considerações Finais](#considerações-finais)

## Introdução
Este projeto foi desenvolvido para o desafio de Cientista de Dados da Indicium. O objetivo é desenvolver um modelo preditivo de preços para uma plataforma de aluguéis temporários em Nova York, utilizando o dataset fornecido. O projeto abrange uma análise exploratória detalhada (EDA), o desenvolvimento de modelos preditivos (problema de regressão) e a interpretação dos resultados, além de responder às seguintes questões de negócio:
- **Onde seria mais indicada a compra de um apartamento para alugar na plataforma?**
- **O número mínimo de noites e a disponibilidade interferem no preço?**
- **Existe algum padrão no texto do nome do anúncio para lugares de mais alto valor?**
- **Como a previsão é feita e qual modelo se aproxima melhor dos dados?**

## Requisitos do Projeto
- Python 3.7+
- Bibliotecas: pandas, numpy, matplotlib, seaborn, missingno, scikit-learn, scipy, shap, pickle, entre outras.
- O arquivo `teste_indicium_precificacao.csv` deve estar na raiz do projeto.

## Instalação
1. Clone o repositório: https://github.com/lukasales/Projeto_final

git clone <[link-do-repositorio](https://github.com/lukasales/Projeto_final)>

2. Instale as dependências:

pip install -r requirements.txt

## Execução
Para executar o projeto, abra o notebook `Desafio_Cientista_de_Dados.ipynb` e execute as células na ordem.

## Estrutura do Projeto
- **Desafio_Cientista_de_Dados.ipynb:** Notebook contendo todo o código organizado em blocos, com análise exploratória, modelagem, tuning e interpretação.
- **requirements.txt:** Lista de dependências e versões.
- **best_model_nn.pkl:** (ou o modelo final escolhido) – Modelo final salvo.
- **README.md:** Este arquivo.
- **Relatório_Final.pdf:** Relatório detalhado das análises e resultados.

## Detalhamento das Etapas
### 1. Análise Exploratória de Dados (EDA)
Eu comecei carregando e limpando os dados, removendo duplicatas e preenchendo valores ausentes. Em seguida, criei diversos gráficos (histograma, boxplot, heatmap) para visualizar a distribuição dos preços e as relações entre as variáveis. Também criei a feature "tem_luxo" a partir dos termos do nome dos anúncios e executei um t-test para verificar a diferença de preços entre anúncios com e sem essa característica.

### 2. Respostas às Perguntas de Negócio
- **Onde comprar?**  
A análise dos gráficos de preço médio por "bairro_group" e "bairro" me permitiu identificar que, embora bairros com preços mais altos (como em Manhattan) indiquem alta demanda, eles também podem ter alta concorrência. Assim, a escolha do investimento dependerá de um equilíbrio entre custo e potencial de valorização.

- **Impacto de "minimo_noites" e "disponibilidade":**  
O heatmap de correlação me mostrou as relações entre "minimo_noites", "disponibilidade_365" e "price". Em meu conjunto de dados, essas correlações não foram extremamente fortes, sugerindo que, isoladamente, essas variáveis têm impacto moderado, mas podem ser relevantes em conjunto com outras features.

- **Padrão no nome dos anúncios:**  
O teste t para a feature "tem_luxo" indicou uma diferença estatisticamente significativa entre os preços dos anúncios com termos de luxo e os que não os possuem. Isso demonstra que a forma como o anúncio é nomeado influencia a percepção de valor e, consequentemente, o preço.

- **Previsão de Preço e Escolha do Modelo:**  
Eu tratei o problema como um problema de regressão. A partir da transformação dos dados (OneHotEncoder para variáveis categóricas, StandardScaler para variáveis numéricas e SelectKBest para seleção de features), desenvolvi quatro pipelines para modelos diferentes: Regressão Linear, Random Forest, Gradient Boosting e uma rede neural (MLPRegressor). Eu escolhi o RMSE como métrica principal, pois ela penaliza erros grandes e é facilmente interpretada em termos monetários. Cada modelo apresenta vantagens e desvantagens – por exemplo, a rede neural pode capturar relações complexas, mas exige cuidado com overfitting, enquanto o Random Forest é robusto, mas menos interpretável.  

### 3. Modelagem Preditiva e Tuning
Eu criei pipelines para os modelos, avaliei o desempenho inicial (baseline) e depois realizei tuning dos hiperparâmetros usando RandomizedSearchCV para Random Forest, Gradient Boosting e a rede neural. Após o tuning, validei os modelos com validação cruzada e comparei os resultados usando boxplots.

### 4. Previsão de Caso Específico e Salvamento do Modelo
Utilizei o modelo otimizado (neste caso, optei pela rede neural, mas a comparação está disponível para todos os modelos) para prever o preço de um apartamento com características específicas. O modelo final foi salvo no formato .pkl para futura utilização.

## Dependências
As dependências do projeto estão listadas no arquivo `requirements.txt`. Por exemplo:
- pandas==1.3.5
- numpy==1.21.5
- matplotlib==3.5.1
- seaborn==0.11.2
- scikit-learn==1.0.2
- missingno==0.5.1
- scipy==1.7.3
- shap==0.40.0

## Considerações Finais
Eu realizei uma análise completa, desde a limpeza dos dados e exploração inicial até a construção, tuning e validação dos modelos preditivos. O relatório detalha cada etapa, os gráficos gerados e as hipóteses de negócio testadas. Além disso, a utilização de uma rede neural me permitiu comparar abordagens lineares e não-lineares para prever os preços dos anúncios. Este projeto demonstra meu domínio em análise exploratória, modelagem preditiva e interpretação dos resultados.
