---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

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

# Taxa verdadeira positiva (TPR)
{: #quality_tpr}

A Taxa de positivo verdadeiro (TPR) fornece a proporção de predições corretas em predições de classe positiva. 
{: shortdesc}

## Visão rápida da Taxa de positivo verdadeiro (TPR)
{: #quality_tpr-glance}

- **Descrição**: proporção de predições corretas em predições de classe positiva
- **Limites padrão**: limite inferior = 80%
- **Recomendação padrão**:
   - **Tendência ascendente**: uma tendência ascendente indica que a métrica está melhorando. Isso significa que a reciclagem dos modelos é eficaz.
   - **Tendência descendente**: uma tendência descendente indica que a métrica está se deteriorando. Os dados de feedback estão se tornando significativamente diferentes dos dados de treinamento.
   - **Variação errática ou irregular**: uma variação errática ou irregular indica que os dados de feedback não são consistentes entre as avaliações. Aumente o tamanho de amostra mínimo para o monitor de Qualidade.
- **Tipo de problema**: classificação binária
- **Valores de gráfico**: último valor no prazo
- **Detalhes de métricas disponíveis**: matriz de confusão

## Interpretando a exibição
{: #quality_tpr-display}

![o gráfico de Taxa de positivo verdadeiro é exibido.](images/quality-tpr.png)

## Fazer os cálculos
{: #quality_tpr-math}

A Taxa positiva verdadeira é calculada pela fórmula a seguir:

```
                  número de positivos verdadeiros TPR = _________________________________________________________

        (número de positivos verdadeiros + número de falsos negativos)
```
