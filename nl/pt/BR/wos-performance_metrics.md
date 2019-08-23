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

# Visão geral das métricas de desempenho ![tag beta](images/beta.png)
{: #anlz_metrics_performance}

Use o monitoramento de desempenho para saber a velocidade dos registros de dados processados por sua implementação. Você ativa o monitoramento de desempenho ao selecionar a implementação a ser rastreada e monitorada pelo {{site.data.keyword.aios_short}}.
{: shortdesc}

As métricas de desempenho são calculadas com base nas informações a seguir:

- dados de carga útil de pontuação

Para um propósito de monitoramento adequado, cada solicitação de pontuação deve ser registrada no {{site.data.keyword.aios_short}} também. A criação de log de dados de carga útil é automatizada para mecanismos do {{site.data.keyword.pm_full}}. Para outros mecanismos de aprendizado de máquina, os dados de carga útil podem ser fornecidos usando o cliente Python ou a API de REST. O monitoramento de desempenho não cria nenhuma solicitação de pontuação adicional na implementação monitorada.

É possível revisar o valor das métricas de desempenho ao longo do tempo no painel do {{site.data.keyword.aios_short}}:

![gráfico de desempenho](images/performance_metrics_001.png)

## Métricas de desempenho suportadas
{: #anlz_metrics_performance_supp_quality_mets}

As métricas de desempenho a seguir são suportadas pelo {{site.data.keyword.aios_short}}:

- [Rendimento](/docs/services/ai-openscale?topic=ai-openscale-performance_mets_through)
