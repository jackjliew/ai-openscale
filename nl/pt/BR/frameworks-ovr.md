---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: supported frameworks, models, model types, limitations, limits

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

# Mecanismos de aprendizado de máquina, estruturas e modelos suportados
{: #in-fram}

O serviço {{site.data.keyword.aios_short}} suporta os mecanismos de aprendizado de máquina a seguir. Cada tempo de execução suporta modelos que são criados nas estruturas a seguir:

- [{{site.data.keyword.pm_full}}](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-wml#frmwrks-wml) 
- [Azure ML Studio](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azure#frmwrks-azure)
- [AWS SageMaker](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-aws-sage#frmwrks-aws-sage)
- [Customizado](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-custom#frmwrks-custom)
- [SPSS C&DS](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-spss#frmwrks-spss) (disponível somente no {{site.data.keyword.wos4d_full}})

- [SAS AI Studio](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-sas#frmwrks-sas)
{: download}
- [Google Cloud ML Engine](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-google#frmwrks-google)
{: download}

O suporte completo inclui os recursos a seguir para a estrutura específica, problema e tipo de dados:

- Registro de carga útil	
- Criação de log de feedback	
- Precisão de desempenho	
- Detecção de propensão de tempo de execução	
- Explicabilidade	
- Despropensão automática

<p>&nbsp;</p>


## Tipos de Modelos Suportados
{: #abt-models}

Tabela 1. Detalhes do suporte do modelo

| Algoritmos | **Justiça** | **Despropensão automática** | **Explicar** | **Precisão** |
|:---|:---:|:---:|:---:|:---:|
| **Classificação estruturada** | Sim | Sim<sup>1</sup> | Sim<sup>1</sup> | Sim |
| **Regressão estruturada**     | Sim | Em breve | Sim | Sim |
| **Classificação de texto**       | Não-tópico de investigação activa | Não-tópico de investigação activa | Sim<sup>1</sup> | Não |
| **Classificação de imagem**      | Não-tópico de investigação activa | Não-tópico de investigação activa | Sim<sup>1</sup> | Não ||
{: caption="Detalhes do suporte do modelo" caption-side="top"}

<sup>1</sup> Se seu modelo/estrutura gerar saída de probabilidades de predição

<p>&nbsp;</p>

## Suporte do Navegador
{: #in-brw}

O conjunto de ferramentas do serviço {{site.data.keyword.aios_short}} requer o mesmo nível de software do navegador que é requerido pelo {{site.data.keyword.cloud_notm}}. Consulte o tópico {{site.data.keyword.cloud_notm}} [Pré-requisitos](/docs/overview?topic=overview-prereqs-platform#browsers-platform) para obter detalhes.

<p>&nbsp;</p>

## Ferramenta CLI do ModelOps
{: #in-mop}

A [ferramenta de operações de modelo da CLI do {{site.data.keyword.aios_short}}](https://github.com/IBM-Watson/aiopenscale-modelops-cli){: external} permite executar tarefas relacionadas ao gerenciamento de ciclo de vida de modelos de aprendizado de máquina. Essa ferramenta é complementar à ferramenta da CLI do {{site.data.keyword.cloud_notm}}, aumentada com o [plug-in de aprendizado de máquina](https://www.ibm.com/support/knowledgecenter/DSXDOC/analyze-data/ml_dlaas_environment.html){: external}.

<p>&nbsp;</p>

## Cliente Python
{: #in-pyc}

O [cliente Python do {{site.data.keyword.aios_short}}](http://ai-openscale-python-client.mybluemix.net/){: external} é uma biblioteca Python que permite que você trabalhe diretamente com o serviço {{site.data.keyword.aios_short}} no {{site.data.keyword.cloud_notm}}. É possível usar o cliente Python, em vez da UI do cliente do {{site.data.keyword.aios_short}}, para configurar diretamente um banco de dados de criação de log, ligar seu mecanismo de aprendizado de máquina e selecionar e monitorar implementações. Para obter exemplos usando o cliente Python dessa maneira, consulte os [blocos de notas de amostra do {{site.data.keyword.aios_short}}](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks).

<p>&nbsp;</p>

## Próximos passos
{: #in-next}

- [Introdução](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted) ao serviço.
- Visualizar o [material de Referência da API](https://{DomainName}/apidocs/ai-openscale){: external}.

Você ainda tem dúvidas? 

- [O quê há de novo](/docs/services/ai-openscale?topic=ai-openscale-rn-relnotes)
- [Entrar em contato com a IBM](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson){: external}.
