---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds, False positive rate, fpr

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

# Taxa de falso positivo (FPR) ![tag beta](images/beta.png)
{: #quality_fpr_false}

A taxa de falso positivo fornece a proporção de predições incorretas na classe positiva.
{: shortdesc}

## Taxa de falso positivo (FPR)
{: #quality_fpr_false-glance}

- **Descrição**: proporção de predições incorretas na classe positiva
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
{: #quality_fpr_false-display}

![o gráfico de Taxa de falso positivo é exibido.](images/quality-fpr.png)

## Faça as contas
{: #quality_fpr_false-math}

A taxa de falso positivo é calculada como o número total de falsos positivos dividido pelo número de falsos positivos e o número de negativos verdadeiros.

```
                        número de falsos positivos
Taxa de falso positivo =  ______________________________________________________

                       (número de falsos positivos + número de negativos verdadeiros)
```
