---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds

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

# Precisão
{: #accuracy-opener}

Precisão é uma medida da proporção de predições corretas contidas em seu modelo.
{: shortdesc}

## Visão rápida da Precisão
{: #anlz_metrics_supqualdets_acc}

- **Descrição**: a proporção de predições corretas
- **Limites padrão**: limite inferior = 80%
- **Recomendação padrão**:
   - **Tendência ascendente**: uma tendência ascendente indica que a métrica está melhorando. Isso significa que a reciclagem dos modelos é eficaz.
   - **Tendência descendente**: uma tendência descendente indica que a métrica está se deteriorando. Os dados de feedback estão se tornando significativamente diferentes dos dados de treinamento.
   - **Variação errática ou irregular**: uma variação errática ou irregular indica que os dados de feedback não são consistentes entre as avaliações. Aumente o tamanho de amostra mínimo para o monitor de Qualidade.
- **Tipos de problemas**: classificação binária e classificação de classe múltipla
- **Valores de gráfico**: último valor no prazo
- **Detalhes de métricas disponíveis**: matriz de confusão


## Entendendo a Precisão
{: #acc-understand}

A Precisão pode significar coisas diferentes dependendo do tipo do algoritmo:

- *Classificação multiclasse*: a Precisão mede o número de vezes que qualquer classe foi prevista corretamente, normalizada pelo número de pontos de dados. Para obter mais detalhes, consulte [Classificação multiclasse](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#multiclass-classification){: external} na documentação do Apache Spark.

- *Classificação binária*: para um algoritmo de classificação binária, a precisão é medida como a área sob uma curva ROC. Consulte [Classificação binária](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#binary-classification){: external} na documentação do Apache Spark para obter mais detalhes.

- *Regressão*: os algoritmos de regressão são medidos usando o Coeficiente de Determinação, ou R2. Para obter mais detalhes, consulte [Avaliação do modelo de regressão](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#regression-model-evaluation){: external} na documentação do Apache Spark.

### Como ele funciona
{: #acc-works}

É necessário incluir dados de feedback rotulados manualmente por meio da IU do {{site.data.keyword.aios_short}}, conforme mostrado nos exemplos a seguir, usando um [cliente Python](http://ai-openscale-python-client.mybluemix.net/#feedbacklogging){: external} ou uma [API de REST](https://cloud.ibm.com/apidocs/ai-openscale#post-feedback-payload){: external}.

### Precisão sem propensão
{: #acc-debias-view}

Quando há dados para o suporte, a precisão é calculada tanto no modelo original quanto no modelo sem propensão. O {{site.data.keyword.aios_full_notm}} calcula a precisão para a saída sem propensão e a armazena na tabela de criação de log de carga útil como uma coluna adicional.

![uma visualização de modelo aparece com precisão calculada para os modelos original e sem propensão](images/debiased-accuracy.png)
