---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits, AWS, Sagemaker, Amazon

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

# Estruturas Amazon SageMaker
{: #frmwrks-aws-sage}

É possível usar o Amazon SageMaker para executar a criação de log de carga útil e de feedback e para medir a precisão do desempenho, a detecção de propensão de tempo de execução, a explicabilidade e a função de remoção automática de propensão no {{site.data.keyword.aios_full}}.

O {{site.data.keyword.aios_full}} suporta totalmente as estruturas do Amazon SageMaker a seguir:
{: shortdesc}

Tabela 1. Detalhes do suporte da estrutura

| Estrutura | Tipo de problema | Tipo de dados |
|:---|:---:|:---:|
| Nativo | Classificação | Estruturadas |
| Nativo | Regressão<sup>1</sup> | Estruturadas |
{: caption="Detalhes do suporte da estrutura" caption-side="top"}

<sup>1</sup>O suporte para modelos de regressão não inclui a magnitude de desvio.

## Incluindo o Amazon SageMaker no {{site.data.keyword.aios_short}}
{: #frmwrks-aws-sage-add}

É possível configurar o {{site.data.keyword.aios_short}} para trabalhar com o Amazon SageMaker usando um dos métodos a seguir:

- Se essa for a primeira vez que você está incluindo um provedor de aprendizado de máquina no {{site.data.keyword.aios_short}}, será possível usar a interface de configuração. Para obter mais informações, consulte [Especificando uma instância do Amazon SageMaker](/docs/services/ai-openscale?topic=ai-openscale-csm-connect).
- Também é possível incluir o seu provedor de aprendizado de máquina usando o Python SDK. Deve-se usar este método caso você deseje ter mais de um provedor. Para obter mais informações sobre como executar isso programaticamente, consulte [Ligue o seu mecanismo de aprendizado de máquina do Amazon SageMaker](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind).


## Blocos de notas de amostra
{: #frmwrks-aws-sage-smpl-ntbks}

As anotações a seguir mostram como trabalhar com o Amazon SageMaker:

- [Criação e implementação do modelo de previsão de risco de crédito](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Credit%20%20model%20with%20SageMaker%20linear-learner%20.ipynb){: external}
- [Criação de data mart, monitoramento de implementação de modelo e análise de dados](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20SageMaker%20ML%20Engine.ipynb){: external}

## Especificando uma instância de serviço do Amazon SageMaker ML
{: #csm-connect}

Sua primeira etapa na ferramenta {{site.data.keyword.aios_short}} é especificar uma instância de serviço do Amazon SageMaker. Sua instância de serviço do Amazon SageMaker é onde você armazena seus modelos e implementações de IA.
{: shortdesc}

Também é possível incluir o seu provedor de aprendizado de máquina usando o Python SDK. Para obter mais informações sobre como executar isso programaticamente, consulte [Ligue o seu mecanismo de aprendizado de máquina do Amazon SageMaker](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind).

### Conecte sua instância de serviço Amazon SageMaker
{: #csm-config}

O {{site.data.keyword.aios_short}} se conecta a modelos e implementações de IA em uma instância de serviço do Amazon SageMaker.

1.  Na guia **Configurar**, na área de janela de navegação, clique em **Provedores de aprendizado de máquina**.

    ![A tela Selecionar seu provedor de serviços do mecanismo de aprendizado de máquina é mostrada com blocos para os mecanismos de aprendizado de máquina suportados](images/wos-machine-learning-providers-selection.png)

1.  Clique no botão **Incluir provedor de aprendizado de máquina** e, em seguida, clique no bloco **Amazon SageMaker**.

    ![Inserir as credenciais de serviço do Amazon SageMaker](images/connect-sage-cred.png)

1.  Insira e salve suas credenciais:

    - ID da chave de acesso: seu ID da chave de acesso da AWS, `aws_access_key_id`, que verifica quem você é, além de autenticar e autorizar chamadas feitas para a AWS.
    - Chave de acesso secreta: sua chave de acesso secreta da AWS, `aws_secret_access_key`, que é necessária para verificar quem você, além de para autenticar e autorizar chamadas feitas para a AWS.
    - Região: insira a região onde seu ID da chave de acesso foi criado. As chaves são armazenadas e usadas na região em que foram criadas e não podem ser transferidas para outra região. 

1.  O {{site.data.keyword.aios_short}} lista seus modelos implementados. Selecione aqueles que você deseja monitorar.

## Criação de log de carga útil com o mecanismo de aprendizado de máquina Amazon SageMaker
{: #cml-smconfig}

### Ligar seu mecanismo de aprendizado de máquina do Amazon SageMaker
{: #cml-smbind}

- Um mecanismo não {{site.data.keyword.pm_full}} é ligado como Customizado, o que significa que isso se trata apenas de metadados; não há integração direta com o serviço não {{site.data.keyword.pm_full}}.

    ```python
    SAGEMAKER_ENGINE_CREDENTIALS = {
    "access_key_id": "***",
    "secret_access_key": "***",
    "region": "***"
    }

    binding_uid_3 = client.data_mart.bindings.add('My SageMaker engine', SageMakerMachineLearningInstance(SAGEMAKER_ENGINE_CREDENTIALS))

    bindings_details = client.data_mart.bindings.get_details ()
    ```
  É possível ver sua ligação de serviços com o comando a seguir:

    ```python
    client.data_mart.bindings.list ()
    ```

    ![Ligação do SageMaker ML](images/ml-sagemaker-bind.png)

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

- Pontuem seu modelo. Para ver um exemplo completo, consulte o [bloco de notas Trabalhando com o mecanismo de aprendizado de máquina SageMaker](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20SageMaker%20ML%20Engine.ipynb){: external}.


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
{: #csm-next}

- Agora, o {{site.data.keyword.aios_short}} está pronto para que você [configure monitores](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
- [Monitorar aprendizado de máquina do SageMaker com o Watson OpenScale](https://developer.ibm.com/patterns/monitor-amazon-sagemaker-machine-learning-models-with-ai-openscale//){: external}
