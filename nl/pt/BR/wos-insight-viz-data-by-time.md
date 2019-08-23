---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: fairness, monitoring, charts, de-biasing, bias, accuracy

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:download: .download}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:faq: data-hd-content-type='faq'}

# Visualizando dados para uma hora específica
{: #it-vdet}

Para ver os detalhes por trás de uma determinada estatística de justiça, clique no gráfico para um horário específico. Uma visualização é aberta dos pontos de dados para um recurso monitorado na hora selecionada. Seguindo o exemplo anterior, o recurso Idade é mostrado no exemplo a seguir.
{: shortdesc}

Observe os três filtros na parte superior da página (Recurso, Data e Hora) que permitem selecionar um recurso ou horário diferente para revisar os detalhes.

![O gráfico de séries temporais é exibido com colunas que representam dados perturbados e de carga útil para a idade e o número de resultados favoráveis](images/wos-insight-data-detail.png)

## Interpretando o gráfico
{: #it-intp}

O gráfico mostra várias coisas:

- Você pode observar a propensão de experiência da população (clientes entre 18 e 23 anos). O gráfico também mostra a porcentagem de resultados esperados para essa população.

- O gráfico mostra a percentagem do resultado esperado (70%) para a população de referência. Essa é a média do resultado esperado entre todas as populações de referência.

- O gráfico está indicando a presença de propensão, porque a proporção entre a porcentagem de resultados esperados para as populações de 18 a 23 anos de idade e a porcentagem de resultados esperados para a população de referência excede o limite. Em outras palavras, 0,52/0,7 = 0,74, que é menor que o limite de 0,8.

- O gráfico também mostra a distribuição dos valores de referência e monitorados para cada valor distinto do atributo nos dados da tabela de carga útil que foi analisada para identificar a propensão. Em outras palavras, se o algoritmo de detecção de propensão analisou os últimos 1790 registros da tabela de carga útil, 120 desses registros tiveram idade de cliente entre 18 e 23 e, fora dessa distribuição, os resultados `Approved` e `Denied` são representados pelo gráfico de barras. A distribuição dos dados de carga útil é mostrada para cada valor distinto do atributo de justiça (mesmo os valores de referência são mostrados). Essas informações podem ser usadas para correlacionar a propensão com a quantia de dados recebidos pelo modelo.

- O gráfico mostra, adicionalmente, que a população com idades entre 31 e 35 anos recebeu 91% de resultados esperados. Isso significa a origem da propensão, o que significa que os dados nesse grupo distorceram os resultados e levaram a um aumento na porcentagem de resultados esperados para a classe de referência. Essas informações podem ser usadas para identificar partes dos dados que podem, em seguida, ser subamostrados ao treinar novamente o modelo.

- Outra coisa importante que o gráfico mostra é o nome da tabela que contém os dados que foram identificados para rotulagem manual. Sempre que o algoritmo detecta propensão em um modelo, ele também identifica os pontos de dados que podem ser enviados para rotulagem manual por humanos. Esses dados rotulados manualmente podem então ser usados juntamente com os dados de treinamento originais para treinar novamente o modelo. Esse modelo treinado novamente provavelmente não terá a propensão. A tabela de rotulagem manual está presente no banco de dados associado à instância do {{site.data.keyword.aios_short}}.
