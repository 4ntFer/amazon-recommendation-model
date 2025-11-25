# Amazon Recommendation Model: Descoberta de Tópicos Latentes e Predição de Consumo

Este repositório contém a implementação da pesquisa realizada como parte da disciplina **Ciência de Dados 2** do **Programa de Pós-Graduação em Computação Aplicada da UTFPR (PPGCA)**. O objetivo principal foi explorar a descoberta de temas latentes nas descrições de produtos da **Amazon** (nas categorias **Filmes e TV**) e entender como esses temas influenciam o comportamento de consumo dos usuários. A partir dessa análise, foi possível construir **perfís de consumidores** e usar esses perfis para prever o consumo de **novos produtos**.

- [Clique para visualizar a apresentação dos resultado de pesquisa](https://github.com/4ntFer/amazon-recommendation-model/blob/main/04%20-%20Pesquisa/Apresenta%C3%A7%C3%A3o.pdf)

## Motivação

Em sistemas de recomendação, entender o comportamento do usuário e os fatores que influenciam suas escolhas é essencial para gerar recomendações precisas e personalizadas. O trabalho foi motivado pela necessidade de desenvolver um modelo de recomendação mais eficiente, utilizando dados de avaliações de usuários da Amazon, especificamente na categoria de **Filmes e TV**.

Para isso, a pesquisa combina técnicas de **modelagem de tópicos** com **perfilamento de usuários** e **predição de consumo futuro**. Com isso, buscamos extrair padrões de comportamento e melhorar as recomendações de produtos baseadas nas preferências individuais dos usuários.

### Modelo de Dados Utilizado

Para a análise, utilizamos o **conjunto de dados de reviews e produtos da Amazon** (Ni, Li e McAuley, 2019), que inclui avaliações de **filmes e produtos de TV**. A partir desses dados, o modelo se concentra em identificar quais tópicos estão presentes nas descrições dos produtos e como esses tópicos se relacionam com o comportamento de consumo dos usuários.

## Metodologia

O processo de desenvolvimento do modelo foi dividido em três partes principais: **Modelagem de Tópicos**, **Perfilamento de Usuários** e **Predição de Consumo Futuro**.

### 1. **Modelagem de Tópicos (Topic Modeling)**

O primeiro passo foi realizar a **modelagem de tópicos** nas descrições dos produtos utilizando o algoritmo **BERTopic**, que foi escolhido por sua capacidade de lidar com dados textuais grandes e encontrar tópicos de forma eficaz. A modelagem de tópicos revelou temas latentes que surgem nas descrições dos produtos, como gêneros de filmes (ex: **terror**, **ficção científica**, **romance**) e aspectos técnicos dos produtos (ex: **formato de mídia**, **duração**, **idioma**).

- **Técnica Utilizada:** **BERTopic**, que utiliza embeddings de palavras e clustering para identificar tópicos relevantes.
- **Parâmetros Importantes:** Número de palavras por tópico (20) e tamanho mínimo dos tópicos (50).

### 2. **Perfilamento de Usuários**

Após a modelagem de tópicos, o próximo passo foi construir **perfís de usuários** baseados nos tópicos consumidos. Isso foi feito utilizando uma abordagem de **regressão logística** para associar os tópicos aos usuários e gerar um vetor de características para cada usuário. Este vetor representa a **probabilidade de cada usuário estar interessado em determinados tópicos**, baseado no seu histórico de consumo.

- **Modelo Utilizado:** **Regressão Logística** para associar os tópicos aos produtos consumidos pelos usuários.
- **Métrica de Avaliação:** A precisão do modelo foi avaliada utilizando a métrica **Normalized Discounted Cumulative Gain (nDCG)**.

### 3. **Predição de Consumo Futuro**

Para testar a capacidade de **prever o consumo futuro de produtos**, aplicamos três modelos de **fatoração matricial**: **ALS (Alternating Least Squares)**, **SVD (Singular Value Decomposition)** e **NMF (Non-negative Matrix Factorization)**. Esses modelos foram treinados para prever quais produtos o usuário poderia consumir com base em seus tópicos de interesse.

- **Modelos Utilizados:** **ALS**, **SVD** e **NMF**.
- **Métrica de Avaliação:** **NMAE (Normalized Mean Absolute Error)** para avaliar o erro de predição.

### 4. **Agrupamento de Usuários**

Finalmente, foi realizado um **clustering dos usuários** com base nos seus perfís, utilizando o algoritmo **K-means**. O objetivo era observar se as categorias de produtos consumidas pelos usuários influenciam suas avaliações e criar agrupamentos baseados em comportamentos similares.

## Resultados

### 1. **Modelagem de Tópicos**

- O modelo encontrou **54 tópicos significativos**, que variaram de temas amplos (como **ficção científica**, **romance** e **história**) a nichos específicos (como **Doctor Who**, **Star Trek**).
- A **coerência semântica** dos tópicos foi avaliada e considerada satisfatória.

### 2. **Perfilamento de Usuários**

- O modelo baseado em **regressão logística** teve um desempenho superior ao modelo de média simples na construção dos perfís dos usuários. 
- A métrica **nDCG@10** foi de 0.7877, indicando que o modelo foi eficaz em prever os produtos consumidos pelos usuários.

### 3. **Predição de Consumo Futuro**

- Os modelos de fatoração matricial tiveram um **erro muito baixo** nas predições de consumo, com **NMAE** variando entre **0.0081 e 0.0087**.
- Esses resultados indicam que os tópicos extraídos podem ser usados para prever com precisão o consumo de novos produtos.

### 4. **Agrupamento de Usuários**

- O agrupamento dos usuários mostrou que não há uma diferença significativa nas avaliações de produtos de categorias mais ou menos consumidas pelos grupos de usuários.

## Tecnologias Utilizadas

- **Python**: Para desenvolvimento da solução.
- **BERTopic**: Para modelagem de tópicos.
- **scikit-learn**: Para implementação de modelos de regressão e avaliação de desempenho.
- **Pandas** e **NumPy**: Para manipulação e análise de dados.
- **Surprise**, **implicit**: Para implementação de modelos de fatoração matricial.
- **Matplotlib**, **Seaborn**: Para visualização de resultados.
