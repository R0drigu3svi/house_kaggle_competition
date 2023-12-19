# Desafio Kaggle Open Challenge - Vivi

## 💥 Compreensão do desafio
O objetivo central deste desafio é desenvolver um modelo preditivo robusto capaz de estimar com precisão os preços finais das casas residenciais em Ames, Iowa. Para isso, o desafio se baseia em práticas avançadas de modelagem, incluindo o uso de modelos de regressão linear (Ridge e Lasso) e técnicas de regularização. 

## Conjunto de Dados
O conjunto de dados abrange 79 variáveis explicativas, oferecendo uma visão das características físicas, condições e atributos das residências. A competição desafia os participantes a explorar e modelar essas variáveis para extrair padrões que influenciam significativamente os preços imobiliários.

### 🗃 Arquivos 
O processo é dividido em três arquivos principais: pipeline.py, preprocessors.py e trainer.py. Cada arquivo desempenha um papel específico na construção e avaliação do modelo.

#### 🗂 Arquivo pipeline.py

Possui 3 funções:
* **'create_preproc()'**: cria um pipeline de pré-processamento para os dados dividido em três partes: numérico, ordinal e nominal.
* **'create_model()'**:  cria um modelo empilhado (StackingRegressor) composto por diferentes regressores: Gradient Boosting, AdaBoost, Ridge e SVM. O regressor final é uma Regressão Linear.
* **'create_pipeline()'**: combina o pré-processamento e o modelo em um único pipeline usando a função make_pipeline do scikit-learn.

#### 🗂 Arquivo preprocessors.py

Possui 3 funções:
* **'create_preproc_ordinal()'**: cria um pré-processador específico para características ordinais.
  - Imputação de valores ausentes com a categoria "missing".
  - Codificação ordinal usando OrdinalEncoder.
  - Normalização das características usando MinMaxScaler.

* **'create_preproc_numerical()'**: cria um pré-processador específico para características numéricas.
  - Imputação de valores ausentes usando KNNImputer.
  - Normalização das características usando MinMaxScaler.

* **'create_preproc_nominal()'**: cria um pré-processador específico para características nominais.
  - Imputação de valores ausentes usando a estratégia "most_frequent" (SimpleImputer).
  - Codificação one-hot usando OneHotEncoder.

#### 🗂 Arquivo trainer.py

A classe Trainer é responsável por carregar os dados, construir o pipeline e realizar a validação cruzada. Isso é feito a partir da criação de uma instância do Trainer feita pelo script.

**Métodos:**

  → load_data(): Carrega os dados do conjunto de treinamento.

  → build_pipeline(feature_cutoff_percentage=75): Constrói o pipeline chamando as funções em "pipeline.py".

  → cross_validate(cv=5): Realiza a validação cruzada e imprime o RMSLE médio e desvio padrão.


Além desses 3 arquivos principais, o desafio possui outros 3 sendo de teste. Eles fornecem casos de teste automatizados para verificar se os diferentes componentes estão funcionando conforme esperado.

#### 🗂 Arquivo test_features_overview.py

  Contém um caso de teste para verificar se o número de características categóricas está correto.

#### 🗂 Arquivo test_preproc_baseline.py

  Contém um caso de teste para verificar se a forma do conjunto de dados após o pré-processamento está correta.

#### 🗂 Arquivo test_submission_baseline.py

  Contém vários casos de teste relacionados à submissão de resultados.

#### 🗂 **Descrições de outros arquivos**

  - **train.csv**: conjunto de treinamento
    
  - **test.csv**: conjunto de testes
    
  - **data_description.txt**: descrição completa de cada coluna, originalmente preparada por Dean De Cock, mas ligeiramente editada para corresponder aos nomes das colunas usados aqui
    
  - **sample_submission.csv**: envio de referência de uma regressão linear no ano e mês da venda, metragem quadrada do lote e número de quartos


## Métodos de treinamento - Modelo Essemble

### 🩷 Modelo Ridge Regression
A Ridge Regression é uma técnica de regularização que se destina a lidar com o desafio da multicolinearidade em conjuntos de dados caracterizados pela presença de muitas variáveis explicativas. Ela ocorre quando algumas variáveis independentes em um modelo de regressão linear estão fortemente correlacionadas entre si. Ele é útil para lidar com modelos que assumem uma relação linear entre as características e o alvo.

- Métrica de Desempenho : RMSLE (Root Mean Squared Logarithmic Error).
- Média do RMSE : -32,091.87

### ❤️ Modelo KNN
O K-Nearest Neighbors (KNN) é um modelo de aprendizado supervisionado utilizado para classificação e regressão. Ele prediz a classe ou valor alvo de uma instância com base na média ou moda dos K vizinhos mais próximos no espaço de características, onde a proximidade é medida por uma métrica, como a distância euclidiana. 

- Média do RMSE: -0.157 (negativo devido à configuração de greater_is_better=False)

### 🧡 Modelo Decision Tree
A Decision Tree (Árvore de Decisão) é um modelo de aprendizado de máquina que opera dividindo iterativamente os dados com base em características, criando segmentações hierárquicas que representam decisões e suas consequências. 

### 💛 Modelo SVM (Support Vector Machine)
O Support Vector Machine é um modelo de aprendizado de máquina usado para tarefas de classificação e regressão que busca encontrar um hiperplano que melhor separa os dados em classes diferentes. 

### 💚 Modelo RandomForest
O Random Forest (Floresta Aleatória) é um modelo que opera através da construção de múltiplas árvores de decisão durante o treinamento e, em seguida, combina suas previsões para obter uma previsão mais robusta e precisa.

### 🩵 Modelo AdaBoost
O AdaBoost é um algoritmo de aprendizado de máquina que pertence à família de métodos de ensemble, projetado para melhorar o desempenho de modelos mais fracos ao atribuir pesos diferenciados às instâncias de dados. 

### 💙 Modelo GradientBoosting
O Gradient Boosting é uma técnica de ensemble que constrói modelos de maneira sequencial, buscando corrigir os erros dos modelos anteriores.

### 💜 Modelo Stacking
O Stacking, ou Empilhamento, é uma técnica de ensemble que combina as previsões de vários modelos base, usando um meta-modelo para realizar a predição final.

## Possíveis melhorias:
- **Experimentação com Codificação Categórica:** explorar diferentes formas de codificação para características categóricas, incluindo outras técnicas além da codificação ordinal e one-hot.
- **Refinamento na Seleção de Características:** reduzir o número de características para evitar overfitting, melhorar a eficiência do modelo e identificar as características mais impactantes para a previsão de preços.
- **Transformação Logarítmica do Alvo:** avaliar a transformação logarítmica do alvo (y_log) para obter uma distribuição mais normal.
- **Otimização Adicional dos Hiperparâmetros:** realizar uma otimização mais detalhada dos hiperparâmetros para levar a um desempenho ainda mais aprimorado do modelo.
