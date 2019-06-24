---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

keywords: machine learning, services, ml, custom 

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

# Especificando uma Instância de Serviço ML Customizada
{: #co-connect}

Sua primeira etapa na ferramenta {{site.data.keyword.aios_short}} é especificar uma instância de serviço. Sua instância de serviço é onde você armazena seus modelos e implementações de IA.
{: shortdesc}

## Conectar sua instância de serviço customizado
{: #co-config}

O {{site.data.keyword.aios_short}} se conecta a modelos e implementações de IA em uma instância de serviço.

1.  Na página inicial da ferramenta {{site.data.keyword.aios_short}}, clique em **Iniciar**.

    ![Home page](images/gs-config-start.png)

2.  Selecione o ladrilho **Customizado** e clique em **Avançar**.

    ![Select custom](images/connect-custom.png)

3.  Conecte-se às implementações selecionando uma das opções:

    ![Select custom](images/connect-custom-deploy.png)

4.  Se você selecionou o ladrilho "Inserir terminais de pontuação individual", insira suas credenciais:

    ![Enter service credentials](images/connect-custom-cred.png)

5.  Clique em **Avançar**.

    - Se você selecionou o ladrilho "Inserir terminais de pontuação individual", deve-se fornecer um nome de implementação e um terminal:

      ![Enter service credentials](images/connect-custom-endpoint.png)

      Clique em **Avançar**.

    - Se você selecionou a tela "Solicitar uma lista de implementações", deve-se fornecer um nome do host ou endereço IP e o número da porta:

      ![Enter service credentials](images/connect-custom-apiendpoint.png)

      Clique em **Avançar**.

      Em seguida, selecione entre a lista de implementações:

      ![Enter service credentials](images/connect-custom-apiendpoint2.png)

6.  Revise suas implementações selecionadas.

    ![Enter service credentials](images/connect-custom-deploy2.png)

7.  Clique em **Avançar**.

### Como ele funciona
{: #co-works}

Esta imagem mostra o suporte ao ambiente Customizado:

![How Custom works](images/custom-how-works.png)

Também é possível referenciar os links a seguir:

[API de criação de log de carga útil do AIOS ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/ai-openscale#publish-scoring-payload){: new_window}

[API de implementação customizada ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://aiopenscale-custom-deployement-spec.mybluemix.net/){: new_window}

[SDK de ligação do cliente Python ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://ai-openscale-python-client.mybluemix.net/#bindings){: new_window}

[Trabalhando com o mecanismo de aprendizado de máquina customizado ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: new_window}

[Python SDK for IBM Watson OpenScale ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://pypi.org/project/ibm-ai-openscale/){: new_window}

- **Critérios de entrada para que os modelos suportem monitores**

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

- **Critérios de saída para que os modelos suportem monitores**

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

  A saída de pontuação acima deve estar acessível por meio de um terminal de pontuação em tempo real que o {{site.data.keyword.aios_short}} pode chamar sobre REST. Para o AzureML, o SageMaker e o WML, o {{site.data.keyword.aios_short}} conecta-se diretamente aos terminais de pontuação nativos (portanto, não é necessário se preocupar com a implementação da especificação de pontuação)

### Próximos passos
{: #co-next}

O {{site.data.keyword.aios_short}} agora está pronto para você [especificar um banco de dados](/docs/services/ai-openscale?topic=ai-openscale-connect-db).
