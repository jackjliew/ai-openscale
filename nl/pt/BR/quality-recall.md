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

# Rechamada ![tag beta](images/beta.png)
{: #quality_recall}

A Rechamada fornece a proporção de predições corretas em classe positiva.
{: shortdesc}

## Visão rápida da Rechamada
{: #quality_recall-glance}

- **Descrição**: proporção de predições corretas na classe positiva
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
{: #quality_recall-display}

![o gráfico de Rechamada é exibido.](images/quality-recall.png)

## Faça as contas
{: #quality_recall-math}

A rechamada (R) é definida como o número de positivos verdadeiros (Tp) sobre o número de positivos verdadeiros mais o número de falsos negativos (Fn).

```
            número de positivos verdadeiros Rechamada = ______________________________________________________

           (número de positivos verdadeiros + número de falsos negativos)
```
