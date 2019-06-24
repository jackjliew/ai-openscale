---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

keywords: payload, non-Watson, machine learning, services, subscription

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Criação de log de carga útil para instâncias de serviço não do Watson Machine Learning
{: #cml-connect}

Se o seu modelo de IA é implementado em um mecanismo de aprendizado de máquina diferente do Watson Machine Learning (WML), deve-se ativar a criação de log de carga útil para o mecanismo de aprendizado de máquina externo com um cliente Python.
{: shortdesc}

Consulte informações mais completas na [documentação do cliente Python do {{site.data.keyword.aios_short}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://ai-openscale-python-client.mybluemix.net/){: new_window} e nos blocos de notas de amostra do cliente Python do {{site.data.keyword.aios_short}} Python que fazem parte dos [tutoriais do {{site.data.keyword.aios_short}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/README.md){: new_window}.

## Antes de Começar
{: #cml-prereq}

Você precisará ter os dados de treinamento de seu modelo disponíveis no Db2 ou no Cloud Object Storage para monitorar a propensão para o seu modelo. A explicabilidade e a precisão não são suportadas para as funções Python. Para
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

## Trabalhando com o mecanismo de aprendizado de máquina customizado
{: #cml-cusconfig}

### Ligar seu mecanismo de aprendizado de máquina customizado
{: #cml-cusbind}

- Um mecanismo não WML é ligado como Customizado, significando que se trata apenas de metadados; não há integração direta com o serviço não WML.

    ```python
    custom_engine_credentials = {
    "url": "***",
    "username": "***",
    "password": "***"
    }

    binding_uid = client.data_mart.bindings.add ('Meu mecanismo customizado', CustomMachineLearningInstance (custom_engine_credentials))

    bindings_details = client.data_mart.bindings.get_details ()
    ```
  É possível ver sua ligação de serviços com o comando a seguir:

    ```python
    client.data_mart.bindings.list ()
    ```

    ![Generic ML binding](images/ml-generic-bind.png)

### Incluir Assinatura Customizada
{: #cml-cussub}

- Incluir assinatura

    ```python
    client.data_mart.subscriptions.add (CustomMachineLearningAsset (source_uid = 'action', binding_uid = binding_uid, prediction_column= 'predictedActionLabel'))
    ```

- Obter lista de assinaturas

    ```python
    inscrições = client.data_mart.subscriptions.get_details ()

    subscriptions_uids = client.data_mart.subscriptions.get_uids()
    print(subscriptions_uids)
    ```

### Ativar Log de Carga Útil
{: #cml-cusenlog}

- Ativar a criação de log de carga útil na assinatura

    ```python
    subscription.payload_logging.enable ()
    ```

- Obter Detalhes da Criação de

    ```python
    subscription.payload_logging.get_details ()
    ```

### Log de Pontuação e Carga Útil
{: #cml-cusscore}

- Pontuem seu modelo. Para obter um exemplo integral, consulte o [Bloco de notas do mecanismo do IBM {{site.data.keyword.aios_full}} & Custom ML![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: new_window}.

<!---
    ```python
    import urllib.request
    import json

    data = {
            {
             "input1":
             [
                {
                  <YOUR-JSON-DATA>
                }
             ],
            },
    }

    body = str.encode(json.dumps(data))

    url = '<YOUR-SERVICE-URL>'
    api_key = '<API-KEY-FOR-YOUR-WEB-SERVICE>'
    headers = {'Content-Type':'application/json', 'Authorization':('Bearer '+ api_key)}

    req = urllib.request.Request(url, body, headers)
    response = urllib.request.urlopen(req)

    result = response.read()
    result = json.loads(result.decode())['Results']['output1'][0]
    print(json.dumps(result, indent=2))
    ```
--->

- Armazene a solicitação e a resposta na tabela de criação de log de carga útil

    ```python
    records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time), PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

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

## Trabalhando com o mecanismo de aprendizado de máquina Microsoft Azure
{: #cml-azconfig}

### Ligar o mecanismo MS Azure ML
{: #cml-azbind}

- Um mecanismo não WML é ligado como Customizado, significando que se trata apenas de metadados; não há integração direta com o serviço não WML.

    ```python
    AZURE_ENGINE_CREDENTIALS = {
    "client_id": "***",
    "client_secret": "***",
    "subscription_id": "***",
    "tenant": "***"
    }

    binding_uid = client.data_mart.bindings.add('My Azure ML Studio engine', AzureMachineLearningInstance(AZURE_ENGINE_CREDENTIALS))

    bindings_details = client.data_mart.bindings.get_details ()
    ```
  É possível ver sua ligação de serviços com o comando a seguir:

    ```python
    client.data_mart.bindings.list ()
    ```

    ![Azure ML binding](images/ml-azure-bind.png)

### Incluir Assinatura ML do MS Azure
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

- Pontuem seu modelo. Para obter um exemplo integral, consulte o [bloco de notas Trabalhando com o mecanismo Azure Machine Learning Studio ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: new_window}.

<!---
    ```python
    import urllib.request
    import json

    data = {
            {
             "input1":
             [
                {
                  <YOUR-JSON-DATA>
                }
             ],
            },
    }

    body = str.encode(json.dumps(data))

    url = '<YOUR-SERVICE-URL>'
    api_key = '<API-KEY-FOR-YOUR-WEB-SERVICE>'
    headers = {'Content-Type':'application/json', 'Authorization':('Bearer '+ api_key)}

    req = urllib.request.Request(url, body, headers)
    response = urllib.request.urlopen(req)

    result = response.read()
    result = json.loads(result.decode())['Results']['output1'][0]
    print(json.dumps(result, indent=2))
    ```
--->

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

## Trabalhando com o mecanismo de aprendizado de máquina Amazon SageMaker
{: #cml-smconfig}

### Ligar o mecanismo ML AWS SageMaker
{: #cml-smbind}

- Um mecanismo não WML é ligado como Customizado, significando que se trata apenas de metadados; não há integração direta com o serviço não WML.

    ```python
    SAGEMAKER_ENGINE_CREDENTIALS = {
    "access_key_id": "***",
    "secret_access_key": "***",
    "region": "***"
    }

    binding_uid = client.data_mart.bindings.add( 'Meu mecanismo SageMaker ', SageMakerMachineLearningInstance (SAGEMAKER_ENGINE_CREDENTIALS))

    bindings_details = client.data_mart.bindings.get_details ()
    ```
  É possível ver sua ligação de serviços com o comando a seguir:

    ```python
    client.data_mart.bindings.list ()
    ```

    ![SageMaker ML binding](images/ml-sagemaker-bind.png)

### Incluir Assinatura ML do Amazon SageMaker
{: #cml-smsub}

- Incluir assinatura

    ```python
    client.data_mart.subscriptions.add(
        SageMakerMachineLearningAsset(source_uid=source_uid,
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
{: #cml-smenlog}

- Ativar a criação de log de carga útil na assinatura

    ```python
    subscription.payload_logging.enable ()
    ```

- Obter Detalhes da Criação de

    ```python
    subscription.payload_logging.get_details ()
    ```

### Log de Pontuação e Carga Útil
{: #cml-smscore}

- Pontuem seu modelo. Para obter um exemplo integral, consulte o [bloco de notas Trabalhando com o mecanismo de aprendizado de máquina SageMaker ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20SageMaker%20ML%20Engine.ipynb){: new_window}.

<!---
    ```python
    import urllib.request
    import json

    data = {
            {
             "input1":
             [
                {
                  <YOUR-JSON-DATA>
                }
             ],
            },
    }

    body = str.encode(json.dumps(data))

    url = '<YOUR-SERVICE-URL>'
    api_key = '<API-KEY-FOR-YOUR-WEB-SERVICE>'
    headers = {'Content-Type':'application/json', 'Authorization':('Bearer '+ api_key)}

    req = urllib.request.Request(url, body, headers)
    response = urllib.request.urlopen(req)

    result = response.read()
    result = json.loads(result.decode())['Results']['output1'][0]
    print(json.dumps(result, indent=2))
    ```
--->

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
{: #cml-next}

- Para continuar com o cliente {{site.data.keyword.aios_short}}, consulte [Especificando um banco de dados](/docs/services/ai-openscale?topic=ai-openscale-connect-db).

- Para continuar com a biblioteca de comandos do Python, consulte a [documentação do cliente Python ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://ai-openscale-python-client.mybluemix.net/){: new_window}.
