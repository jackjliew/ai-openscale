---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, confusion matrix

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

# Matriz de confusão
{: #it-conf-mtx}

Como um detalhe das métricas de qualidade, é possível visualizar os registros que o modelo analisou incorretamente. Essas anomalias podem ser falsos positivos ou falsos negativos para modelos de classificação binários ou podem ser designações de classe incorretas para modelos de várias classes. Também
é possível visualizar uma lista de registros de feedback que o modelo não analisou corretamente.
{: shortdesc}

Para revisar detalhes relacionados, como matriz de confusão para classificação binária e de várias classes, que estão disponíveis para algumas métricas, clique no gráfico.

![tabela detalhada de métricas de qualidade](images/quality_metrics_002.png)

Para problemas binários, o {{site.data.keyword.aios_full}} designa a categoria de destino para o nível `positive` ou `negative`. Para isso, a saída da matriz de confusão segue a convenção em que o rótulo para a categoria positiva está localizado na segunda linha ou coluna.


## Etapas
{: #it-conf-mtx-steps}

1. Em qualquer um dos gráficos de **Qualidade**, como **Precisão**, clique em uma hora/dia no gráfico.
    
    ![Lista de transações com propensão](images/Confusion_Matrix_040819.004.png)

1. Uma matriz de confusão exibe os falsos positivos e os falsos negativos. Clique em uma célula
para visualizar o subconjunto de registros de feedback.

    ![Lista de transações com propensão](images/Confusion_Matrix_040819.005.png)

1. Revise os registros de feedback e solicite uma explicação da análise com relação ao registro de feedback.

    ![Lista de transações com propensão](images/Confusion_Matrix_040819.006.png)

1. As transações aparecem em sequência.

    ![Lista de transações com propensão](images/Confusion_Matrix_040819.007.png)

