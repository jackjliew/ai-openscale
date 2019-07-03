---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: dashboard, navigating, navigation, insights

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

# Obtendo insights com o {{site.data.keyword.aios_short}}
{: #io-ov}

É possível rastrear todas as implementações que você está monitorando por meio do painel do {{site.data.keyword.aios_full}}. O painel é sua visualização principal para o {{site.data.keyword.aios_short}} e fornece os meios de obtenção de insights sobre como seus modelos estão sendo executados.
{: shortdesc}

## Insights
{: #io-ins}

A guia **Insights** (![Painel Insight](images/insight-dash-tab.png)) fornece uma visualização de alto nível de seu monitoramento de implementação.

  ![Insight dashboard](images/insight-dashboard.png)

- ***Implementações monitoradas*** - neste exemplo, um total de 10 implementações estão sendo monitoradas. Oito das dez implementações a seguir são mostradas como blocos individuais.

- ***Alertas de precisão*** - um total de 3 alertas de Precisão é representado nos blocos a seguir. Neste exemplo, as implementações `Driver Performance`, `Market Analytics` e `Pricing Risk` mostram valores de Precisão de `60%`, `65%` e `79%`, respectivamente.

- ***Alertas de justiça*** - há um total de 6 alertas de Justiça representados nos blocos a seguir e por uma pequena tag `BIAS`. Neste exemplo, as implementações `Driver Performance`, `Market Analytics`, `Regulatory Compliance`, `Fraud Detection`, `Premium Optimization` e `Damage Cost Estimator` mostram valores de Justiça de `59%`, `68%`, `62%`, `64%`, `79%` e `63%`, respectivamente.

Cada ladrilho fornece um resumo da atividade de monitoramento para essa implementação. Observe que o ladrilho de implementação `Call Center Routing` não mostra nenhum problema, indicando um modelo razoavelmente estável e preciso.

### Próximos passos
{: #io-next}

Selecione qualquer um dos ladrilhos de implementação individual para visualizar mais detalhes sobre essa implementação. Para obter mais informações, consulte [Monitorando justiça, média de solicitações por minuto e precisão](/docs/services/ai-openscale?topic=ai-openscale-it-ov) e [Monitorando a explicabilidade](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).



## Transações
{: #io-tran}

Use a guia **Explicar uma transação** (![Guia Explicar uma transação](images/insight-transact-tab.png)) para procurar um ID de transação específico para explicar uma transação de implementação
específica. Para obter mais informações, consulte [Monitorando a explicabilidade](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).


