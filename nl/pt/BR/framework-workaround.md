---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: machine learning engines, frameworks, Microsoft Azure, Amazone SageMaker, custom ML engine 

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

# Integrando mecanismos de aprendizado de máquina de terceiros ao {{site.data.keyword.aios_short}}
{: #fmrk-workaround}

O {{site.data.keyword.aios_full}} integra-se aos mecanismos de serviço de aprendizado de máquina externos, como Microsoft Azure ML Studio e Amazon SageMaker.
{: shortdesc}

É possível integrar o {{site.data.keyword.aios_short}} aos mecanismos de terceiros das maneiras a seguir:

- Nível de ligação do mecanismo: capacidade de listar implementações e obter detalhes da implementação.
  
- Nível de assinatura da implementação: o {{site.data.keyword.aios_short}} precisa ser capaz de pontuar a implementação inscrita no formato necessário, como o formato do {{site.data.keyword.pm_full}}, e de receber a saída no mesmo formato compatível. O {{site.data.keyword.aios_short}} deve ser configurado para processar os formatos de entrada e de saída.
   

- Criação de log de carga útil: cada entrada e cada saída para o modelo implementado acionado pelo aplicativo de um usuário devem ser armazenadas em um armazenamento de carga útil. O formato dos registros de carga útil segue a mesma especificação, conforme mencionado na seção anterior, nos níveis de assinatura de implementação.
   
   O {{site.data.keyword.aios_short}} usa esses registros para calcular propensões, explicações e outros aspectos. O {{site.data.keyword.aios_short}} não pode armazenar automaticamente transações que são executadas no site do usuário, que está fora do sistema {{site.data.keyword.aios_short}}. Esta é uma das maneiras de o {{site.data.keyword.aios_short}} salvaguardar informações protegidas por direitos autorais. Use a API de REST do {{site.data.keyword.aios_short}} ou o SDK do Python para trabalhar com dados seguros.
   
## Etapas para implementar essa solução
{: #fmrk-workaround-steps}

1. [Aprender sobre mecanismos de aprendizado de máquina customizados](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-customengine).
2. [Configurar a criação de log de carga útil](/docs/services/ai-openscale?topic=ai-openscale-cdb-payload).
3. [Automatizar a criação de log de carga útil](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-pyld-lg).
4. Configurar um mecanismo de aprendizado de máquina customizado usando um destes [Exemplos de mecanismos de aprendizado de máquina customizados](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-cstmmlsengex).

