---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Area under ROC

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

# Área sob ROC
{: #quality_roc}

A área sob a curva característica de operação do receptor fornece a área sob rechamada e uma curva de taxa de falso positivo. Ela calcula a sensibilidade com relação à taxa de precipitação.
{: shortdesc}

## Visão rápida da Área sob ROC
{: #quality_roc-glance}

- **Descrição**: área sob rechamada e curva de taxa de falso positivo
- **Limites padrão**: limite inferior = 80%
- **Recomendação padrão**:
   - **Tendência ascendente**: uma tendência ascendente indica que a métrica está melhorando. Isso significa que a reciclagem dos modelos é eficaz.
   - **Tendência descendente**: uma tendência descendente indica que a métrica está se deteriorando. Os dados de feedback estão se tornando significativamente diferentes dos dados de treinamento.
   - **Variação errática ou irregular**: uma variação errática ou irregular indica que os dados de feedback não são consistentes entre as avaliações. Aumente o tamanho de amostra mínimo para o monitor de Qualidade.
- **Tipo de problema**: classificação binária
- **Valores de gráfico**: último valor no prazo
- **Detalhes de métricas disponíveis**: matriz de confusão

## Interpretando a exibição
{: #quality_roc-display}

![o gráfico de Área sob ROC é exibido.](images/quality-area-under-roc.png)

## Fazer os cálculos
{: #quality_roc-math}

A Área sob ROC é plotada parametricamente como a `True positive rate` versus a `False positive rate` com relação a um limite `T`.



