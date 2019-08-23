---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Proportion explained variance

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

# Variação explicada da proporção
{: #quality_var}

A Variação explicada da proporção fornece a razão da variação explicada e a variação de destino. A variação explicada é a diferença entre a variância de destino e a variância do erro de predição.
{: shortdesc}

## Visão rápida da Variação explicada da proporção
{: #quality_var-glance}

- **Descrição**: a variância explicada da proporção é a proporção de variação explicada e a variação de destino. A variação explicada é a diferença entre a variância de destino e a variância do erro de predição.
- **Limites padrão**: limite inferior = 80%
- **Recomendação padrão**:
   - **Tendência ascendente**: uma tendência ascendente indica que a métrica está melhorando. Isso significa que a reciclagem dos modelos é eficaz.
   - **Tendência descendente**: uma tendência descendente indica que a métrica está se deteriorando. Os dados de feedback estão se tornando significativamente diferentes dos dados de treinamento.
   - **Variação errática ou irregular**: uma variação errática ou irregular indica que os dados de feedback não são consistentes entre as avaliações. Aumente o tamanho de amostra mínimo para o monitor de Qualidade.
- **Tipo de problema**: regressão
- **Valores de gráfico**: último valor no prazo
- **Detalhes de métricas disponíveis**: nenhum

## Interpretando a exibição
{: #quality_var-display}

![o gráfico de Variação explicada da proporção é exibido.](images/xxxx.png)

## Fazer os cálculos
{: #quality_var-math}

A Variação explicada da proporção é calculada pela média dos números e, em seguida, para cada número, subtraindo a média e o quadrado dos resultados. Em seguida, trabalhe os quadrados

```
                                  soma de quadrados entre grupos
Variação explicada da proporção =  ________________________________

                                      soma do total dos quadrados
```
