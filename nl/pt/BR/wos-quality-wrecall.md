---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, weighted recal

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

# Rechamada ponderada
{: #quality_weighted_recall}

A Rechamada ponderada fornece a média ponderada de rechamada com pesos iguais à probabilidade de classe.
{: shortdesc}

## Visão rápida da Rechamada ponderada
{: #quality_weighted_recall-glance}

- **Descrição**: média ponderada de rechamada com pesos igual à probabilidade de classe
- **Limites padrão**: limite inferior = 80%
- **Recomendação padrão**:
   - **Tendência ascendente**: uma tendência ascendente indica que a métrica está melhorando. Isso significa que a reciclagem dos modelos é eficaz.
   - **Tendência descendente**: uma tendência descendente indica que a métrica está se deteriorando. Os dados de feedback estão se tornando significativamente diferentes dos dados de treinamento.
   - **Variação errática ou irregular**: uma variação errática ou irregular indica que os dados de feedback não são consistentes entre as avaliações. Aumente o tamanho de amostra mínimo para o monitor de Qualidade.
- **Tipo de problema**: classificação de multiclasses
- **Valores de gráfico**: último valor no prazo
- **Detalhes de métricas disponíveis**: matriz de confusão

## Interpretando a exibição
{: #quality_weighted_recall-display}

![o gráfico de rechamada ponderada é exibido.](images/quality-recall.png)

## Fazer os cálculos
{: #quality_weighted_recall-math}

A Rechamada ponderada (wR) é definida como o número de positivos verdadeiros (Tp) sobre o número de positivos verdadeiros mais o número de falsos negativos (Fn) usados com dados ponderados. 

```
            número de positivos verdadeiros Rechamada = ______________________________________________________

           (número de positivos verdadeiros + número de falsos negativos)
```
