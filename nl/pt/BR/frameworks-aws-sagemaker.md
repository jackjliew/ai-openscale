---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: supported frameworks, models, model types, limitations, limits, AWS, Sagemaker, Amazon

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

# Estruturas Amazon SageMaker
{: #frmwrks-aws-sage}

O {{site.data.keyword.aios_full}} suporta totalmente as estruturas do Amazon SageMaker a seguir:
{: shortdesc}

Tabela 1. Detalhes do suporte da estrutura

| Estrutura | Tipo de problema | Tipo de dados |
|:---|:---:|:---:|
| Nativo | Classificação | Estruturados |
{: caption="Detalhes do suporte da estrutura" caption-side="top"}


## Incluindo o Amazon SageMaker no {{site.data.keyword.aios_short}}
{: #frmwrks-aws-sage-add}

É possível configurar o {{site.data.keyword.aios_short}} para trabalhar com o Amazon SageMaker usando um dos métodos a seguir:

- Se essa for a primeira vez que você está incluindo um provedor de aprendizado de máquina no {{site.data.keyword.aios_short}}, será possível usar a interface de configuração. Para obter mais informações, consulte [Especificando uma instância do Amazon SageMaker](/docs/services/ai-openscale?topic=ai-openscale-csm-connect).
- Também é possível incluir o seu provedor de aprendizado de máquina usando o Python SDK. Deve-se usar este método caso você deseje ter mais de um provedor. Para obter mais informações sobre como executar isso programaticamente, consulte [Ligue o seu mecanismo de aprendizado de máquina do Amazon SageMaker](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind).


## Blocos de notas de amostra
{: #frmwrks-aws-sage-smpl-ntbks}

As anotações a seguir mostram como trabalhar com o Amazon SageMaker:

- [Criação e implementação do modelo de previsão de risco de crédito](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Credit%20%20model%20with%20SageMaker%20linear-learner%20.ipynb){: external}
- [Criação de data mart, monitoramento de implementação de modelo e análise de dados](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20SageMaker%20ML%20Engine.ipynb){: external}


## Explorar mais
{: #frmwrks-aws-sage-mediumblogs}

[Monitorar aprendizado de máquina do SageMaker com o Watson OpenScale](https://developer.ibm.com/patterns/monitor-amazon-sagemaker-machine-learning-models-with-ai-openscale//){: external}
