---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: supported frameworks, models, model types, limitations, limits, azure

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

# Estruturas do Microsoft Azure ML Service
{: #frmwrks-azure-service}

O {{site.data.keyword.aios_full}} suporta totalmente as estruturas do Microsoft Azure Machine Learning Service a seguir:
{: shortdesc}

Tabela 1. Detalhes do suporte da estrutura

| Estrutura | Tipo de problema | Tipo de dados |
|:---|:---:|:---:|
| Nativo | Classificação | Estruturados |
{: caption="Detalhes do suporte da estrutura" caption-side="top"}

## Incluindo o Microsoft Azure ML Service no {{site.data.keyword.aios_short}}
{: #frmwrks-azure-add}

É possível configurar o {{site.data.keyword.aios_short}} para trabalhar com o Microsoft Azure ML Service usando um dos métodos a seguir:

- Se essa for a primeira vez que você está incluindo um provedor de aprendizado de máquina no {{site.data.keyword.aios_short}}, será possível usar a interface de configuração. Para obter mais informações, consulte [Especificando uma instância do Microsoft Azure ML Studio](/docs/services/ai-openscale?topic=ai-openscale-connect-azure).
- Também é possível incluir o seu provedor de aprendizado de máquina usando o Python SDK. Deve-se usar este método caso você deseje ter mais de um provedor. Para obter mais informações sobre como executar isso programaticamente, consulte [Ligue o seu mecanismo de aprendizado de máquina do Microsoft Azure](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind).


Carga útil integrada do usuário necessária para metadados.
Crie a IU de integração
do modelo para configurar o monitoramento para
fazer upload de dados de treinamento/anotações. O OpenScale precisa de informações
para executar a criação de log de carga útil,
IU - atualização

Ônus no implementador 

MJS: acompanhamento com Lukasz e Clifford Chu

A

## Blocos de notas de amostra
{: #frmwrks-azure-smpl-ntbks}

As anotações a seguir mostram como trabalhar com o Microsoft Azure ML Service:

- [Criação de data mart, monitoramento de implementação de modelo e análise de dados](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}
- [Exemplos de pontuação de modelo do MS Azure Service](https://dataplatform.cloud.ibm.com/analytics/notebooks/v2/0d4ebd8d-87cb-4c38-8ba8-37f5623df131/view?access_token=fcb2c411aed913bf94f86f434184db67aef1a6b304824b86b4ad63686e4890be){: external}

## Explorar mais
{: #frmwrks-azure-mediumblogs}

[Monitorar aprendizado de máquina do Azure com o Watson OpenScale](https://developer.ibm.com/patterns/monitor-azure-machine-learning-studio-models-with-ai-openscale/){: external}
