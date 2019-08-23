---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits

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
{:external: target="_blank" .external}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:faq: data-hd-content-type='faq'}

# Limitações e problemas conhecidos do {{site.data.keyword.aios_short}} for {{site.data.keyword.cloud_notm}}
{: #rn-12ki}

A lista a seguir contém as limitações e os problemas conhecidos que são comuns no {{site.data.keyword.aios_full}} for {{site.data.keyword.Bluemix}} e no {{site.data.keyword.wos4d_full}}, além daqueles específicos do {{site.data.keyword.aios_full}} for {{site.data.keyword.Bluemix}}.
{: shortdesc}

<p>&nbsp;</p>

## Problemas Comuns
{: #wos-common-issues}

As limitações e os problemas conhecidos a seguir são comuns no {{site.data.keyword.aios_full}} on {{site.data.keyword.Bluemix}} e no {{site.data.keyword.wos4d_full}}.

<p>&nbsp;</p>


### Limitações comuns
{: #wos-limitations}

- Para o {{site.data.keyword.pm_full}}, a entrada de pontuação para modelos de classificação de imagem enviados para a criação de log de carga útil não pode exceder ai-open-scale-ibm-aios-scheduling  | 1 | Planejando o serviceMB. Para evitar problemas de tempo limite, as imagens não devem exceder 125 x 125 pixels e devem ser enviadas sequencialmente de modo que a explicação para a segunda imagem seja solicitada quando a primeira estiver concluída.


- A explicabilidade para modelos de texto não estruturados não é suportada para linguagens de script contínuas, como japonês, chinês e coreano, que não usam caracteres de espaço em branco ou de pontuação para separar as palavras.



<p>&nbsp;</p>


### Erros de configuração de desvio impedem a configuração do monitor de desvio
{: #wos-common-issues-mismatchdatatype}

A flexibilidade da tela de configuração do modelo também poderá levar a problemas posteriormente quando você desejar configurar monitores, como o monitor de detecção de desvio. Como é possível escolher os tipos de dados, deve-se assegurar que as suas opções reflitam o que é original para o modelo. O erro a seguir poderá ocorrer se o tipo de coluna de predição não estiver selecionado corretamente:

```
"error": AIQDS2003E",
"message": "The model predictions '[0. 1.]' are different from class names in training data '['No' 'Yes']' for the subscription <<number>> in datamart <<datamart ID>> and service binding <<binding ID>>.
```

Os casos a seguir são a causa mais provável:

- A etiqueta `class` é do tipo sequência e a **predição** `modeling_role` é designada à coluna **predição** como um tipo duplo porque é assim que o esquema de dados de saída é definido.
- Você seleciona a coluna **predição** do tipo duplo na IU, que não é restrita.


### Formatos da carga útil
{: #wos-common-issues-payloadformat}

Para um processamento adequado de análise da carga útil, o {{site.data.keyword.aios_short}} não suporta nomes de coluna com aspas duplas (") na carga útil. Isso afeta a carga útil de pontuação e os dados de feedback nos formatos de CSV e de JSON.

<p>&nbsp;</p>



### Microsoft Azure ML Studio
{: #wos-common-issues-msazure}

- Dos dois tipos de serviços da web do Azure Machine Learning, somente o tipo `Novo` é suportado pelo {{site.data.keyword.aios_short}}. O tipo `Classic` não é suportado.

- __*O nome de entrada padrão deve ser usado*__: no serviço da web Azure, o nome de entrada padrão é `"input1"`. Atualmente, esse campo é obrigatório para o {{site.data.keyword.aios_short}} e, se ele estiver ausente, o {{site.data.keyword.aios_short}} não funcionará.

  Se o seu serviço da web Azure não usar o nome padrão, mude o nome do campo de entrada para `"input1"`, em seguida, o código funcionará.

- Se as chamadas para que o Microsoft Azure ML Studio liste os modelos de aprendizado de máquina fizerem com que a resposta atinja o tempo limite, por exemplo, quando houver muitos serviços da web, você deverá aumentar os valores de tempo limite. Por exemplo, se você estiver usando o balanceador de carga HAProxy, poderá ser necessário contornar esse problema emitindo os comandos a seguir:

   - Efetue login no nó do balanceador de carga e atualize `/etc/haproxy/haproxy.cfg` para configurar o tempo limite do cliente e do servidor de `1m` para `5m`:

       ```bash
       timeout client           5m
          timeout server           5m
      ```

   - Execute `systemctl restart haproxy` para reiniciar o balanceador de carga HAProxy.

Se você estiver usando um balanceador de carga diferente do HAProxy, poderá ser necessário ajustar os valores de tempo limite de uma maneira semelhante.
      {: note}

- Dos dois tipos de serviços da web do Azure Machine Learning, somente o tipo `Novo` é suportado pelo {{site.data.keyword.aios_short}}. O tipo `Classic` não é suportado.

- No serviço da web Azure, o nome de entrada padrão é `"input1"`. Atualmente, esse campo é obrigatório para o {{site.data.keyword.aios_short}} e, se ele estiver ausente, o monitoramento de Precisão falhará.

   Se o seu serviço da web do Azure não usar o nome padrão, mude o nome do campo de entrada para `"input1"`.

<p>&nbsp;</p>


### Amazon SageMaker
{: #wos-common-issues-aws}

- __*O algoritmo BlazingText não é suportado*__: o formato de carga útil de entrada do algoritmo BlazingText do Amazon SageMaker não é suportado na liberação atual do {{site.data.keyword.aios_short}}.

<p>&nbsp;</p>


### Instância de serviço de aprendizado de máquina customizado
{: #wos-common-issues-custom}

- O [módulo Python](/docs/services/ai-openscale?topic=ai-openscale-as-module) não tem atualmente a Explicabilidade funcionando para a instância de serviço Customizado. Isso é porque a instância de serviço Customizado requer uma predição numérica nos dados de resposta, que não está incluída com o script de módulo.

<p>&nbsp;</p>


- **Fragmentos de código inválidos**

    - Os fragmentos de código de cURL e Python fornecidos para a configuração do monitor são inválidos. Os fragmentos de código corretos são fornecidos aqui:

      *Criação de log de carga útil*

      ```cURL
      # Generate an ICP access token by passing an ICP username as $USERNAME, and ICP password as $PASSWORD in the following request

      curl -k -X GET \
      -user "$USERNAME:$PASSWORD" \
      "https://{{icp_hostname}:{{icp_port}}/v1/preauth/validateAuth"

      # the previous CURL request will return an auth token under "accessToken", that you will use as {icp_token} in the following payload logging request
      # TODO: manually define and pass:
      # request - input to scoring endpoint in supported by {{site.data.keyword.aios_short}} format - replace sample fields and values with proper ones
      # response - output from scored model in supported by {{site.data.keyword.aios_short}} format - replace sample fields and values with proper ones
      # - $SCORING_ID - ID of the scoring transaction
      # - $SCORING_TIME - Time (ms) taken to make prediction (for performance monitoring)

      SCORING_PAYLOAD='[{
        "scoring_id": "$SCORING_ID",
        "response_time": "$SCORING_TIME",
        "request": {
          "fields": ["AGE", "SEX", "BP", "CHOLESTEROL", "NA", "K"],
          "values": [[28, "F", "LOW", "HIGH", 0.61, 0.026]]
      },
      "response": {
        "fields": ["AGE", "SEX", "BP", "CHOLESTEROL", "NA", "K", "probability", "prediction", "DRUG"],
        "values": [[28, "F", "LOW", "HIGH", 0.61, 0.026, [0.82, 0.07, 0.0, 0.05, 0.03], 0.0, "drugY"]]
        },
        "binding_id": "{{binding_id}}",
        "subscription_id": "{{subscription_id}}",
        "deployment_id": "{{deployment_id}}"
      }]'

      curl -k -X POST https://{{icp_hostname}:{{icp_port}}/v1/data_marts/{{data_mart_id}}/scoring_payloads -d "$SCORING_PAYLOAD" \
      --header 'Content-Type: application/json' --header 'Accept: application/json' --header "Authorization: Bearer $ICP_TOKEN"
      ```

      *Criação de log de feedback*

      ```cURL
      # Generate an ICP access token by passing an ICP username as $USERNAME, and ICP password as $PASSWORD in the following request

      curl -k -X GET \
      --user "$USERNAME:$PASSWORD" \
      "https://{{icp_hostname}:{{icp_port}}/v1/preauth/validateAuth"

      # the previous CURL request will return an auth token under "accessToken" key that you will use as {icp_token} in the following payload logging request
      # TODO: manually define and pass:
      # fields - list of fields names - replace sample values with proper ones
      # values - feedback data records - replace sample values with proper ones
      # - $SCORING_ID - ID of the scoring transaction
      # - $SCORING_TIME - Time (ms) taken to make prediction (for performance monitoring)

      FEEDBACK_DATA='{
        "fields": ["AGE", "SEX", "BP", "CHOLESTEROL", "NA", "K", "DRUG"],
        "values": [[28, "F", "LOW", "HIGH", 0.61, 0.026, "drugB"]],
        "binding_id": "{{binding_id}}",
        "subscription_id": "{{subscription_id}}"
      }'

      curl -k -X POST https://{{icp_hostname}:{{icp_port}}/v1/data_marts/{{data_mart_id}}/feedback_payloads -d "$FEEDBACK_DATA" \
      --header 'Content-Type: application/json' --header 'Accept: application/json' --header "Authorization: Bearer $ICP_TOKEN"
      ```

    - O fragmento de código Java fornecido para o terminal de remoção de propensão é inválido. O fragmento de código correto é fornecido aqui:

      *Terminal de remoção de propensão*

      ```java
      /**
      At runtime you need to replace values for the following

      <HOSTNAME> - Host Name eg: aiopenscale.test.cloud.ibm.com
      <PORT> - Server Port
      <DATA_MART_ID> - DataMart id
      <SERVICE_BINDING_ID> - Service Binding id
      <ASSET_ID> - Asset id or the model id
      <DEPLOYMENT_ID> - Deployment id
      <TOKEN> - Bearer token

      */
      import org.apache.http.HttpVersion;
      import org.apache.http.client.fluent.Request;
      import org.apache.http.entity.ContentType;

      String bearerToken = "Bearer <TOKEN>";
      String URL = "https://<HOSTNAME>:<PORT>/v1/data_marts/<DATA_MART_ID>/service_bindings/<SERVICE_BINDING_ID>/subscriptions/<ASSET_ID>/deployments/<DEPLOYMENT_ID>/online";

      String payload = "{ \"fields\": [ \"field1\", \"field2\", \"field3\" ], \"values\": [ [ \"field1Value1\", \"field2Value1\", \"field3Value1\" ], [ \"field1Value2\", \"field2Value2\", \"field3Value2\" ]] }";

      byte[] res = Request.Post(URL).addHeader("Authorization", bearerToken).useExpectContinue().version(HttpVersion.HTTP_1_1)
                .bodyString(payload, ContentType.APPLICATION_JSON).execute().returnContent().asBytes();
      ```

<p>&nbsp;</p>


### Suporte do Navegador
{: #abt-browser}

O conjunto de ferramentas do serviço {{site.data.keyword.aios_short}} requer o mesmo nível de software do navegador que é requerido pelo {{site.data.keyword.cloud_notm}}. Consulte o tópico {{site.data.keyword.cloud_notm}}[Pré-requisitos](/docs/overview?topic=overview-prereqs-platform#browsers) para obter detalhes.

<p>&nbsp;</p>


### Cliente Python
{: #abt-python}

O [cliente Python do {{site.data.keyword.aios_short}}](http://ai-openscale-python-client.mybluemix.net/){: external} é uma biblioteca Python que permite que você trabalhe diretamente com o serviço {{site.data.keyword.aios_short}}. É possível usar o cliente Python, em vez da IU do cliente do {{site.data.keyword.aios_short}}, para configurar diretamente o banco de dados data mart, ligar seu mecanismo de aprendizado de máquina e selecionar e monitorar as implementações. Para obter exemplos usando o cliente Python dessa maneira, consulte os [blocos de notas de amostra do {{site.data.keyword.aios_short}}](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks).


## Problemas específicos do {{site.data.keyword.aios_short}}
{: #cloud-issues}

A limitação e os problemas a seguir são específicos do {{site.data.keyword.aios_short}} for {{site.data.keyword.Bluemix}}.

<p>&nbsp;</p>

### Limitações
{: #cloud-limitations}

- A liberação atual suporta apenas um banco de dados, uma instância do {{site.data.keyword.pm_full}} e uma instância do {{site.data.keyword.aios_short}}. 

- O banco de dados e a instância do {{site.data.keyword.pm_full}} devem ser implementados
na mesma conta {{site.data.keyword.cloud_notm}}.

- O {{site.data.keyword.aios_short}} usa um banco de dados PostgreSQL ou Db2 para armazenar dados relacionados ao modelo (dados de feedback, carga útil de pontuação) e métricas calculadas. Os planos Lite do Db2 não são suportados atualmente.

- O banco de dados do plano Lite grátis não é compatível com o GDPR. Se o seu modelo processar informações pessoalmente identificáveis (PII), você deverá comprar um novo banco de dados ou usar um banco de dados existente que esteja em conformidade com as regras do GDPR.



<p>&nbsp;</p>
## Próximos passos
{: #abt-next}

- [Iniciar](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted)
- Visualizar o [material de Referência da API](https://{DomainName}/apidocs/ai-openscale){: external}.
- [O que há
de novo no {{site.data.keyword.aios_short}}](/docs/services/ai-openscale?topic=ai-openscale-rn-relnotes)
- [Entrar em contato com a IBM](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson){: external}.
