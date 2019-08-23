---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits, azure, studio

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

# Estruturas Microsoft Azure ML Studio
{: #frmwrks-azure}

É possível usar o Microsoft Azure ML Studio para executar a criação de log de carga útil e de feedback e para medir a precisão do desempenho, a detecção de propensão de tempo de execução, a explicabilidade e a função de remoção automática de propensão no {{site.data.keyword.aios_full}}.

O {{site.data.keyword.aios_full}} suporta totalmente as estruturas do Microsoft Azure Machine Learning Studio a seguir:
{: shortdesc}

Tabela 1. Detalhes do suporte da estrutura

| Estrutura | Tipo de problema | Tipo de dados |
|:---|:---:|:---:|
| Nativo | Classificação | Estruturadas |
| Nativo | Procedimento de | Estruturadas |
{: caption="Detalhes do suporte da estrutura" caption-side="top"}

## Incluindo o Microsoft Azure ML Studio no {{site.data.keyword.aios_short}}
{: #frmwrks-azure-add}

É possível configurar o {{site.data.keyword.aios_short}} para trabalhar com o Microsoft Azure ML Studio usando um dos métodos a seguir:

- Se essa for a primeira vez que você está incluindo um provedor de aprendizado de máquina no {{site.data.keyword.aios_short}}, será possível usar a interface de configuração. Para obter mais informações, consulte [Especificando uma instância do Microsoft Azure ML Studio](/docs/services/ai-openscale?topic=ai-openscale-connect-azure).
- Também é possível incluir o seu provedor de aprendizado de máquina usando o Python SDK. Deve-se usar este método caso você deseje ter mais de um provedor. Para obter mais informações sobre como executar isso programaticamente, consulte [Ligue o seu mecanismo de aprendizado de máquina do Microsoft Azure](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind).


## Blocos de notas de amostra
{: #frmwrks-azure-smpl-ntbks}

As anotações a seguir mostram como trabalhar com o Microsoft Azure ML Studio:

- [Criação de data mart, monitoramento de implementação de modelo e análise de dados](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}
- [Exemplos de pontuação de modelo do MS Azure Service](https://dataplatform.cloud.ibm.com/analytics/notebooks/v2/0d4ebd8d-87cb-4c38-8ba8-37f5623df131/view?access_token=fcb2c411aed913bf94f86f434184db67aef1a6b304824b86b4ad63686e4890be){: external}

## Explorar mais
{: #frmwrks-azure-mediumblogs}

-[Monitorar o aprendizado de máquina do Azure com o Watson OpenScale](https://developer.ibm.com/patterns/monitor-azure-machine-learning-studio-models-with-ai-openscale/){: external}
- [Como o serviço Azure Machine Learning difere do Studio?](https://docs.microsoft.com/en-us/azure/machine-learning/service/overview-what-is-azure-ml#how-does-azure-machine-learning-service-differ-from-studio){: external}
- [Consumir um modelo de aprendizado de máquina do Azure implementado como um serviço da web](https://docs.microsoft.com/en-us/azure/machine-learning/service/how-to-consume-web-service){: external}

## Especificando uma instância do Microsoft Azure ML Studio
{: #connect-azure}

Sua primeira etapa na ferramenta {{site.data.keyword.aios_short}} é especificar uma instância
do Microsoft Azure ML Studio. Sua instância do Azure ML Studio é onde você armazena seus modelos e
implementações de IA.
{: shortdesc}

Também é possível incluir o seu provedor de aprendizado de máquina usando o Python SDK. Para obter mais informações sobre como executar isso programaticamente, consulte [Ligue o seu mecanismo de aprendizado de máquina do Microsoft Azure](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind).

### Conecte sua instância do Azure ML Studio
{: #ca-connect}

O {{site.data.keyword.aios_short}} se conecta aos modelos e implementações de IA em uma
instância do Azure ML Studio.

1.  Na guia **Configurar**, na área de janela de navegação, clique em **Provedores de aprendizado de máquina**.

    ![A tela Selecionar seu provedor de serviços do mecanismo de aprendizado de máquina é mostrada com blocos para os mecanismos de aprendizado de máquina suportados](images/wos-machine-learning-providers-selection.png)

1.  Clique no botão **Incluir provedor de aprendizado de máquina** e, em seguida, clique no bloco **Microsoft Azure ML Studio**.

    ![Insira as credenciais do Azure ML Studio](images/connect-azure-cred.png)

1.  Insira e salve suas credenciais:

    - ID do cliente: o valor de sequência real de seu ID do cliente, que verifica quem você é, além de autenticar e autorizar chamadas feitas para o Azure Studio.
    - Segredo do cliente: o valor de sequência real do segredo, que verifica quem você é, além de autenticar e autorizar chamadas feitas para o Azure Studio.
    - Locatário: seu ID do locatário corresponde à sua organização e é uma instância dedicada do Azure AD. Para localizar o ID do locatário, passe o mouse sobre o nome de sua conta para obter o ID do diretório/locatário ou selecione Azure Active Directory > Propriedades > ID do diretório no portal do Azure.
    - ID da assinatura: credenciais de assinatura que identificam exclusivamente a assinatura do Microsoft Azure. O ID da assinatura faz parte do URI de cada chamada de serviço.

    Consulte [Como: Usar o portal para criar um aplicativo e uma entidade de serviço do Microsoft Azure Active Directory que possa acessar recursos](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: external} para obter instruções sobre como obter suas credenciais do Microsoft Azure.
    {: note}

1.  O {{site.data.keyword.aios_short}} lista seus modelos implementados. Selecione aqueles que você deseja monitorar e clique em **Configurar**.

Você selecionou com êxito as implementações.

## Criação de log de carga útil com o mecanismo do Microsoft Azure Machine Learning Studio
{: #cml-azconfig}

### Ligar seu mecanismo de aprendizado de máquina do Microsoft Azure
{: #cml-azbind}

- Um mecanismo não {{site.data.keyword.pm_full}} é ligado como Customizado, o que significa que isso se trata apenas de metadados; não há integração direta com o serviço não {{site.data.keyword.pm_full}}.

    ```python
    AZURE_ENGINE_CREDENTIALS = {
    "client_id": "***",
    "client_secret": "***",
    "subscription_id": "***",
    "tenant": "***"
    }

    binding_uid_2 = client.data_mart.bindings.add('My Azure ML Studio engine', AzureMachineLearningInstance(AZURE_ENGINE_CREDENTIALS))

    bindings_details = client.data_mart.bindings.get_details ()
    ```
  É possível ver sua ligação de serviços com o comando a seguir:

    ```python
    client.data_mart.bindings.list ()
    ```

    ![Ligação do Azure ML](images/ml-azure-bind.png)

### Incluir assinatura do Microsoft Azure ML Studio
{: #cml-azsub}

- Incluir assinatura

    ```python
    client.data_mart.subscriptions.add(
        AzureMachineLearningAsset(source_uid=source_uid,
                                  binding_uid=binding_uid,
                                  input_data_type=InputDataType.STRUCTURED,
                                  problem_type=ProblemType.MULTICLASS_CLASSIFICATION,
                                  label_column='<my_label_column_name>',
                                  prediction_column='Scored Labels'))
    ```

- Obter lista de assinaturas

    ```python
    inscrições = client.data_mart.subscriptions.get_details ()

    subscriptions_uids = client.data_mart.subscriptions.get_uids()
    print(subscriptions_uids)
    ```

### Ativar Log de Carga Útil
{: #cml-azenlog}

- Ativar a criação de log de carga útil na assinatura

    ```python
    subscription.payload_logging.enable ()
    ```

- Obter Detalhes da Criação de

    ```python
    subscription.payload_logging.get_details ()
    ```

### Log de Pontuação e Carga Útil
{: #cml-azscore}

- Pontuem seu modelo. Para ver um exemplo completo, consulte o [bloco de notas Trabalhando com o mecanismo Azure Machine Learning Studio](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}.

- Armazene a solicitação e a resposta na tabela de criação de log de carga útil:

    ```python
    records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time),
                    PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

    for i in range(1, 10):
    records_list.append(PayloadRecord(request=request_data, response=response_data, response_time=response_time))

    subscription.payload_logging.store(records=records_list)
    ```
    **Nota**: para linguagens diferentes de Python, também é possível executar a criação de log de carga útil diretamente, usando uma API de REST.

    ```json
    token_endpoint = "https://iam.cloud.ibm.com/identity/token"
    headers = {
            "Content-Type": "application/x-www-form-urlencoded",
            "Accept": "application/json"
    }

    data = {
            "grant_type":"urn:ibm:params:oauth:grant-type:apikey",
            "apikey":aios_credentials["apikey"]
    }

    req = requests.post(token_endpoint, data=data, headers=headers)
    token = req.json()['access_token']
    ```

    ```json
    pedidos de importação, uuid

    PAYLOAD_STORING_HREF_PATTERN = '{}/v1/data_marts/{}/scoring_payloads'
    endpoint = PAYLOAD_STORING_HREF_PATTERN.format(aios_credentials['url'], aios_credentials['data_mart_id'])

    payload = [{
      'binding_id': binding_uid,
      'deployment_id': subscription.get_details()['entity']['deployments'][0]['deployment_id'],
      'subscription_id': subscription.uid,
      'scoring_id': str(uuid.uuid4()),
      'response': response_data,
      'request': request_data
    }]

    headers = {"Authorization": "Bearer " + token}
    req_response = requests.post(endpoint, json=payload, headers = headers)
    print("Request OK: " + str(req_response.ok))
    ```


## Próximos passos
{: #ca-next}

Agora, o {{site.data.keyword.aios_short}} está pronto para que você [configure monitores](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
