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

# Criação de log de carga útil com o mecanismo do Microsoft Azure Machine Learning Studio
{: #cml-azconfig}

## Ligar seu mecanismo de aprendizado de máquina do Microsoft Azure
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

## Incluir assinatura do Microsoft Azure ML Studio
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

## Ativar Log de Carga Útil
{: #cml-azenlog}

- Ativar a criação de log de carga útil na assinatura

    ```python
    subscription.payload_logging.enable ()
    ```

- Obter Detalhes da Criação de

    ```python
    subscription.payload_logging.get_details ()
    ```

## Log de Pontuação e Carga Útil
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

