---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Weighted F1-Measure

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

# Medida F1 ponderada
{: #quality_wght_f1-measure}

A Medida F1 ponderada fornece a média ponderada da medida F1 com pesos iguais à probabilidade de classe.
{: shortdesc}

## Visão rápida da Medida F1 ponderada
{: #quality_wght_f1-measure-glance}

- **Descrição**: média ponderada de medida F1 com pesos igual à probabilidade de classe
- **Limites padrão**: limite inferior = 80%
- **Recomendação padrão**:
   - **Tendência ascendente**: uma tendência ascendente indica que a métrica está melhorando. Isso significa que a reciclagem dos modelos é eficaz.
   - **Tendência descendente**: uma tendência descendente indica que a métrica está se deteriorando. Os dados de feedback estão se tornando significativamente diferentes dos dados de treinamento.
   - **Variação errática ou irregular**: uma variação errática ou irregular indica que os dados de feedback não são consistentes entre as avaliações. Aumente o tamanho de amostra mínimo para o monitor de Qualidade.
- **Tipo de problema**: classificação de multiclasses
- **Valores de gráfico**: último valor no prazo
- **Detalhes de métricas disponíveis**: matriz de confusão

## Interpretando a exibição
{: #quality_wght_f1-measure-display}

![o gráfico de Medida F1 ponderada é exibido.](images/quality-f1-meas.png)

## Fazer os cálculos
{: #quality_wght_f1-measure-math}

A Medida F1 ponderada é o resultado do uso de dados ponderados.

```
          (precisão * rechamada) F1 = 2 * ____________________

          (precisão + rechamada)
```
