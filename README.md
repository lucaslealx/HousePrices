# HousePrices
Repositório criado para a **[competição do Kaggle](https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques) sobre a previsão de preço das casas** na cidade de Ames, Iowa (Estados Unidos)

<img src='https://github.com/lucaslealx/HousePrices/blob/main/img/img1.png' />

O histórico dos resultados é mostrado abaixo:



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
