---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: credentials, REST API, data mart

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

# Criando credenciais para o {{site.data.keyword.aios_short}}
{: #cred-create}

Para acessar as APIs de REST do {{site.data.keyword.aios_full}}, são necessários uma chave de API da plataforma e um ID do data mart, também conhecido como instância de serviço. A chave de API da Plataforma fornece a um usuário individual a capacidade de acessar recursos no {{site.data.keyword.cloud_notm}}.
{: shortdesc}

Para contas corporativas, um administrador pode criar o data mart, convidar usuários para a conta e fornecer a esses usuários acesso a um data mart específico do {{site.data.keyword.aios_short}}. Um usuário pode criar sua própria chave de API da plataforma e pode acessar o mesmo data mart do {{site.data.keyword.aios_short}}. Não há risco de conflito nem de segurança.

## Criando a chave de API da plataforma
{: #cred-create-apikey}

Para criar uma chave de API da Plataforma, conclua as etapas a seguir:

- Efetue login no [{{site.data.keyword.cloud_notm}}](https://{DomainName}){: external}.

- Selecione **Gerenciar** --> **Segurança** --> **Chaves de API da Plataforma**

    ![Chaves de API da Plataforma](images/cred-api-key.png)

- Crie e salve uma chave de API da Plataforma.

Para localizar seu ID do data mart (ou instância de serviço):

- Na página {{site.data.keyword.aios_short}} **Configuração --> Resumo**, a primeira entrada é seu ID de Data Mart (instância de serviço).

    ![ID do Data Mart](images/data-mart-id.png)

## Criando credenciais de instância de serviço usando o console de comando
{: #cred-creds}

Para criar credenciais para o {{site.data.keyword.aios_short}}, conclua as etapas a seguir usando o [console de comando](/docs/cli?topic=cloud-cli-ibmcloud-cli) do {{site.data.keyword.cloud_notm}}:

1. Recupere a chave de API executando o comando a seguir:

    ```curl
    ibmcloud login --sso
    ibmcloud iam api-key-create 'my_key'
    ```

    A seguinte informação mostra:

    ```bash
    Name         my_key
    Created At   2018-10-09T14:04+0000
    API Key      Tg4Gxxxxxxxxxxxxxxxxx_xxxxxxxxxxxxxxxxxQU-nE
    Locked       false
    UUID         ApiKey-xxxxxxxxx-afd7-xxxxx-b0e1-xxxxxxxxxxx
    ```
2. Verifique o Grupo de recursos que você está usando em sua conta do {{site.data.keyword.cloud_notm}}.

  ![Resource Group in Cloud](images/cloud-resource.png)

  Se você não estiver usando o grupo de recursos `Default`, execute o comando a seguir para obter sua credencial para o {{site.data.keyword.aios_short}}:

   ```curl
   ibmcloud target -g myResourceGroup
   ```

  em que `myResourceGroup` é o nome do grupo de recursos associado à sua instância do {{site.data.keyword.aios_short}}.

3. Recupere o ID da instância do {{site.data.keyword.aios_short}} executando o comando a seguir:

    ```curl
    ibmcloud resource service-instance '<Your_Watson_OpenScale_instance_name>'
    ```
    **Nota**: se você estiver usando o console de comando do {{site.data.keyword.cloud_notm}} no Windows, substitua as aspas simples (') nos comandos anteriores por aspas duplas (").

    A seguinte informação mostra:

    ```bash
    Name:                  AI OpenScale-my_instance
    ID:                    crn:v1:ibmcloud:public:aiopenscale:us-south:a/c2f2xxxxxxxxxxxx867::
    GUID:                  03daxxxx-xxxx-xxxx-xxxx-xxxxxxxx38a7
    Location:              us-south
    Service Name:          aiopenscale
    Service Plan Name:     lite
    Resource Group Name:   Default
    State:                 active
    Type:                  service_instance
    Sub Type:
    Tags:
    Created at:            2018-09-17T13:58:43Z
    Updated at:
    ```

    O valor `GUID` é o seu ID de instância do {{site.data.keyword.aios_short}}.
        
## Próximos passos
{: #cred-create-next-steps}

Especifique seu provedor de aprendizado de máquina:

- [Especificando uma instância de serviço do IBM Watson Machine Learning](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-wml-connect)
- [Especificando uma instância do Microsoft Azure ML Studio](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-connect-azure)
- [Especificando uma instância de serviço do Amazon SageMaker ML](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-csm-connect)
- [Especificando uma Instância de Serviço ML Customizada](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-co-connect)
