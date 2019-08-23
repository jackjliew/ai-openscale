---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits, custom machine learning engine, custom

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

# Estruturas ML customizadas
{: #frmwrks-custom}

É possível usar sua estrutura de aprendizado de máquina customizado para executar a criação de log de carga útil e de feedback e para medir a precisão do desempenho, a detecção de propensão de tempo de execução, a explicabilidade e a função de remoção automática de propensão no {{site.data.keyword.aios_full}}. A estrutura de aprendizado de máquina customizado deve ser equivalente ao produto {{site.data.keywor.pm_full}}.

O {{site.data.keyword.aios_full}} suporta totalmente as estruturas de aprendizado de máquina customizado a seguir:
{: shortdesc}

Tabela 1. Detalhes do suporte da estrutura

| Estrutura | Tipo de problema | Tipo de dados |
|:---|:---:|:---:|
| Equivalente a {{site.data.keyword.pm_full}} | Classificação | Estruturadas |
{: caption="Detalhes do suporte da estrutura" caption-side="top"}

## Incluindo um mecanismo de aprendizado de máquina customizado no {{site.data.keyword.aios_short}}
{: #frmwrks-custom-add}

É possível configurar o {{site.data.keyword.aios_short}} para trabalhar com um provedor de aprendizado de máquina customizado usando um dos métodos a seguir:

- Se essa for a primeira vez que você está incluindo um provedor de aprendizado de máquina customizado no {{site.data.keyword.aios_short}}, será possível usar a interface de configuração. Para obter mais informações, consulte [Especificando uma instância de aprendizado de máquina customizado](/docs/services/ai-openscale?topic=ai-openscale-co-connect).
- Também é possível incluir o seu provedor de aprendizado de máquina usando o Python SDK. Deve-se usar este método caso você deseje ter mais de um provedor. Para obter mais informações sobre como executar isso programaticamente, consulte [Ligar seu mecanismo de aprendizado de máquina customizado](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-cusbind).


## Blocos de notas de amostra
{: #frmwrks-custom-smpl-ntbks}

- [Criação do mecanismo de Aprendizado de máquina customizado usando o cluster Kubernetes](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix){: external}
- [Criação de data mart, monitoramento de implementação de modelo e análise de dados](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}

## Explorar mais
{: #frmwrks-custom-mediumblogs}

[Monitorar o mecanismo de aprendizado de máquina customizado com o Watson OpenScale](https://developer.ibm.com/patterns/monitor-custom-machine-learning-engine-with-ai-openscale/){: external}

## Mecanismo de aprendizado de máquina customizado
{: #fmrk-workaround-customengine}

Um mecanismo de aprendizado de máquina customizado fornece os recursos de infraestrutura e de hosting para modelos de aprendizado de máquina e aplicativos da web. Os mecanismos de aprendizado de máquina customizados que são suportados pelo {{site.data.keyword.aios_short}} devem se adequar aos requisitos a seguir:

- Exponha dois tipos de terminais da API de REST:

   * terminal de descoberta (lista de implementações e detalhes de GET)
   * terminais de pontuação (pontuação on-line e em tempo real)

- Todos os terminais precisam ser compatíveis com a especificação swagger a ser suportada.

- A carga útil de entrada e a saída para a implementação ou da implementação devem ser compatíveis com o formato de arquivo JSON que está descrito na especificação.

Neste estágio, somente os formatos `BasicAuth` ou `none` são suportados
{: Note}

O exemplo a seguir mostra a especificação de terminais da API de REST:

![A especificação de terminais da API de REST é exibida por meio do documento do swagger](images/wosdeployments.png)


O exemplo a seguir mostra o formato para uma carga útil de entrada:

![O exemplo de carga útil de entrada é mostrado](images/wosinputdata.png)


## Quando um mecanismo de aprendizado de máquina customizado é a melhor opção para mim?
{: #fmrk-workaround-enging-choice}

Um mecanismo de aprendizado de máquina customizado é a melhor opção quando as situações a seguir são verdadeiras:

- Você não está usando nenhum produto pronto para utilização para atender a seus modelos de aprendizado de máquina. Você acabou de desenvolver seu próprio sistema para fazer isso. Não há e não haverá nenhum suporte direto no {{site.data.keyword.aios_short}} para isso.
- O mecanismo de entrega que você está usando por meio de um fornecedor de terceiros ainda não é suportado pelo {{site.data.keyword.aios_short}}. Nesse caso, considere o desenvolvimento de um mecanismo de aprendizado de máquina customizado como um wrapper para suas implementações originais ou nativas.

## Especificando uma Instância de Serviço ML Customizada
{: #co-connect}

Sua primeira etapa na ferramenta {{site.data.keyword.aios_short}} é especificar uma instância de serviço. Sua instância de serviço é onde você armazena seus modelos e implementações de IA.
{: shortdesc}

## Conectar sua instância de serviço customizado
{: #co-config}

O {{site.data.keyword.aios_short}} se conecta a modelos e implementações de IA em uma instância de serviço. É possível conectar um serviço customizado

1.  Na guia **Configurar**, na área de janela de navegação, clique em **Provedores de aprendizado de máquina**.

   ![A tela Selecionar seu provedor de serviços do mecanismo de aprendizado de máquina é mostrada com blocos para os mecanismos de aprendizado de máquina suportados](images/wos-machine-learning-providers-selection.png)

2. Clique no botão **Incluir provedor de aprendizado de máquina** e, em seguida, clique no bloco **Ambiente customizado**.

   ![a tela Configuração do provedor de aprendizado de máquina customizado é mostrada com campos para credenciais, nome e descrição da instância](images/ml-custom-provider.png)

3. Insira um nome e uma descrição para o seu provedor de aprendizado de máquina customizado e clique em **Avançar**. 

4. Escolha se conectar às suas implementações [solicitando uma lista](/docs/services/ai-openscale?topic=ai-openscale-co-connect#co-config-request-list) ou [inserindo terminais de pontuação individuais](/docs/services/ai-openscale?topic=ai-openscale-co-connect#co-config-scoring-endpoints).

   ![A tela Conectar-se a implementações é mostrada com opções para solicitar uma lista de implementações ou inserir um terminal de pontuação individual](images/ml-custom-connect-deployments.png)
    
5. Clique em **Avançar**.

### Solicitando a lista de implementações
{: #co-config-request-list}

1. Se você selecionou o bloco **Solicitar a lista de implementações**, insira as suas credenciais e o terminal de API e, em seguida, clique em **Salvar**.

   ![a tela Lista de implementações é mostrada com campos para inserir credenciais de serviço e um terminal de API](images/connect-custom-cred.png)

2. Depois de salvar sua configuração de aprendizado de máquina, retorne ao **Painel**, clique na guia **Insights** e, em seguida, clique no botão **Incluir no painel**.

3. Selecione uma implementação na lista e clique em **Configurar**.

Agora você está pronto para configurar os monitores.

### Fornecendo terminais de pontuação individuais
{: #co-config-scoring-endpoints}

1. Se você selecionou o bloco **Inserir terminais de pontuação individuais**, insira as suas credenciais para o terminal de API e, em seguida, clique em **Salvar**.

2. Depois de salvar sua configuração de aprendizado de máquina, retorne ao **Painel**, clique na guia **Insights** e, em seguida, clique no botão **Incluir no painel**.

3. Clique no botão **Incluir terminal**.

4. No menu suspenso, selecione o ambiente customizado, digite o nome da implementação e do terminal de API e, em seguida, clique em **Salvar**.

Agora você está pronto para configurar os monitores.

### Como ele funciona
{: #co-works}

A imagem a seguir mostra o suporte ao ambiente customizado:

![Como o gráfico de trabalhos customizados é exibido. Ele mostra caixas para o ambiente customizado com a API do cliente e a API do Watson OpenScale](images/custom-how-works.png)

Também é possível referenciar os links a seguir:

[API de criação de log de carga útil do {{site.data.keyword.aios_short}}](https://{DomainName}/apidocs/ai-openscale#publish-scoring-payload){: external}

[API de implementação customizada](https://aiopenscale-custom-deployement-spec.mybluemix.net/){: external}

[SDK de ligação do cliente Python](http://ai-openscale-python-client.mybluemix.net/#bindings){: external}

[Trabalhando com o mecanismo de aprendizado de máquina customizado](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}

[SDK do Python para o IBM Watson OpenScale](https://pypi.org/project/ibm-ai-openscale/){: external}

- **Critérios de entrada para modelo para suportar monitores**

  Seu modelo deve tomar como entrada um vetor de recurso, que é essencialmente uma coleção de campos nomeados e seus valores (os campos sendo monitorados para propensão sendo um destes campos):

  ```bash
  {
    "fields": [
        "name",
        "age",
        "position"
    ],
    "values": [
        [
            "john",
            33,
            "engineer"
        ],
        [
            "mike",
            23,
            "student"
        ]
    ]
  }
  ```

  Nesse exemplo, `“age”` poderia ser um campo que alguém está avaliando para justiça.

  Se a entrada for um tensor/matriz, que é transformado por meio do espaço do recurso de entrada (que é geralmente o caso em deep learning de texto ou imagens), esse modelo não poderá ser manipulado pela plataforma {{site.data.keyword.aios_short}} na liberação atual. Por extensão, os modelos de deep learning com entradas de texto ou imagem não podem ser manipulados para detecção e mitigação de propensão.

  Além disso, os dados de treinamento devem ser carregados para suportar a Explicabilidade.

  Para explicabilidade no texto, o texto integral deve ser um dos recursos. A Explicabilidade em imagens para um modelo Customizado não é suportada na liberação atual.
  {: note}

- **Critérios de saída para modelo para suportar monitores**

  Seu modelo deve gerar a saída do vetor de recurso de entrada juntamente com as probabilidades de predição de várias classes nesse modelo.

  ```bash
  {
    "fields": [
        "name",
        "age",
        "position",
        "prediction",
        "probability"
    ],
    "labels": [
        "personal",
        "camping"
    ],
    "values": [
        [
            "john",
            33,
            "engineer",
            "personal",
            [
                0.6744664422398081,
                0.3255335577601919
            ]
        ],
        [
            "mike",
            23,
            "student"
            "camping",
            [
                0.2794765664946941,
                0.7205234335053059
            ]
        ]
    ]
  }
  ```

  Nesse exemplo, `"personal”` e `“camping”` são as classes possíveis e as pontuações em cada saída de pontuação são designadas a ambas as classes. Se as probabilidades de predição estiverem ausentes, a detecção de propensão funcionará, mas a despropensão automática não.

  A saída de pontuação anterior deve estar acessível por meio de um terminal de pontuação em tempo real que o {{site.data.keyword.aios_short}} poderia chamar REST. Para o AzureML, o SageMaker e o {{site.data.keyword.pm_full}}, o {{site.data.keyword.aios_short}} conecta-se diretamente aos terminais de pontuação nativos (portanto, não é necessário se preocupar com a implementação da especificação de pontuação).

## Exemplos do mecanismo de aprendizado de máquina customizado
{: #fmrk-workaround-cstmmlsengex}

Use os exemplos a seguir para configurar seu próprio mecanismo de aprendizado de máquina customizado.
{: shortdesc}

### Python e Flask
{: #fmrk-workaround-pandflask}

O [exemplo de Mecanismo de ML customizado publicado no git](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix){: external} está usando Python e Flask para entregar o modelo scikit-learn.

O [arquivo LEIA-ME](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-bluemix){: external} descreve como o app pode ser implementado localmente para propósitos de teste, bem como para o aplicativo cf no IBM Cloud. A implementação de terminais da API de REST pode ser localizada no [arquivo app.py](https://github.com/pmservice/ai-openscale-tutorials/blob/master/applications/custom-ml-engine-bluemix/app.py){: external}.

### Node.js
{: #fmrk-workaround-nodejs}

Também é possível localizar um exemplo de mecanismo de aprendizado de máquina customizado gravado no [Node.js aqui](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-nodejs){: external}.

### Padrão de código End2end
{: #fmrk-workaround-e2ecode}

[Padrão de código](https://developer.ibm.com/patterns/monitor-custom-machine-learning-engine-with-ai-openscale){: external} mostrando o exemplo de end2end da implementação e integração do mecanismo customizado com o {{site.data.keyword.aios_short}}.

## Criação de log de carga útil com o mecanismo de aprendizado da máquina
{: #cml-cusconfig}

### Ligar seu mecanismo de aprendizado de máquina customizado
{: #cml-cusbind}

- Um mecanismo não {{site.data.keyword.pm_full}} é ligado como Customizado, o que significa que isso se trata apenas de metadados; não há integração direta com o serviço não {{site.data.keyword.pm_full}}. É possível ligar mais de um mecanismo de aprendizado de máquina ao {{site.data.keyword.aios_short}} usando o método `client.data_mart.bindings.add`.

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

    ![Ligação genérica do ML](images/ml-generic-bind.png)

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

Para obter mais informações, consulte [Criação de log da carga útil](/docs/services/ai-openscale?topic=ai-openscale-cml-connect).

### Log de Pontuação e Carga Útil
{: #cml-cusscore}

- Pontuem seu modelo. Para obter um exemplo integral, consulte o [bloco de notas IBM {{site.data.keyword.aios_full}} e mecanismo de aprendizado de máquina customizado](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}.

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


## Próximos passos
{: #fmrk-workaround-nxt-steps-over}

Agora, o {{site.data.keyword.aios_short}} está pronto para que você [configure monitores](/docs/services/ai-openscale?topic=ai-openscale-mo-config).

Implemente sua própria solução usando um destes [Exemplos de aprendizado de máquina customizado](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-cstmmlsengex).
