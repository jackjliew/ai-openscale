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

# Visão geral das métricas de qualidade
{: #anlz_metrics}

Use o monitoramento de qualidade para determinar a qualidade da previsão de resultados do seu modelo. Quando o
monitoramento de qualidade está ativado, por padrão, ele gera um conjunto de métricas a cada hora. É possível gerar essas métricas sob demanda clicando no botão **Verificar qualidade agora** ou usando o cliente Python.
{: shortdesc}

As métricas de qualidade são calculadas com base nas informações a seguir:

- dados de feedback rotulados manualmente,
- respostas de implementação monitoradas para esses dados.

Para monitoramento adequado, os dados de feedback devem ser registrados no {{site.data.keyword.aios_short}}
em uma base regular. Os dados de feedback podem ser fornecidos usando a opção "Incluir dados de feedback" ou
usando o cliente Python ou a API de REST.

Para mecanismos de aprendizado de máquina diferentes do {{site.data.keyword.aios_short}}, como o Microsoft Azure ML Studio, o Microsoft Azure ML Service ou o Amazon SageMaker ML, o monitoramento de qualidade cria solicitações de pontuação adicionais na implementação monitorada.
{: note}

É possível revisar todos os valores de métricas ao longo do tempo no painel do {{site.data.keyword.aios_short}}:

![gráfico de métricas de qualidade mostrando o desvio da área sob ROC](images/quality_metrics_001.png)


Para revisar detalhes relacionados, tais como matriz de confusão para classificação binária
e de várias classes, que estão disponíveis para algumas métricas, clique no gráfico.

![tabela de detalhes das métricas de qualidade](images/quality_metrics_002.png)

## Métricas de qualidade suportadas
{: #anlz_metrics_supqualdets}

As métricas de qualidade a seguir são suportadas pelo {{site.data.keyword.aios_short}}:

- [Área sob ROC](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_roc)
- [Área sob PR](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality-area-pr)
- [Variação explicada da proporção](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_var)
- [Erro médio absoluto](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_abserror)
- [Erro quadrático médio](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_squerror)
- [R ao quadrado](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_r_squared)
- [Raiz do erro quadrático médio](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-supqualdets_squ_errors_mean)
- [Precisão](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-accuracy-opener)
- [Taxa positiva verdadeira ponderada (wTPR)](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality-wtpr)
- [Taxa verdadeira positiva (TPR)](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_tpr)
- [Taxa de falso positivo ponderada (wFPR)](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_wfpr_weighted)
- [Taxa de falso positivo (FPR)](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_fpr_false)
- [Rechamada ponderada](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_weighted_recall)
- [Rechamada](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_recall)
- [Precisão ponderada](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_wgth_prec)
- [Precisão](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_precision)
- [Medida F1 ponderada](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_wght_f1-measure)
- [Medida F1](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_f1-measr)
- [Perda logarítmica](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_log_loss)

## Detalhes de qualidade suportados
{: #anlz_metrics_supqualdets_suppr_dets}

Os detalhes a seguir para as métricas de qualidade são suportados pelo {{site.data.keyword.aios_short}}:

### Matriz de confusão
{: #anlz_metrics_supqualdets_confusion-quickovr}

A matriz de confusão o ajuda a entender para qual dos seus dados de feedback a resposta da implantação monitorada está correta e para qual não está.

Para obter mais informações, consulte [Matriz de confusão](/docs/services/ai-openscale?topic=ai-openscale-it-conf-mtx).

## Próximos passos

- Depois que o {{site.data.keyword.aios_short}} detecta problemas de qualidade, como violações de limite de precisão, deve-se criar uma nova versão do modelo que corrija o problema. Usando os dados rotulados manualmente na tabela de feedback, deve-se treinar novamente o modelo com os dados de treinamento originais.

