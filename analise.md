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


### ❤️ Modelo KNN

### 🧡 Modelo Decision Tree

### 💛 Modelo SVM (Support Vector Machine)

### 💚 Modelo RandomForest

### 🩵 Modelo AdaBoost

### 💙 Modelo GradientBoosting

### 💜 Modelo Stacking


## Possíveis melhorias:
- **Experimentação com Codificação Categórica:** explorar diferentes formas de codificação para características categóricas, incluindo outras técnicas além da codificação ordinal e one-hot.
- **Refinamento na Seleção de Características:** reduzir o número de características para evitar overfitting, melhorar a eficiência do modelo e identificar as características mais impactantes para a previsão de preços.
- **Transformação Logarítmica do Alvo:** avaliar a transformação logarítmica do alvo (y_log) para obter uma distribuição mais normal.
- **Otimização Adicional dos Hiperparâmetros:** realizar uma otimização mais detalhada dos hiperparâmetros para levar a um desempenho ainda mais aprimorado do modelo.
