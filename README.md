# Data Cleaning e Data Preparation

Este notebook explora as técnicas de limpeza e preparação de dados utilizando o Pandas, NumPy, e outras bibliotecas populares. Ele aborda a importação de dados, tratamento de valores nulos, remoção de duplicatas, tratamento de strings e padronização dos dados.

## Importando as Bibliotecas

As bibliotecas necessárias para a manipulação e análise dos dados são:

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt


### Criando um Dataset
O dataset utilizado é o conjunto de dados de filmes disponíveis no GitHub. Os dados são carregados utilizando o Pandas:
dados = pd.read_csv(r'https://raw.githubusercontent.com/ribeiromatheus/imdb-dataset/master/movies.csv')
dados
### Tratamento de Nulos
Após carregar o dataset, realizamos a verificação de valores nulos:

dados.describe()
dados.isnull().sum()

### Estratégias para Tratamento de Nulos:
Para variáveis categóricas: podemos substituir os valores nulos pela moda.
Para variáveis contínuas: podemos utilizar a média ou a mediana.
Em alguns casos, a melhor solução pode ser remover as linhas com dados nulos.
Exemplo de substituição de valores nulos pela média:

dados['director_facebook_likes'] = dados['director_facebook_likes'].fillna(dados['director_facebook_likes'].mean())
dados = dados.dropna()
dados

### Tratamento de Duplicatas
O tratamento de duplicatas é realizado para verificar e remover linhas repetidas:

dados_duplicados = dados[['color', 'language']]
dados_duplicados.drop_duplicates().count()
dados_duplicados.drop_duplicates()
dados_duplicados.drop_duplicates(subset=['color'])

### Tratamento de String
Realizamos o tratamento de strings, como a substituição de espaços por underscores e a conversão para minúsculas:

for i in dados.index:
    dados.director_name[i] = dados.director_name[i].replace(' ','_').lower()
dados

### Padronização dos Dados
A padronização dos dados é feita utilizando o StandardScaler do Scikit-Learn para normalizar as variáveis contínuas:

from sklearn.preprocessing import StandardScaler

dados_padronizado = dados[['gross', 'imdb_score']]
scaler = StandardScaler()

dados_padronizado_2 = scaler.fit_transform(dados_padronizado)


### Tecnologias Utilizadas
Pandas: para manipulação e análise de dados.
NumPy: para operações matemáticas e de álgebra linear.
Matplotlib: para visualização de dados.
Scikit-Learn: para a padronização de dados.


### Como Executar
Clone este repositório.
Instale as dependências necessárias:

pip install pandas numpy matplotlib scikit-learn
Execute o notebook para explorar o processo de limpeza e preparação de dados.
