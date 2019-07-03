---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds, Mean squared error

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

# Erro quadrático médio ![tag beta](images/beta.png)
{: #quality_squerror}

O erro quadrático médio fornece a média de diferença quadrática entre a predição do modelo e o valor de destino.
É possível utilizá-lo como a medida da qualidade de um estimador.
{: shortdesc}

## Visão rápida do erro quadrático médio
{: #quality_squerror-glance}

- **Descrição**: média de diferença quadrática entre predição de modelo e valor de destino
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
{: #quality_squerror-display}

![o gráfico de Erro quadrático médio é exibido.](images/xxxx.png)

## Faça as contas
{: #quality_squerror-math}

O Erro quadrático médio em sua forma mais simples é representado pela fórmula a seguir.

```
                             SUM  (Yi - ^Yi) * (Yi - ^Yi)
Erros quadráticos médios  =  ____________________________

                             número de erros
```
