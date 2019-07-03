---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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

# Visão geral da métrica de qualidade ![tag beta](images/beta.png)
{: #anlz_metrics}

Use o monitoramento de qualidade para determinar como o seu modelo prevê resultados. Quando o monitoramento de qualidade é ativado, ele gera um conjunto de métricas a cada hora, por padrão. É possível gerar essas métricas sob demanda clicando no botão **Verificar qualidade agora** ou usando o cliente Python.

As métricas de qualidade são calculadas com base nas informações a seguir:

- dados de feedback rotulados manualmente,
- respostas de implementação monitoradas para esses dados.

Para monitoramento adequado, os dados de feedback devem ser registrados no {{site.data.keyword.aios_short}} regularmente. Os dados de feedback podem ser fornecidos usando a opção "Incluir dados de Feedback" ou usando o cliente Python ou a API de REST.

Para mecanismos de aprendizado de máquina diferentes do {{site.data.keyword.aios_short}}, como o Microsoft Azure ML Studio ou o Amazon Sagemaker ML, o monitoramento de qualidade cria solicitações de pontuação adicionais na implementação monitorada.
{: note}

É possível revisar todos os valores de métricas ao longo do tempo no painel do {{site.data.keyword.aios_short}}:

![gráfico de métricas de qualidade que mostra drift de área sob ROC](images/quality_metrics_001.png)


Para revisar detalhes relacionados, como matriz de confusão para classificação binária e de várias classes, que estão disponíveis para algumas métricas, clique no gráfico.

![tabela detalhada de métricas de qualidade](images/quality_metrics_002.png)

## Métricas de qualidade suportadas
{: #anlz_metrics_supqualdets}

As métricas de qualidade a seguir são suportadas pelo {{site.data.keyword.aios_short}}:

- [Área sob ROC](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_roc)
- [Área sob PR](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality-area-pr)
- [Variação explicada da proporção](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_var){: download}
- [Erro médio absoluto](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_abserror){: download}
- [Erro quadrático médio](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_squerror){: download}
- [R ao quadrado](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_r_squared){: download}
- [Raiz do erro quadrático médio](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-supqualdets_squ_errors_mean){: download}
- [Precisão](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-accuracy-opener)
- [Taxa positiva verdadeira ponderada (wTPR)](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality-wtpr){: download}
- [Taxa verdadeira positiva (TPR)](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_tpr)
- [Taxa de falso positivo ponderada (wFPR)](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_wfpr_weighted){: download}
- [Taxa de falso positivo (FPR)](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_fpr_false)
- [Rechamada ponderada](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_weighted_recall){: download}
- [Rechamada](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_recall)
- [Precisão ponderada](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_wgth_prec){: download}
- [Precisão](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_precision)
- [Medida F1 ponderada](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_wght_f1-measure){: download}
- [Medida F1](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_f1-measr)
- [Perda logarítmica](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_log_loss)

## Detalhes de qualidade suportados
{: #anlz_metrics_supqualdets_suppr_dets}

Os detalhes a seguir para as métricas de qualidade são suportados pelo {{site.data.keyword.aios_short}}:

### Matriz de confusão
{: #anlz_metrics_supqualdets_confusion-quickovr}

A matriz de confusão ajuda você a entender para qual de seus dados de feedback a resposta de implementação monitorada está correta e para a qual ela não está.

Para obter mais informações, consulte [Matriz de confusão](/docs/services/ai-openscale?topic=ai-openscale-it-conf-mtx).
