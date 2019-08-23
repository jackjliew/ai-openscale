---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: machine learning, services, ml, custom 

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

# Especificando uma Instância de Serviço ML Customizada
{: #co-connect}

Sua primeira etapa na ferramenta {{site.data.keyword.aios_short}} é especificar uma instância de serviço. Sua instância de serviço é onde você armazena seus modelos e implementações de IA.
{: shortdesc}

## Conectar sua instância de serviço customizado
{: #co-config}

O {{site.data.keyword.aios_short}} se conecta a modelos e implementações de IA em uma instância de serviço. É possível conectar um serviço customizado

1. Na guia **Configurar**, clique em **Provedor de aprendizado de máquina**. Dependendo de seu ambiente, talvez você não veja todos os provedores a seguir:

   ![A tela Selecionar seu provedor de serviços do mecanismo de aprendizado de máquina é mostrada com blocos para os mecanismos de aprendizado de máquina suportados](images/wos-machine-learning-providers-selection.png)

2. Selecione o bloco **Ambiente customizado**.

   ![a tela Configuração do provedor de aprendizado de máquina customizado é mostrada com campos para credenciais, nome e descrição da instância](images/ml-custom-provider.png)

1.  Insira e salve suas credenciais:

    - Nome de usuário: seu nome de usuário do provedor de aprendizado de máquina customizado.
    - Senha: sua senha do provedor de aprendizado de máquina customizado.
    - Nome da instância do provedor de serviços: o nome específico designado a esse provedor de serviços.
    - Descrição (opcional): sua descrição em linguagem simples dessa instância do provedor de serviços. Se tiver ambientes de produção e teste, inclua essas informações nestes locais.

4. Escolha se conectar às suas implementações [solicitando uma lista](/docs/services/ai-openscale?topic=ai-openscale-co-connect#co-config-request-list) ou [inserindo terminais de pontuação individuais](/docs/services/ai-openscale?topic=ai-openscale-co-connect#co-config-scoring-endpoints).

   ![Selecionar customizado](images/ml-custom-connect-deployments.png)
    
5. Clique em **Avançar**.

### Solicitando a lista de implementações
{: #co-config-request-list}

1. Se você selecionou o bloco **Solicitar a lista de implementações**, insira as suas credenciais e o terminal de API e, em seguida, clique em **Salvar**.

   ![Inserir credenciais de serviço](images/connect-custom-cred.png)

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

![Como a customização funciona](images/custom-how-works.png)

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

### Próximos passos
{: #co-next}

Agora, o {{site.data.keyword.aios_short}} está pronto para que você [configure monitores](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
