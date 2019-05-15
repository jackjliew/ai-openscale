---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

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

É possível rastrear todas as implementações que você está monitorando por meio do painel do {{site.data.keyword.aios_short}}. O painel é a sua visualização principal no {{site.data.keyword.aios_short}}. O painel consiste em cinco guias:

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

A guia **Explicar uma transação** (![Guia Explicar uma transação](images/insight-transact-tab.png)) permite procurar um ID de transação específico para explicar uma determinada transação de implementação. Para obter mais informações, consulte [Monitorando a explicabilidade](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).

## Ferramentas de IA
{: #io-too}

A guia **Ferramentas de IA** (![Guia Ferramentas de IA](images/aitools.png)) abre um diálogo que fornece um link para opções adicionais de ferramentas de IA da IBM:

- *[Plano Lite do Watson Studio ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://dataplatform.cloud.ibm.com/registration/stepone?apps=all&context=wdp){: new_window}*: o Watson Studio fornece o ambiente e as ferramentas para analisar e visualizar dados, limpar e modelar dados, ingerir dados de fluxo contínuo ou criar, treinar e implementar modelos de aprendizado de máquina. Clique no link "Inscreva-se para obter o plano Lite grátis do Watson Studio" para obter o Watson Studio.

- *[NeuNetS ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://dataplatform.cloud.ibm.com/ml/neunets){: new_window}* (*Beta*): o Neural Network Synthesizer, ou "NeuNetS", atualmente na liberação beta, permite sintetizar modelos de IA usando a tecnologia {{site.data.keyword.aios_short}} no Watson Studio. Clique no botão "Sintetizar um modelo" para trabalhar com o NeuNetS.

  ![Diálogo do NeuNetS](images/neunets-dialog.png)

## Guia Ajuda
{: #io-help}

A guia Ajuda (![guia Transações](images/insight-help-tab.png)) fornece informações adicionais para ajudá-lo a usar o {{site.data.keyword.aios_short}}.
