---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

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

# {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.pm_short}}
{: #frmwrks-wml}

É possível usar o {{site.data.keyword.pm_full}} para executar a criação de log de carga útil e de feedback e para medir a precisão do desempenho, a detecção de propensão de tempo de execução, a explicabilidade e a função de remoção automática de propensão no {{site.data.keyword.aios_full}}.

{{site.data.keyword.aios_full}} suporta totalmente as seguintes estruturas do {{site.data.keyword.pm_full}}: 
{: shortdesc}

Tabela 1. Detalhes do suporte da estrutura

| Estrutura | Tipo de problema | Tipo de dados |
|:---|:---:|:---:|
| Apache Spark MLlib | Classificação | Estruturadas |
| Apache Spark MLLib | Procedimento de | Estruturadas |
| Keras com TensorFlow<sup>1</sup><sup>&</sup><sup>2</sup> | Classificação | Não estruturados (imagem, texto) |
| Keras com TensorFlow<sup>1</sup><sup>&</sup><sup>2</sup> | Procedimento de | Não estruturados (imagem, texto) |
| função Python | Classificação | Estruturadas |
| função Python | Procedimento de | Estruturadas |
| scikit-learn | Classificação | Estruturadas |
| scikit-learn | Procedimento de | Estruturadas |
| XGBoost | Classificação | Estruturadas |
| XGBoost | Procedimento de | Estruturadas |
{: caption="Detalhes do suporte da estrutura" caption-side="top"}

<sup>1</sup>O suporte do Keras não inclui suporte para a justiça.
{: note}

<sup>2</sup>A explicabilidade será suportada se seu modelo/estrutura gerar probabilidades de predição.
{: note}

## Especificando uma instância de serviço do {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.pm_short}}
{: #wml-connect}

Sua primeira etapa na ferramenta {{site.data.keyword.aios_short}} é especificar uma instância do {{site.data.keyword.pm_full}}. Sua instância do
{{site.data.keyword.pm_short}} é onde você armazena os modelos e as implementações de IA.
{: shortdesc}

### pré-requisitos
{: #wml-prereq}

É necessário ter provisionado uma instância do {{site.data.keyword.pm_full}} na mesma conta do {{site.data.keyword.Bluemix_notm}} em que a instância de serviço do {{site.data.keyword.aios_short}} está presente. Se você provisionou uma instância do {{site.data.keyword.pm_full}} em alguma outra conta, não será possível configurá-la com a criação de log de carga útil automática com o {{site.data.keyword.aios_short}}.

### Conectar sua instância de serviço do {{site.data.keyword.pm_short}}
{: #wml-config}

O {{site.data.keyword.aios_short}} se conecta a modelos e implementações de IA em uma instância do {{site.data.keyword.pm_full}}.

1.  Na guia **Configurar**, na área de janela de navegação, clique em **Provedores de aprendizado de máquina**.

    ![A tela Selecionar seu provedor de serviços do mecanismo de aprendizado de máquina é mostrada com blocos para os mecanismos de aprendizado de máquina suportados](images/wos-machine-learning-providers-selection.png)

2.  Clique no botão **Incluir provedor de aprendizado de máquina** e, em seguida, clique no bloco do {{site.data.keyword.pm_full}}. O {{site.data.keyword.aios_short}} verifica a sua conta do {{site.data.keyword.Bluemix_notm}} para localizar quaisquer instâncias existentes do {{site.data.keyword.pm_full}}. 
3. Selecione uma instância no menu suspenso **Serviço Watson Machine Learning**.

    ![Selecionar o serviço {{site.data.keyword.pm_short}}](images/gs-set-wml.png)

4.  (Opcional) Você também tem a opção de **Selecionar um local diferente** para especificar um local de aprendizado de máquina fora de sua conta do {{site.data.keyword.Bluemix_notm}}. Forneça credenciais para seu local como JSON válido:

    ![Configurar a instância do {{site.data.keyword.pm_short}}](images/gs-get-wml.png)

    Clique em **Salvar**.

1.  O {{site.data.keyword.aios_short}} lista seus modelos implementados. Selecione aqueles que você deseja monitorar e clique em **Configurar**.

## Próximos passos
{: #wml-next}

Agora, o {{site.data.keyword.aios_short}} está pronto para que você [configure monitores](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
