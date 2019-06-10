---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: dashboard, navigating, navigation, insights

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:important: .important}
{:note: .note}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Navegando no painel
{: #io-ov}

É possível rastrear todas as implementações que você está monitorando por meio do painel do {{site.data.keyword.aios_short}}. O painel é a sua visualização principal no {{site.data.keyword.aios_short}}. O painel consiste nas guias a seguir:

  ![Insight tabs](images/insight-tabs.png)

{: shortdesc}

## Insights
{: #io-ins}

A guia **Insights** (![Painel Insight](images/insight-dash-tab.png)) fornece uma visualização de alto nível de seu monitoramento de implementação.

  ![Insight dashboard](images/insight-dashboard.png)

- ***Implementações monitoradas*** - neste exemplo, um total de 10 implementações estão sendo monitoradas. Oito das dez implementações são mostradas como ladrilhos individuais abaixo.

- ***Alertas de precisão*** - um total de 3 alertas de Precisão são representados nos ladrilhos abaixo por sombreamento roxo. Neste exemplo, as implementações `Driver Performance`, `Market Analytics` e `Pricing Risk` mostram valores de Precisão de `60%`, `65%` e `79%`, respectivamente.

- ***Alertas de justiça*** - há um total de 6 alertas de Justiça, representados nos ladrilhos abaixo por sombreamento roxo e por uma pequena tag `BIAS`. Neste exemplo, as implementações `Driver Performance`, `Market Analytics`, `Regulatory Compliance`, `Fraud Detection`, `Premium Optimization` e `Damage Cost Estimator` mostram valores de Justiça de `59%`, `68%`, `62%`, `64%`, `79%` e `63%`, respectivamente.

Cada ladrilho fornece um resumo da atividade de monitoramento para essa implementação. Observe que o ladrilho de implementação `Call Center Routing` não mostra nenhum problema, indicando um modelo razoavelmente estável e preciso.

### Próximos passos
{: #io-next}

Selecione qualquer um dos ladrilhos de implementação individual para visualizar mais detalhes sobre essa implementação. Para obter mais informações, consulte [Monitorando justiça, média de solicitações por minuto e precisão](/docs/services/ai-openscale?topic=ai-openscale-it-ov) e [Monitorando a explicabilidade](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).

## e Segurança
{: #io-conf}

A guia **Configuração** (![Guia Configuração](images/insight-config-tab.png)) abre um Resumo de configuração para a implementação selecionada.

  ![Config summary](images/insight-config-summary.png)

Daqui, é possível editar diretamente as definições de configuração para seu monitor de implementação.

## Transações
{: #io-tran}

Use a guia **Explicar uma transação** (![Guia Explicar uma transação](images/insight-transact-tab.png)) para procurar um ID de transação específico para explicar uma transação de implementação
específica. Para obter mais informações, consulte [Monitorando a explicabilidade](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).

## Guia Ajuda
{: #io-help}

A guia Ajuda (![guia Transações](images/insight-help-tab.png)) fornece informações adicionais para ajudá-lo a usar o {{site.data.keyword.aios_short}}.
