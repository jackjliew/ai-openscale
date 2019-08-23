---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits, azure

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

# Estruturas do Microsoft Azure ML Service
{: #frmwrks-azure-service}

É possível usar o Microsoft Azure ML Service para executar a criação de log de carga útil e de feedback e para medir a precisão do desempenho, a detecção de propensão de tempo de execução, a explicabilidade e a função de remoção automática de propensão no {{site.data.keyword.aios_full}}.

O {{site.data.keyword.aios_full}} suporta totalmente as estruturas do Microsoft Azure Machine Learning Service a seguir:
{: shortdesc}

Tabela 1. Detalhes do suporte da estrutura

| Estrutura | Tipo de problema | Tipo de dados |
|:---|:---:|:---:|
| Nativo | Classificação | Estruturadas |
| scikit-learn | Classificação | Estruturadas |
| scikit-learn | Procedimento de | Estruturadas |
{: caption="Detalhes do suporte da estrutura" caption-side="top"}

## Incluindo o Microsoft Azure ML Service no {{site.data.keyword.aios_short}}
{: #frmwrks-azureservice-addsrvc}

É possível configurar o {{site.data.keyword.aios_short}} para trabalhar com o Microsoft Azure ML Service usando um dos métodos a seguir:

- Se essa for a primeira vez que você está incluindo um provedor de aprendizado de máquina no {{site.data.keyword.aios_short}}, será possível usar a interface de configuração. Para obter mais informações, consulte [Especificando uma instância do Microsoft Azure ML Service](/docs/services/ai-openscale?topic=ai-openscale-connect-azureservice).
- Também é possível incluir o seu provedor de aprendizado de máquina usando o Python SDK. Deve-se usar este método caso você deseje ter mais de um provedor. Para obter mais informações sobre como executar isso programaticamente, consulte [Ligue o seu mecanismo de aprendizado de máquina do Microsoft Azure](/docs/services/ai-openscale?topic=ai-openscale-cml-azsrvconfig#cml-azsrvbind).


O {{site.data.keyword.aios_short}} chama vários terminais de REST que são necessários para interagir com o Azure ML Service. Para fazer isso, deve-se ligar o Azure Machine Learning Service {{site.data.keyword.aios_short}}.

1. Criar um Azure Active Directory Service Principal.
2. Especifique os detalhes da credencial ao incluir a ligação de serviços do Azure ML Service por meio da IU ou do {{site.data.keyword.aios_short}} Python SDK.

## Requisitos para arquivos de solicitação e de resposta JSON
{: #frmwrks-azureservice-JSON}

Para o {{site.data.keyword.aios_short}} funcionar com o Azure ML Service, as implementações de serviço da web criadas devem atender a determinados requisitos. As implementações de serviço da web que você criar devem aceitar solicitações JSON e retornar respostas JSON, de acordo com os requisitos descritos abaixo.

### Formato de solicitação JSON do serviço da web necessário
{: #frmwrks-azureservice-JSON-sample-request}

- O corpo da solicitação da API de REST deve ser um documento JSON que contenha uma matriz JSON de objetos JSON
- A matriz JSON deve ser denominada `"input"`.
- Cada objeto JSON pode incluir apenas pares de chave-valor simples, em que os valores podem ser apenas uma sequência, um número, `true`, `false` ou `null`
- Os valores não podem ser um objeto ou matriz JSON
- Cada objeto JSON na matriz deve ter as mesmas chaves (e, portanto, o número de chaves) especificadas, independentemente de haver ou não um valor não `null` disponível


O arquivo JSON de amostra a seguir atende aos requisitos anteriores e pode ser usado como um modelo para criar seus próprios arquivos de solicitação JSON:


```JSON
{
  "input": [
    {
      "field1": "value1",
      "field2": 31,
      "field3": true,
      "field4": 2.3
    },
    {
      "field1": "value2",
      "field2": 15,
      "field3": false,
      "field4": 0.1
    },
    {
      "field1": null,
      "field2": 5,
      "field3": true,
      "field4": 6.1
    }
  ]
}
```


### Formato de resposta JSON de serviço da web necessário
{: #frmwrks-azureservice-JSON-sample-response}

Anote os itens a seguir quando você criar um arquivo de resposta JSON:

- O corpo de resposta da API de REST deve ser um documento JSON que contenha uma matriz JSON de objetos JSON
- A matriz JSON deve ser denominada `"output"`.
- Cada objeto JSON pode incluir apenas pares de chave-valor, em que os valores podem ser apenas uma sequência, um número, `true`, `false`, `null` ou uma matriz que não contenha nenhum outro objeto ou matriz JSON
- Os valores não podem ser um objeto JSON
- Cada objeto JSON na matriz deve ter as mesmas chaves (e número de chaves) especificadas, independentemente de haver ou não um valor não `null` disponível
- Para modelos de classificação: o serviço da web deve retornar uma matriz de probabilidades para cada classe e a ordenação das probabilidades deve ser consistente para cada objeto JSON na matriz
  - Exemplo: suponha que você tenha um modelo de classificação binário que prevê o risco de crédito, em que as classes são `Risk` ou `No Risk`
  - Para cada resultado retornado de volta na matriz "output", os objetos devem conter um par de chave-valor que inclua as probabilidades em ordem fixa, no formato:
  
  <code>"output": [{"Scored Probabilities": [<i>"Risk" probability,"No Risk" probability</i>]}, {"Scored Probabilities": [<i>"Risk" probability,"No Risk" probability</i>]}]</code>

Para ser consistente com as ferramentas visuais do Azure ML usadas no Azure ML Studio e no Service, é recomendado, embora não seja necessário, usar os seguintes nomes de chave:

- o nome da chave `"Scored Labels"` para a chave de saída que denota o valor previsto do modelo
- o nome da chave `"Score Probabilities"` para a chave de saída que denota uma matriz de probabilidades para cada classe

O arquivo JSON de amostra a seguir atende aos requisitos anteriores e pode ser usado como um modelo para a criação de seus próprios arquivos de resposta JSON:


```JSON
{
  "output": [
    {
      "Scored Labels": "No Risk",
      "Scored Probabilities": [
        0.8922524675865824,
        0.10774753241341757
      ]
    },
    {
      "Scored Labels": "No Risk",
      "Scored Probabilities": [
        0.8335192848546905,
        0.1664807151453095
      ]
    }
  ]
}
```

## Blocos de notas de amostra
{: #frmwrks-azureservice-smpl-ntbks}

As anotações a seguir mostram como trabalhar com o Microsoft Azure ML Service:

- [Exemplos de pontuação de modelo do MS Azure Service](https://dataplatform.cloud.ibm.com/analytics/notebooks/v2/0d4ebd8d-87cb-4c38-8ba8-37f5623df131/view?access_token=fcb2c411aed913bf94f86f434184db67aef1a6b304824b86b4ad63686e4890be){: external}


## Especificando uma instância do Microsoft Azure ML Service
{: #connect-azureservice}

Sua primeira etapa na ferramenta {{site.data.keyword.aios_short}} é especificar uma instância do Microsoft Azure ML Service. A instância do Azure ML Service é o local em que você armazena seus modelos e implementações de IA.
{: shortdesc}

Também é possível incluir o seu provedor de aprendizado de máquina usando o Python SDK. Para obter mais informações sobre como realizar essa execução programaticamente, consulte [Vincule seu mecanismo de aprendizado de máquina do serviço Microsoft Azure](/docs/services/ai-openscale?topic=ai-openscale-cml-azsrvconfig#cml-azsrvbind).

## Conecte a sua instância do Azure ML Service
{: #ca-connect}

O {{site.data.keyword.aios_short}} se conecta aos modelos e implementações de IA em uma instância do Azure ML Service.

1.  Na guia **Configurar**, na área de janela de navegação, clique em **Provedores de aprendizado de máquina**.
1.  Clique no botão **Incluir provedor de aprendizado de máquina** e, em seguida, clique no bloco **Microsoft Azure ML Service**.
1.  Insira e salve suas credenciais:

    - Identificador de cliente: o valor da sequência real de seu identificador de cliente, que verifica quem você é e autentica e autoriza as chamadas que você faz para o Azure Service.
    - Segredo do cliente: o valor da sequência real do segredo, que verifica quem você é e autentica e autoriza as chamadas que você faz para o Azure Service.
    - Locatário: seu ID do locatário corresponde à sua organização e é uma instância dedicada do Azure AD. Para localizar o ID do locatário, passe o mouse sobre o nome de sua conta para obter o ID do diretório/locatário ou selecione Azure Active Directory > Propriedades > ID do diretório no portal do Azure.
    - ID da assinatura: credenciais de assinatura que identificam exclusivamente a assinatura do Microsoft Azure. O ID da assinatura faz parte do URI de cada chamada de serviço.

    Consulte [Como: Usar o portal para criar um aplicativo e uma entidade de serviço do Microsoft Azure Active Directory que possa acessar recursos](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: external} para obter instruções sobre como obter suas credenciais do Microsoft Azure.
    {: note}

1.  O {{site.data.keyword.aios_short}} lista seus modelos implementados. Selecione aqueles que você deseja monitorar e clique em **Configurar**.

Você selecionou com êxito as implementações.

## Criação de log de carga útil com o mecanismo do Microsoft Azure ML Service
{: #cml-azsrvconfig}

### Ligar o mecanismo do Microsoft Azure ML Service
{: #cml-azsrvbind}

Um mecanismo não {{site.data.keyword.pm_full}} é ligado como Customizado, o que significa que isso se trata apenas de metadados; não há integração direta com o serviço não {{site.data.keyword.pm_full}}.
   
```
AZURE_ENGINE_CREDENTIALS = {
"client_id": "***",
    "client_secret": "***",
    "subscription_id": "***",
    "tenant": "***"
}

binding_uid = client.data_mart.bindings.add('My Azure ML Service engine', AzureMachineLearningServiceInstance(AZURE_ENGINE_CREDENTIALS))


bindings_details = client.data_mart.bindings.get_details ()
```
{: codeblock}

É possível ver sua ligação de serviços com o comando a seguir:

```
client.data_mart.bindings.list ()
```
{: codeblock}

A saída de amostra:

```
uid	                                   name	                      service_type	                   created
410e730f-8462-45fe-8b41-a029d6d6043a	My Azure ML Service engine azure_machine_learning_service2019-06-10T22:10:29.398Z
```
{: codeblock}
    
    
### Incluir assinatura do Microsoft Azure ML Service
{: #cml-azsrvsub}

Incluir assinatura

```
client.data_mart.subscriptions.add(
        AzureMachineLearningAsset(source_uid=source_uid,
                                  binding_uid=binding_uid,
                                  input_data_type=InputDataType.STRUCTURED,
                                  problem_type=ProblemType.MULTICLASS_CLASSIFICATION,
                                  label_column='<my_label_column_name>',
                                  prediction_column='Scored Labels'))
```
{: codeblock}

Obter lista de assinaturas

```
inscrições = client.data_mart.subscriptions.get_details ()

subscriptions_uids = client.data_mart.subscriptions.get_uids()
    print(subscriptions_uids)
```
{: codeblock}

### Ativar Log de Carga Útil
{: #cml-azsrvenlog}

Ativar a criação de log de carga útil na assinatura

```
subscription.payload_logging.enable ()
```
{: codeblock}

Obter Detalhes da Criação de

```
subscription.payload_logging.get_details ()
```
{: codeblock}

### Log de Pontuação e Carga Útil
{: #cml-azsrvscore}

Pontuem seu modelo. Para obter um exemplo completo, consulte o [bloco de notas Trabalhando com o mecanismo do Azure Machine Learning Service](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Azure%20ML%20Studio%20Engine.ipynb){: external}.

Armazene a solicitação e a resposta na tabela de criação de log de carga útil:

```
records_list = [PayloadRecord(request=request_data, response=response_data, response_time=response_time),
                    PayloadRecord(request=request_data, response=response_data, response_time=response_time)]

for i in range(1, 10):
    records_list.append(PayloadRecord(request=request_data, response=response_data, response_time=response_time))

subscription.payload_logging.store(records=records_list)
```
{: codeblock}
{: python}
   
Para linguagens diferentes da Python, também é possível executar a criação de log de carga útil diretamente usando uma API de REST.
   
```
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
{: codeblock}
{: json}


```
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
{: codeblock}



## Próximos passos
{: #ca-next}

- Agora, o {{site.data.keyword.aios_short}} está pronto para [configurar os monitores](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
- [Como o serviço Azure Machine Learning difere do Studio?](https://docs.microsoft.com/en-us/azure/machine-learning/service/overview-what-is-azure-ml#how-does-azure-machine-learning-service-differ-from-studio){: external}

