---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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

# Problemas conhecidos e limitações para o {{site.data.keyword.aios_short}}
{: #rn-12ki}

As listas a seguir contêm os problemas conhecidos e a limitação para o {{site.data.keyword.aios_full}}.
{: shortdesc}

<p>&nbsp;</p>

## Limitações
{: #wos-limitations}

- O {{site.data.keyword.aios_short}} suporta múltiplos mecanismos de aprendizado de máquina, desde que você configure mecanismos adicionais usando o SDK do Python.

- A liberação atual suporta somente um banco de dados, uma instância do {{site.data.keyword.pm_full}} e uma instância do {{site.data.keyword.aios_short}}

- O banco de dados e a instância do {{site.data.keyword.pm_full}} devem ser implementados
na mesma conta {{site.data.keyword.cloud_notm}}.

- O plano Lite (grátis) tem os limites mensais a seguir:

    - Dois modelos implementados monitorados
    - 20 transações explicadas
    - 50.000 registros de carga útil (acumulativos)
    - 50.000 registros de feedback (acumulativos)

- O {{site.data.keyword.aios_short}} usa um banco de dados PostgreSQL ou Db2 para armazenar dados relacionados ao modelo (dados de feedback, carga útil de pontuação) e métricas calculadas. Os planos Lite do Db2 não são suportados atualmente.

- Há um limite de licença de 20 modelos implementados por instância do {{site.data.keyword.aios_short}}.

- Para o {{site.data.keyword.pm_full}}, a entrada de pontuação para modelos de classificação de imagem que são enviados para a criação de log de carga útil não pode exceder 1 MB. Para evitar problemas de tempo limite, as imagens não devem exceder 125 x 125 pixels e devem ser enviadas sequencialmente de modo que a explicação para a segunda imagem seja solicitada quando a primeira estiver concluída.

- O banco de dados do plano Lite grátis não é compatível com o GDPR. Se o seu modelo processar informações pessoalmente identificáveis (PII), você deverá comprar um novo banco de dados ou usar um banco de dados existente que esteja em conformidade com as regras do GDPR. 

- A explicabilidade para modelos de texto não estruturados não é suportada para linguagens de script contínuas, como japonês, chinês e coreano, que não usam caracteres de espaço em branco ou de pontuação para separar as palavras.



<p>&nbsp;</p>

## Problemas Comuns
{: #wos-common-issues}

Os problemas a seguir são comuns ao {{site.data.keyword.aios_full}} no {{site.data.keyword.Bluemix}} e {{site.data.keyword.wos4d_full}}.

<p>&nbsp;</p>

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


## Problemas conhecidos para o {{site.data.keyword.wos4d_notm}}
{: #rn-16April2019ki}

Os problemas a seguir são específicos para o {{site.data.keyword.wos4d_full}}.

<p>&nbsp;</p>


### IBM SPSS Collaboration and Deployment Services (C&DS)
{: #rn-16April2019ki-icp-spss}

- **Suporte limitado à explicabilidade**

   - A explicabilidade é suportada para modelos binários e para modelos de multiclasses do SPSS que retornam probabilidades para todas as classes. 
   - A explicabilidade não é suportada para modelos de multiclasses do SPSS que retornam apenas a probabilidade da classe vencedora.


<p>&nbsp;</p>


- **O ID de implementação não pode conter o caractere de sublinhado (_) no IBM SPSS Collaboration and Deployment Services (C&DS)**

    - Remova o caractere de sublinhado (_) de `deployment_id` para uma assinatura.

<p>&nbsp;</p>




- O **IBM SPSS Collaboration and Deployment Services (C&DS) (somente o tipo binário) requer que uma solicitação de carga útil adicional seja feita**

    - Para as assinaturas binárias do IBM SPSS Collaboration & Deployment Services, deve-se fazer outra [solicitação de criação de log (pontuação) de carga útil](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-cdb-connect#cdb-scoring) depois de [preparar os monitores para uma implementação](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mo-config#mo-config) ou depois que todos os monitores forem configurados. Isso assegura que a [Explicabilidade](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-ie-ov#ie-ov) será precisa.

<p>&nbsp;</p>


- **A contagem de registros corrigidos do IBM SPSS C&DS (somente o tipo binário) pode estar errada**

    - Para as assinaturas binárias do IBM SPSS Collaboration & Deployment Services, a contagem de *Registros corrigidos* pode não estar exata quando visualizada usando o botão **Visualizar transações**.

<p>&nbsp;</p>

### Métricas
{: #rn-16April2019ki-icp-metrics}

- **Métricas de desempenho do {{site.data.keyword.pm_full}} não coletadas**

    - Em um ambiente do Cloud Pak for Data, as métricas de desempenho do {{site.data.keyword.pm_full}} não são coletadas.

<p>&nbsp;</p>

- **Limitações de suporte à explicabilidade**

    - Ao construir seus modelos, não inclua a coluna de destino (etiqueta) da solicitação de entrada para pontuação. Se o modelo requerer que a coluna de destino seja incluída na solicitação de entrada, a verificação de propensão, a remoção da propensão e a explicabilidade não funcionarão.


<p>&nbsp;</p>


### Funções do Python
{: #rn-16April2019ki-icp-python}

- **Funções do Python não suportadas**

    - A verificação de propensão, a remoção da propensão e a explicabilidade não são suportadas para as funções do Python na liberação atual.

<p>&nbsp;</p>


### Instalação e Configuração
{: #rn-16April2019ki-icp-install}


- **O script de desinstalação não exclui tópicos do Kafka**

    - A execução do script de desinstalação não remove os tópicos do Kafka do {{site.data.keyword.aios_short}} criados no EventStream durante a instalação.

<p>&nbsp;</p>

### Bancos de Dados
{: #rn-16April2019ki-icp-dbs}

- **Limitação de tamanho de linha usando o Db2 Warehouse**

    - Há um limite de tamanho de linha de 1 MB para o Db2 Warehouse. Quando houver múltiplas colunas de texto (mais de 30) (32.000 bytes para cada VARCHAR), o limite será excedido. Essa limitação é mais perceptível quando se usa o Amazon SageMaker, pois o formato nativo do SageMaker tem todas as colunas no formato de sequência.

       Como o {{site.data.keyword.aios_short}} usa o espaço de tabela padrão para criar objetos de banco de dados, os limites reais dependem da configuração do banco de dados. Informações adicionais sobre essa limitação estão disponíveis na [documentação do Db2 no IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/SSEPGG_11.1.0/com.ibm.db2.luw.sql.ref.doc/doc/r0001029.html).





## Suporte do Navegador
{: #abt-browser}

O conjunto de ferramentas do serviço {{site.data.keyword.aios_short}} requer o mesmo nível de software do navegador que é requerido pelo {{site.data.keyword.cloud_notm}}. Consulte o tópico {{site.data.keyword.cloud_notm}}[Pré-requisitos](/docs/overview?topic=overview-prereqs-platform#browsers) para obter detalhes.

<p>&nbsp;</p>


## Cliente Python
{: #abt-python}

O [cliente Python do {{site.data.keyword.aios_short}}](http://ai-openscale-python-client.mybluemix.net/){: external} é uma biblioteca Python que permite que você trabalhe diretamente com o serviço {{site.data.keyword.aios_short}}. É possível usar o cliente Python, em vez da IU do cliente do {{site.data.keyword.aios_short}}, para configurar diretamente o banco de dados data mart, ligar seu mecanismo de aprendizado de máquina e selecionar e monitorar as implementações. Para obter exemplos usando o cliente Python dessa maneira, consulte os [blocos de notas de amostra do {{site.data.keyword.aios_short}}](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks).

<p>&nbsp;</p>
## Próximos passos
{: #abt-next}

- [Introdução](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-gs-get-started) ao serviço.
- Visualizar o [material de Referência da API](https://{DomainName}/apidocs/ai-openscale){: external}.

Você ainda tem dúvidas? 

- [O quê há de novo](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-rn-relnotes)
- [Entrar em contato com a IBM](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson){: external}.
