---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, R squared

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

# R ao quadrado
{: #quality_r_squared}

R ao quadrado é a razão de diferença entre a variação de destino e a variação para o erro de predição para a variação de destino. Ele pode dizer com que eficiência os dados usados para criar o modelo se ajusta à regressão.
{: shortdesc}

## Visão rápida do R ao quadrado
{: #quality_r_squared-glance}

- **Descrição**: razão de diferença entre a variação de destino e a variação para o erro de predição para a variação de destino
- **Limites padrão**: limite inferior = 80%
- **Recomendação padrão**:
   - **Tendência ascendente**: uma tendência ascendente indica que a métrica está melhorando. Isso significa que o novo treinamento dos modelos é efetivo.
   - **Tendência de queda**: uma tendência de queda indica que a métrica
está se deteriorando. Os dados de feedback estão se tornando significativamente diferentes dos dados de treinamento.
   - **Variação errática ou irregular**: uma variação errática ou irregular
indica que os dados de feedback não são consistentes entre as avaliações. Aumente o tamanho mínimo da
amostra para o monitor de Qualidade.
- **Tipo de problema**: regressão
- **Valores de gráfico**: último valor no prazo
- **Detalhes de métricas disponíveis**: nenhum

## Interpretando a exibição
{: #quality_r_squared-display}

![o gráfico de R ao quadrado é exibido.](images/xxxx.png)

## Fazer os cálculos
{: #quality_r_squared-math}

A métrica do R ao quadrado é definida na fórmula a seguir.

```
                  explained variation
R squared =ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling service-  _____________________

                    variação total
```
