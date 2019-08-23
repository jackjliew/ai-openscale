---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Weighted precision

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

# Precisão ponderada
{: #quality_wgth_prec}

A Precisão ponderada fornece a média ponderada da precisão com pesos iguais à probabilidade de classe.
{: shortdesc}

## Visão rápida da Precisão ponderada
{: #quality_wgth_prec-glance}

- **Descrição**: média ponderada de precisão com pesos igual à probabilidade de classe
- **Limites padrão**: limite inferior = 80%
- **Recomendação padrão**:
   - **Tendência ascendente**: uma tendência ascendente indica que a métrica está melhorando. Isso significa que a reciclagem dos modelos é eficaz.
   - **Tendência descendente**: uma tendência descendente indica que a métrica está se deteriorando. Os dados de feedback estão se tornando significativamente diferentes dos dados de treinamento.
   - **Variação errática ou irregular**: uma variação errática ou irregular indica que os dados de feedback não são consistentes entre as avaliações. Aumente o tamanho de amostra mínimo para o monitor de Qualidade.
- **Tipo de problema**: classificação de multiclasses
- **Valores de gráfico**: último valor no prazo
- **Detalhes de métricas disponíveis**: matriz de confusão

## Interpretando a exibição
{: #quality_wgth_prec-display}

![o gráfico de Precisão ponderada é exibido.](images/quality-precision.png)

## Fazer os cálculos
{: #quality_wgth_prec-math}

A precisão (P) é definida como o número de positivos verdadeiros (Tp) sobre o número de positivos verdadeiros mais o número de falsos positivos (Fp).


```
                        número de positivos verdadeiros Precisão = __________________________________________________________

             (número de positivos verdadeiros + o número de falsos positivos)
```
