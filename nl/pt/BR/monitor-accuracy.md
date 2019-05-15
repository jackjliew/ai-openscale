---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

keywords: accuracy, 

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

# Precisão
{: #acc-monitor}

A Precisão permite que você saiba o quão bem seu modelo prevê resultados.
{: shortdesc}

## Entendendo a Precisão
{: #acc-understand}

A Precisão pode significar coisas diferentes dependendo do tipo do algoritmo:

- *Classificação multiclasse*: a Precisão mede o número de vezes que qualquer classe foi prevista corretamente, normalizada pelo número de pontos de dados. Para obter mais detalhes, consulte [Classificação multiclasse ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#multiclass-classification){: new_window} na documentação do Apache Spark.

- *Classificação binária*: para um algoritmo de classificação binária, a precisão é medida como a área sob uma curva ROC. Consulte [Classificação binária ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#binary-classification){: new_window} na documentação do Apache Spark para obter mais detalhes.

- *Regressão*: os algoritmos de regressão são medidos usando o Coeficiente de Determinação, ou R2. Para obter mais detalhes, consulte [Avaliação do modelo de regressão ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#regression-model-evaluation){: new_window} na documentação do Apache Spark.

### Como ele funciona
{: #acc-works}

É necessário incluir os dados de feedback rotulados manualmente por meio da IU do {{site.data.keyword.aios_short}} conforme mostrado abaixo, usando um [cliente Python ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://ai-openscale-python-client.mybluemix.net/#feedbacklogging){: new_window} ou [API de Rest ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/apidocs/ai-openscale#post-feedback-payload){: new_window}.

Revise [Tipos de modelo suportados](/docs/services/ai-openscale?topic=ai-openscale-in-ov#in-mod) e [Estruturas suportadas](/docs/services/ai-openscale?topic=ai-openscale-in-ov#in-fram) para obter as limitações de monitoramento de precisão.

<!---
You need to add manually-labelled data into your feedback table for the accuracy computation to trigger. The feedback table is in the posgres schema with the name <model_id>_feedback.

You can create a performance monitoring system for your predictive models by creating an evaluation instance, and then defining the metrics and triggers for the automatic retraining and deploying of the new model. Spark, Keras and TensorFlow models are supported at this stage, with the following requirements:

- A training definition must be stored in the repository
- `training_data_reference` - must be defined as a part of the stored model's metadata
- `training_definition_url` - must be defined as a part of the stored model's metadata

Use the available [REST API ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://watson-ml-api.mybluemix.net/){: new_window} end-points directly to provide feedback data and kick off evaluation activities. For more information, see the [WML documentation ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://dataplatform.cloud.ibm.com/docs/content/analyze-data/ml-continuous-learning.html?audience=wdp&context=wdp){: new_window}.
--->

## Configurando o Monitor de Precisão
{: #acc-config}

1.  Na página *O que é Precisão?*, clique em **Avançar** para iniciar o processo de configuração.

    ![O Que É Precisão? página](images/accuracy-what-is.png)

1.  Na página *Configurar limite de precisão*, selecione um valor que represente um nível de precisão aceitável.

    A Precisão é um valor sintetizado de métricas relevantes de ciência de dados associadas a cada tipo de modelo específico. A pontuação é uma medida normalizada para permitir que você compare com facilidade a precisão em diferentes tipos de modelo. Em situações típicas, uma pontuação de precisão de 80 é suficiente.
    {: note}

    ![Set accuracy limit](images/accuracy-set-limit.png)

    Clique em **Avançar** para continuar.

1.  Agora, configure os tamanhos mínimo e máximo de amostra. O tamanho mínimo impede a medição de Precisão até que um número mínimo de registros esteja disponível no conjunto de dados de avaliação; isso assegura que o tamanho da amostra não seja muito pequeno para distorcer os resultados. O tamanho máximo da amostra ajuda a gerenciar melhor o tempo e o esforço que leva para avaliar o conjunto de dados; somente os registros mais recentes serão avaliados se esse tamanho for excedido.

     ![Configure sample size](images/accuracy-config-sample.png)

1.  Clique no botão **Avançar**.

    Um resumo de suas seleções é apresentado para revisão. Se você desejar mudar alguma coisa, clique no link **Editar** para essa seção.

1.  Clique em **Salvar** para concluir a configuração.

Agora você é apresentado com a opção de fornecer diretamente dados de feedback para seu modelo, para avaliar a precisão.

  ![Enviar dados de feedback](images/accuracy-send-feedback0.png)

Selecione o botão *Incluir dados de feedback* para fazer upload de um arquivo de dados formatado em CSV; configure o delimitador para corresponder aos seus dados.

Espera-se que o arquivo CSV de feedback tenha todos os valores de recurso e o valor de destino/rótulo designado manualmente. Por exemplo, os dados de treinamento do modelo de remédio contém os valores de recurso `"AGE"`, `"SEX"`, `"BP"`, `"CHOLESTEROL"`,`"NA"`,`"K"` e o valor de destino/rótulo `"DRUG"`. O arquivo CSV de feedback precisa incluir valores para esses campos; um exemplo seria semelhante a `[43, M, HIGH, NORMAL, 0.6345, 1.4587, DrugX]`. Se um cabeçalho for fornecido para o arquivo CSV de feedback, os nomes dos campos serão mapeados usando o cabeçalho. Caso contrário, a ordem do campo **DEVE** ser exatamente a mesma que no esquema de treinamento.
{: important}

Observe que os tipos de predição retornados por seu modelo e a coluna de rótulo/destino em seus dados de feedback devem corresponder.
{: note}

  ![Accuracy delimiter](images/accuracy-delimit.png)

Os tamanhos dos arquivos estão limitados atualmente a 8 MB.
{: note}

Alternativamente, é possível publicar dados de feedback usando os fragmentos de código `cURL` ou `Python` fornecidos.

Os campos e valores nos fragmentos de código precisam ser substituídos por seus valores reais, uma vez que os fornecidos são apenas exemplos.
{: important}

Também é possível escolher **Sair** para ignorar esta etapa opcional; ainda será possível fazer upload de um arquivo CSV para avaliação posteriormente.

### Próximos passos
{: #acc-next}

Na página *Configurar monitores*, é possível selecionar outra categoria de monitoramento.
