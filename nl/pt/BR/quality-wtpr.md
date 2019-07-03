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

# Taxa de positivo verdadeiro ponderada (wTPR) ![tag beta](images/beta.png)
{: #quality-wtpr}

A Taxa de positivo verdadeiro ponderada fornece a média ponderada da classe TPR com pesos iguais à probabilidade de classe.
{: shortdesc)

## Visão rápida da Taxa de positivo verdadeiro ponderada (wTPR)
{: #quality-wtpr-glance}

- **Descrição**: média ponderada da classe TPR com pesos igual à probabilidade de classe
- **Limites padrão**: limite inferior = 80%
- **Recomendação padrão**:
   - **Tendência ascendente**: uma tendência ascendente indica que a métrica está melhorando. Isso significa que o novo treinamento dos modelos é efetivo.
   - **Tendência de queda**: uma tendência de queda indica que a métrica
está se deteriorando. Os dados de feedback estão se tornando significativamente diferentes dos dados de treinamento.
   - **Variação errática ou irregular**: uma variação errática ou irregular
indica que os dados de feedback não são consistentes entre as avaliações. Aumente o tamanho mínimo da
amostra para o monitor de Qualidade.
- **Tipo de problema**: classificação de várias classes
- **Valores de gráfico**: último valor no prazo
- **Detalhes de métricas disponíveis**: matriz de confusão

## Interpretando a exibição
{: #quality-wtpr-display}

![A Taxa de positivo verdadeiro ponderada é exibida](images/quality-tpr.png)

## Faça as contas
{: #quality-wtpr-math}

A Taxa positiva verdadeira é calculada pela fórmula a seguir:

```
                  número de positivos verdadeiros TPR = _________________________________________________________

        (número de positivos verdadeiros + número de falsos negativos)
```
