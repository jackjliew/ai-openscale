---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: payload, non-Watson, machine learning, services, subscription

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

# Criação de log de carga útil para instâncias de serviço não {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.pm_short}}
{: #cml-connect}

If your AI model is deployed in a machine learning engine other than {{site.data.keyword.pm_full}}, you must enable payload logging for the external machine learning engine with a Python client
{: shortdesc}

Veja informações mais completas na [documentação do cliente Python do {{site.data.keyword.aios_short}}](http://ai-openscale-python-client.mybluemix.net/){: external} e nos blocos de notas do cliente Python do {{site.data.keyword.aios_short}} que fazem parte dos [tutoriais do {{site.data.keyword.aios_short}}](https://github.com/pmservice/ai-openscale-tutorials/blob/master/README.md){: external}.

## Antes de Começar
{: #cml-prereq}

Você precisará ter os dados de treinamento de seu modelo disponíveis no Db2 ou {{site.data.keyword.cos_full}} para monitorar a propensão para seu modelo. A explicabilidade e a precisão não são suportadas para as funções Python. Para
obter mais informações sobre os dados de treinamento, veja [Por que o {{site.data.keyword.aios_short}} precisa de acesso aos meus dados de treinamento?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)

- Importar e iniciar o {{site.data.keyword.aios_short}}

    ```python
    a partir de ibm_ai_openscale import APIClient

    aios_credentials = {
      "instance_guid": "***",
      "url": "https://api.aiopenscale.cloud.ibm.com",
      "apikey": "***"
    }

    cliente = APIClient (service_credentials)
    ```
  As credenciais podem ser localizadas seguindo as etapas mostradas no tópico "[Criando credenciais](/docs/services/ai-openscale?topic=ai-openscale-cred-create)".

- Crie um nome de esquema em seu banco de dados PostgreSQL

- Configurar um datamart

    ```python
    client.data_mart.setup (db_credentials = postgres_credentials, schema=schemaName)

    client.data_mart.get_details ()
    ```


## Próximos passos
{: #cml-next}

- Para continuar com o cliente do {{site.data.keyword.aios_short}}, consulte [Configurando o monitor Precisão ou Qualidade](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor).
- Para continuar com a biblioteca de comandos do Python, consulte a [documentação do cliente Python](http://ai-openscale-python-client.mybluemix.net/){: external}.
