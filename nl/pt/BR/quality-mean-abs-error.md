---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds, Mean absolute error

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

# Erro médio absoluto ![tag beta](images/beta.png)
{: #quality_abserror}

O erro médio absoluto fornece a média de diferença absoluta entre a predição do modelo e o valor de destino.
{: shortdesc}

## Visão rápida do erro médio absoluto
{: #quality_abserror-glance}

- **Descrição**: média de diferença absoluta entre a previsão do modelo e o valor de destino
- **Limites padrão**: limite superior = 80%
- **Recomendação padrão**:
   - **Tendência ascendente**: uma tendência ascendente indica que a métrica está se deteriorando. Os dados de feedback estão se tornando significativamente diferentes dos dados de treinamento.
   - **Tendência de queda**: uma tendência de queda indica que a métrica está melhorando. Isso significa que o novo treinamento dos modelos é efetivo.
   - **Variação errática ou irregular**: uma variação errática ou irregular
indica que os dados de feedback não são consistentes entre as avaliações. Aumente o tamanho mínimo da
amostra para o monitor de Qualidade.
- **Tipo de problema**: regressão
- **Valores de gráfico**: último valor no prazo
- **Detalhes de métricas disponíveis**: nenhum

## Interpretando a exibição
{: #quality_abserror-display}

![o gráfico de Erro médio absoluto é exibido.](images/xxxx.png)

## Faça as contas
{: #quality_abserror-math}

O Erro médio absoluto é calculado incluindo todos os erros absolutos e dividindo-os pelo número de erros.

```
                           SUM  | Yi - Xi |
Erros médios absolutos =  ____________________

                          número de erros
```
