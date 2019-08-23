---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"


keywords: supported frameworks, models, model types, limitations, limits, spss, c&ds

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Estruturas do IBM SPSS C & DS
{: #frmwrks-spss}

É possível usar o IBM SPSS C&DS para executar a criação de log de carga útil e de feedback e para medir a precisão do desempenho, a detecção de propensão de tempo de execução, a explicabilidade e a função de remoção automática de propensão no {{site.data.keyword.aios_full}}.

O {{site.data.keyword.aios_full}} planeja suportar totalmente as seguintes estruturas do IBM SPSS Collaboration and Deployment Services (C&DS):
{: shortdesc}

Atualmente, o suporte é limitado ao {{site.data.keyword.wos4d_full}}.
{: note}

Tabela 1. Detalhes do suporte da estrutura

| Estrutura | Tipo de problema | Tipo de dados |
|:---|:---:|:---:|
| SPSS | Classificação | Estrutura |
{: caption="Detalhes do suporte da estrutura" caption-side="top"}

Se o `ID de implementação` para uma assinatura contiver um sublinhado, a precisão sem propensão que normalmente aparece na guia sem propensão de métricas de justiça não será vista.
{: note}


## Suporte à explicabilidade para as estruturas do IBM SPSS Collaboration and Deployment Services (C&DS)
{: #frmwrks-spss-exp-supp}

- A explicabilidade é suportada para modelos binários e para modelos de multiclasses do SPSS que retornam probabilidades para todas as classes. 
- A explicabilidade não é suportada para modelos de multiclasses do SPSS que retornam apenas a probabilidade da classe vencedora.



