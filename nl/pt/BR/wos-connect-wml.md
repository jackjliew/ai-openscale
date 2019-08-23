---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: Watson Studio, Watson Machine Learning, wml, machine learning, services

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

# Especificando uma instância de serviço do {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.pm_short}}
{: #wml-connect}

Sua primeira etapa na ferramenta {{site.data.keyword.aios_short}} é especificar uma instância do {{site.data.keyword.pm_full}}. Sua instância do
{{site.data.keyword.pm_short}} é onde você armazena os modelos e as implementações de IA.
{: shortdesc}

## pré-requisitos
{: #wml-prereq}

É necessário ter provisionado uma instância do {{site.data.keyword.pm_full}} na mesma conta do {{site.data.keyword.Bluemix_notm}} em que a instância de serviço do {{site.data.keyword.aios_short}} está presente. Se você provisionou uma instância do {{site.data.keyword.pm_full}} em alguma outra conta, não será possível configurá-la com a criação de log de carga útil automática com o {{site.data.keyword.aios_short}}.

## Conectar sua instância de serviço do {{site.data.keyword.pm_short}}
{: #wml-config}

O {{site.data.keyword.aios_short}} se conecta a modelos e implementações de IA em uma instância do {{site.data.keyword.pm_full}}.

1.  Na guia **Configurar**, clique em **Provedor de aprendizado de máquina**.

    ![A tela Selecionar seu provedor de serviços do mecanismo de aprendizado de máquina é mostrada com blocos para os mecanismos de aprendizado de máquina suportados](images/wos-machine-learning-providers-selection.png)

2.  Selecione o bloco {{site.data.keyword.pm_full}}. O {{site.data.keyword.aios_short}} verifica a sua conta do {{site.data.keyword.Bluemix_notm}} para localizar quaisquer instâncias existentes do {{site.data.keyword.pm_full}}. 
3. Selecione uma instância no menu suspenso **Serviço Watson Machine Learning**.

    ![Selecionar o serviço {{site.data.keyword.pm_short}}](images/gs-set-wml.png)

4.  (Opcional) Também há a opção de **Selecionar um local diferente** para especificar um local de aprendizado de máquina fora de sua conta do {{site.data.keyword.Bluemix_notm}}. Forneça credenciais para seu local como JSON válido:

    ![Configurar a instância do {{site.data.keyword.pm_short}}](images/gs-get-wml.png)

    Clique em **Salvar**.

1.  O {{site.data.keyword.aios_short}} lista seus modelos implementados. Selecione aqueles que você deseja monitorar e clique em **Configurar**.

### Próximos passos
{: #wml-next}

Agora, o {{site.data.keyword.aios_short}} está pronto para que você [configure monitores](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
