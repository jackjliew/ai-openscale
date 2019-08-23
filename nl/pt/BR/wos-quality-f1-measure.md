---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, F1-Measure

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

# Medida F1
{: #quality_f1-measr}

A Medida F1 fornece a média harmônica de precisão e rechamada.
{: shortdesc}

## Visão rápida da Medida F1
{: #quality_f1-measr-glance}

- **Descrição**: média harmônica de precisão e rechamada
- **Limites padrão**: limite inferior = 80%
- **Recomendação padrão**:
   - **Tendência ascendente**: uma tendência ascendente indica que a métrica está melhorando. Isso significa que o novo treinamento dos modelos é efetivo.
   - **Tendência de queda**: uma tendência de queda indica que a métrica
está se deteriorando. Os dados de feedback estão se tornando significativamente diferentes dos dados de treinamento.
   - **Variação errática ou irregular**: uma variação errática ou irregular
indica que os dados de feedback não são consistentes entre as avaliações. Aumente o tamanho mínimo da
amostra para o monitor de Qualidade.
- **Tipo de problema**: classificação binária
- **Valores de gráfico**: último valor no prazo
- **Detalhes de métricas disponíveis**: matriz de confusão

## Interpretando a exibição
{: #quality_f1-measr-display}

![o gráfico de Medida F1 é exibido.](images/quality-f1-meas.png)

## Fazer os cálculos
{: #quality_f1-measr-math}

A F1-Measure é a média harmônica ponderada, ou média, de precisão e rechamada.

```
          (precisão * rechamada) F1 = 2 * ____________________

          (precisão + rechamada)
```

