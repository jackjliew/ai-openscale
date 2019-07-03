---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: drift, behavior, metrics

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

# Detecção de desvio ![tag beta](images/beta.png)
{: #behavior-drift-ovr}

Ao longo do tempo, a importância e o impacto de determinados recursos em um modelo mudam. Isso afeta os aplicativos associados e os resultados dos negócios. Por meio da detecção de desvio, o {{site.data.keyword.aios_short}} fornece uma maneira de rastrear as métricas do modelo, o desempenho do modelo e a maneira com que os pesos do recurso mudam ao longo do tempo. Desvio é a degradação do desempenho preditivo ao longo do tempo devido ao contexto oculto. À medida que seus dados mudam com o tempo, a capacidade de seu modelo fazer predições precisas pode decair. O {{site.data.keyword.aios_short}} detecta e destaca o desvio para que seja possível tomar uma ação corretiva.
{: shortdesc}

O {{site.data.keyword.aios_short}} analisa todas as transações para localizar aquelas que contribuem para o desvio. Em seguida, ele agrupa os registros com base nos valores de atributos que eram significativos na contribuição para o desvio.

## Visão rápida do desvio
{: #behavior-drift-glance}




## Interpretando a exibição
{: #behavior-drift-display}

![gráfico de métricas de justiça mostrando o desvio inferior ao limite configurado](images/fairness_metrics_001.png)


## Faça as contas
{: #behavior-drift-math}

O {{site.data.keyword.aios_short}} calcula o desvio 
