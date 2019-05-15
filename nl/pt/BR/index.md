---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

keywords: supported frameworks, models, model types, limitations, limits

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
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

# Sobre
{: #in-ov}

O {{site.data.keyword.aios_full}} é um ambiente de classificação corporativa para aplicativos desenvolvidos com IA, fornecendo visibilidade às empresas sobre como a IA está sendo construída e usada e entregando retorno sobre investimento na escala de seu negócio.
{: shortdesc}

<p>&nbsp;</p>

## Implementação
{: #in-imp}

Aqui está como você implementará {{site.data.keyword.aios_short}}:

- **Configurar o {{site.data.keyword.aios_short}}**: com o ambiente gráfico fácil de usar, [configure um banco de dados de criação de log de carga útil](/docs/services/ai-openscale?topic=ai-openscale-connect-db) e a [instância do Watson Machine Learning](/docs/services/ai-openscale?topic=ai-openscale-wml-connect) na qual seus modelos e implementações de IA são armazenados.

- **Trabalhar com monitores**: para cada implementação, configure como o {{site.data.keyword.aios_short}} monitorará essa implementação. É possível monitorar o para:

    - [Justiça](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor)
    - [Precisão](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor)

- **Visualizar e editar dados monitorados**: o {{site.data.keyword.aios_short}} painel do [](/docs/services/ai-openscale?topic=ai-openscale-io-ov) permite visualizar facilmente os insights de chave e identificar problemas para suas implementações. A visualização de pontos de dados individuais para cada recurso monitorado fornece detalhes adicionais.

<p>&nbsp;</p>

## Limitações
{: #in-lim}

- A liberação atual suporta somente um banco de dados, uma instância do Watson Machine Learning e uma instância do {{site.data.keyword.aios_short}}

- A instância do banco de dados e do Watson Machine Learning deve ser implementada na mesma conta do {{site.data.keyword.cloud_notm}}.

- O plano Lite (grátis) tem os limites mensais a seguir:

    - Dois modelos implementados monitorados
    - 20 transações explicadas
    - 50.000 registros de carga útil (acumulativos)
    - 50.000 registros de feedback (acumulativos)

- O {{site.data.keyword.aios_short}} usa um banco de dados PostgreSQL ou Db2 para armazenar o resultado da implementação de modelo e os dados de novo treinamento. Os planos Lite do Db2 não são suportados atualmente.

- Há um limite de licença de 20 modelos implementados por instância do {{site.data.keyword.aios_short}}.

- Atualmente, as explicações não podem ser geradas para imagens que são maiores que 1 MB de tamanho.

<p>&nbsp;</p>

## Tipos de Modelos Suportados
{: #in-mod}

Tabela 1. Detalhes do suporte do modelo

| Algoritmos | **Justiça** | **Despropensão automática** | **Explicar** | **Precisão** |
|:---|:---:|:---:|:---:|:---:|
| **Classificação estruturada** | Sim | Sim<sup>1</sup> | Sim | Sim |
| **Regressão estruturada**     | Sim | Não | Sim | Sim |
| **Classificação de texto**       | Não | Não | Sim | Não |
| **Classificação de imagem**      | Não | Não | Sim | Não ||
{: caption="Detalhes do suporte do modelo" caption-side="top"}

<sup>1</sup> Se seu modelo/estrutura gerar saída de probabilidades de predição

<p>&nbsp;</p>

## Mecanismos e estruturas de aprendizado de máquina suportados
{: #in-fram}

O serviço {{site.data.keyword.aios_short}} suporta os mecanismos de aprendizado de máquina a seguir. Cada tempo de execução suporta modelos criados nas estruturas a seguir, conforme descrito na lista de [Tipos de modelos suportados](#in-mod).

- [{{site.data.keyword.pm_full}}](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-wml#frmwrks-wml) 
- [Azure ML Studio](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-azure#frmwrks-azure)
- [AWS Sagemaker](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-aws-sage#frmwrks-aws-sage)
- [Customizado](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-custom#frmwrks-custom)


- [SAS AI Studio](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-sas#frmwrks-sas)
{: download}
- [Google Cloud ML Engine](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-google#frmwrks-google)
{: download}
- [SPSS C&DS (somente ICP)](/docs/services/ai-openscale?topic=ai-openscale-frmwrks-spss#frmwrks-spss)
{: download}

O suporte completo inclui os recursos a seguir para a estrutura específica, problema e tipo de dados:

- Registro de carga útil	
- Criação de log de feedback	
- Precisão de desempenho	
- Detecção de propensão de tempo de execução	
- Explicabilidade	
- Despropensão automática

<p>&nbsp;</p>

## Suporte do Navegador
{: #in-brw}

O conjunto de ferramentas do serviço {{site.data.keyword.aios_short}} requer o mesmo nível de software do navegador que é requerido pelo {{site.data.keyword.cloud_notm}}. Consulte o tópico {{site.data.keyword.cloud_notm}} [Pré-requisitos](/docs/overview?topic=overview-prereqs-platform#browsers-platform) para obter detalhes.

<p>&nbsp;</p>

## Ferramenta CLI do ModelOps
{: #in-mop}

A ferramenta de operações de modelo da CLI do [{{site.data.keyword.aios_short}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/IBM-Watson/aiopenscale-modelops-cli){: new_window} permite executar tarefas relacionadas ao gerenciamento de ciclo de vida de modelos de aprendizado de máquina. Essa ferramenta é complementar à ferramenta da CLI do {{site.data.keyword.cloud_notm}}, aumentada com o [plug-in de aprendizado de máquina ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/support/knowledgecenter/DSXDOC/analyze-data/ml_dlaas_environment.html){: new_window}.

<p>&nbsp;</p>

## Cliente Python
{: #in-pyc}

O [cliente Python do {{site.data.keyword.aios_short}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://ai-openscale-python-client.mybluemix.net/){: new_window} é uma biblioteca Python que permite trabalhar diretamente com o serviço {{site.data.keyword.aios_short}} no {{site.data.keyword.cloud_notm}}. É possível usar o cliente Python, em vez da UI do cliente do {{site.data.keyword.aios_short}}, para configurar diretamente um banco de dados de criação de log, ligar seu mecanismo de aprendizado de máquina e selecionar e monitorar implementações. Para obter exemplos de como usar o cliente Python dessa maneira, consulte os [blocos de notas de amostra do {{site.data.keyword.aios_short}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks).

<p>&nbsp;</p>

## Próximos passos
{: #in-next}

- [Introdução](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted) ao serviço.
- Visualize o [Material de Referência da API ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/ai-openscale){: new_window}.

Você ainda tem dúvidas? [Entre em contato com a IBM ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson){: new_window}.
