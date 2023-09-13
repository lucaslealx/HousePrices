# HousePrices
Repositório criado para a **[competição do Kaggle](https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques) sobre a previsão de preço das casas** na cidade de Ames, Iowa (Estados Unidos)

<img src='https://github.com/lucaslealx/HousePrices/blob/main/img/img1.png' />

O histórico dos resultados é mostrado abaixo:
<img src='https://raw.githubusercontent.com/lucaslealx/HousePrices/9301f4bc8360541493d28d524ec00a1d5b37f537/img/img2.png' />


## [Etapa 1: Primeiro modelo](https://github.com/lucaslealx/HousePrices/blob/main/Etapa1.ipynb)
- Nesse etapa fizemos apenas o básico para conseguir verificar qual seria o resultado sem fazer nenhum tratamento nem engenharia dos dados
- Para simplificar, **substituímos todos os valores vazios por -1** e **eliminamos todas as colunas de texto**
- Criamos os modelos utilizando **3 algoritmos**: **[Regressão Linear](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html)**, **[Árvore de Regressão](https://scikit-learn.org/stable/modules/tree.html#regression)** e **[KNeighborsRegressor](https://scikit-learn.org/stable/modules/generated/sklearn.neighbors.KNeighborsRegressor.html#sklearn.neighbors.KNeighborsRegressor)** e **avaliamos os resultados** utilizando o **[erro médio absoluto](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.mean_absolute_error.html)** e o **[erro quadrático médio](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.mean_squared_error.html)**, dando preferência ao segundo pois era o critério usando na competição
- O **score público retornado pelo Kaggle foi: 0,25476**

## [Etapa 2: Limpeza dos dados](https://github.com/lucaslealx/HousePrices/blob/main/Etapa2.ipynb)
- Começamos a fazer um processo de **limpeza dos dados**, analisando **valores vazios e informações faltantes** para escolher a melhor estratégia de tratamento
- Em algumas colunas, valores vazios representavam **ausência dos atributos na casa**, como por exemplo o valor vazio na coluna de piscina significava que aquele imóvel não possuia piscina. Nesse caso o vazio **era uma informação**
- Em outros casos onde a informação realmente estava ausente, usamos tratamentos como **substituir pela média da coluna**, **utilizar uma agregação para encontrar a melhor média para o atributo**, **utilizar a moda**, entre outros tratamentos
- Utilizamos os mesmos modelos da etapa 1 (o que pode ser visto no arquivo **[Etapa2Modelos](https://github.com/lucaslealx/HousePrices/blob/main/Etapa2Modelos.ipynb)**) e o **score público retornado pelo Kaggle foi: 0,1812**

## [Etapa 3: Tratamento dos dados](https://github.com/lucaslealx/HousePrices/blob/main/Etapa3.ipynb)
- Utilizamos a base gerada na etapa 2, com os dados já tratados, e começamos primeiramente analisando a **correlação entre as variáveis numéricas e os valores mais frequentes das variáveis de texto**
- Para tratar colunas do tipo texto, começamos **eliminando as colunas com muitos valores iguais** e depois **utilizamos lambda function e criamos nossas próprias funções para aplicar e fazer o tratamento**
- Além disso, também utilizamos o **OneHotEncoder para o tratamento das variáveis que não possuem relação de ordem e o OrdinalEncoder para aquelas ordenadas**. Para saber mais sobre tratamento de variáveis de texto, tenho um artigo escrito no medium: **[Tratando variáveis categóricas em projetos de Ciência de Dados](https://medium.com/@llucaslleall/tratando-vari%C3%A1veis-categ%C3%B3ricas-em-projetos-de-ci%C3%AAncia-de-dados-834dcc5bb636)**
- Por fim, **nos aprofundamos nas colunas de garagem** para fazer um completo entendimento dessa categoria de variáveis. Com mais tempo e melhor entendimento do negócio, poderíamos estender essa análise para todos os outros grupos de colunas
- Nessa etapa, foram geradas 2 bases:
   - a primeira (_1) onde **selecionamos apenas as colunas que analisamos a fundo**: nesta, executamos os mesmo modelos no arquivo **[Etapa3_1Modelos](https://github.com/lucaslealx/HousePrices/blob/main/Etapa3_1Modelos.ipynb)** e tivemos um **score público do Kaggle de 0,18433**
   - a segunda (_2) onde fizemos um **tratamento genérico para todas as colunas de texto**: para essa base foi executado o **[Etapa3_2Modelos](https://github.com/lucaslealx/HousePrices/blob/main/Etapa3_2Modelos.ipynb)** e tivemos um **score público do Kaggle de 0,45474**
    - O resultado foi muito pior devido ao aumento do número de colunas e aos modelos utilizados. Isso será tratado nas próximas etapas! 
 
## Etapa 4: Adicionando novos modelos
- Nessa etapa utilizamos as duas bases geradas anteriormente nos arquivos **[Etapa4_1](https://github.com/lucaslealx/HousePrices/blob/main/Etapa4_1.ipynb)** e **[Etapa4_2](https://github.com/lucaslealx/HousePrices/blob/main/Etapa4_2.ipynb)**
- Adicionamos 2 novos modelos além da regressão linear (modelo que tinha gerado o melhor resultado anteriormente): **[RandomForestRegressor](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestRegressor.html#sklearn.ensemble.RandomForestRegressor)** e **[XGBoost](https://xgboost.readthedocs.io/en/stable/index.html)**
  - A sugestão de usar o **XGBoost** foi dá própria documentação da competição
- Executando nas 2 bases, tivemos:
  - Para a primeira (_1) o **score público do Kaggle foi de 0,15467**
  - Para a segunda base (_2), esse **score foi de 0,15225**
    - **Apenas com a mudança do modelo conseguimos um resultado melhor!**

## [Etapa 5: Melhorando os parâmetros](https://github.com/lucaslealx/HousePrices/blob/main/Etapa5.ipynb)
- Agora utilizamos o **GridSearchCV** para determinar os **melhores parâmetros** para os 2 modelos que utilizamos na etapa anterior
- Como o RandomForest teve um menor erro quadrático e o XGBoost um menor erro absoluto, testamos os 2 modelos nos dados de teste, resultando em:
   - Para o **RandomForest**: 0,15664
   - Para o **XGBoost**: 0,14904
     - **Para os dados de teste, o XGBoost com os parâmetros otimizados gerou o melhor resultado!**
     
