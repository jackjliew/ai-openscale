---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: supported frameworks, models, model types, limitations, limits, custom machine learning engine, custom

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

# Estruturas ML customizadas
{: #frmwrks-custom}

O {{site.data.keyword.aios_full}} suporta totalmente as estruturas de aprendizado de máquina customizado a seguir:
{: shortdesc}

Tabela 1. Detalhes do suporte da estrutura

| Estrutura | Tipo de problema | Tipo de dados |
|:---|:---:|:---:|
| Equivalente a {{site.data.keyword.pm_full}} | Classificação | Estruturados |
{: caption="Detalhes do suporte da estrutura" caption-side="top"}

## Incluindo um mecanismo de aprendizado de máquina customizado no {{site.data.keyword.aios_short}}
{: #frmwrks-custom-add}

É possível configurar o {{site.data.keyword.aios_short}} para trabalhar com um provedor de aprendizado de máquina customizado usando um dos métodos a seguir:

- Se essa for a primeira vez que você está incluindo um provedor de aprendizado de máquina customizado no {{site.data.keyword.aios_short}}, será possível usar a interface de configuração. Para obter mais informações, consulte [Especificando uma instância de aprendizado de máquina customizado](/docs/services/ai-openscale?topic=ai-openscale-co-connect).
- Também é possível incluir o seu provedor de aprendizado de máquina usando o Python SDK. Deve-se usar este método caso você deseje ter mais de um provedor. Para obter mais informações sobre como executar isso programaticamente, consulte [Ligar seu mecanismo de aprendizado de máquina customizado](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-cusbind).


## Blocos de notas de amostra
{: #frmwrks-custom-smpl-ntbks}

- [Criação do mecanismo de Aprendizado de máquina customizado usando o cluster Kubernetes](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix){: external}
- [Criação de data mart, monitoramento de implementação de modelo e análise de dados](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}

## Explorar mais
{: #frmwrks-custom-mediumblogs}

[Monitorar o mecanismo de aprendizado de máquina customizado com o Watson OpenScale](https://developer.ibm.com/patterns/monitor-custom-machine-learning-engine-with-ai-openscale/){: external}
