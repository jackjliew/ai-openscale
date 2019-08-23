---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: ai, getting started, tutorial, understanding, fast start

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

# O tutorial de configuração interativa
{: #gs-obj}

Neste tutorial, você aprende como provisionar os serviços do {{site.data.keyword.Bluemix_notm}} necessários, configurar um projeto, implementar um modelo de amostra no Watson Studio e configurar monitores no {{site.data.keyword.aios_short}}.
{: shortdesc}

1. [Provisionar os serviços de aprendizado de máquina e de armazenamento do {{site.data.keyword.Bluemix_notm}}](/docs/services/ai-openscale?topic=ai-openscale-gs-obj#gs-prps).
2. [Configurar um projeto do Watson Studio e criar, treinar e implementar um modelo de aprendizado de máquina](/docs/services/ai-openscale?topic=ai-openscale-gs-obj#gs-setup).
3. [Configurar e explorar confiança, transparência e explicabilidade para seu modelo](/docs/services/ai-openscale?topic=ai-openscale-gs-obj#gs-confaios).

## Provisionar serviços de pré-requisito do {{site.data.keyword.Bluemix_notm}}
{: #gs-prps}

Além do {{site.data.keyword.aios_short}}, para concluir este tutorial, são necessárias as contas e os serviços a seguir.

**Importante**: para obter melhor desempenho, é recomendado que os serviços de pré-requisito sejam criados na mesma região que o {{site.data.keyword.aios_short}}. Para visualizar os locais disponíveis para o {{site.data.keyword.aios_short}}, consulte [Disponibilidade de serviço](/docs/resources?topic=resources-services_region){: external}.

1.  Efetue login em sua [conta do {{site.data.keyword.Bluemix_notm}}](https://{DomainName}){: external} com seu {{site.data.keyword.ibmid}}.
1.  Para cada um dos serviços a seguir que você ainda não tenha associado à sua conta, crie uma instância clicando no link, fornecendo um nome ao serviço, selecionando o plano **Lite** (grátis) e clicando no botão **Criar**:

    - [{{site.data.keyword.DSX}}](https://{DomainName}/catalog/services/watson-studio){: external}

      ![Watson Studio](images/wos-watson_studio.png)

    - [{{site.data.keyword.pm_full}}](https://{DomainName}/catalog/services/machine-learning){: external}

      ![Machine Learning](images/machine_learning.png)

    - [Armazenamento de objetos](https://{DomainName}/catalog/services/cloud-object-storage){: external}

      ![Object Storage](images/object_storage.png)


## Configurar um projeto do Watson Studio
{: #gs-setup}

1.  Efetue login em sua [conta do Watson Studio](https://dataplatform.ibm.com/){: external} e inicie criando um novo projeto. Clique em **Criar um projeto**.

    ![Criar projeto do Watson Studio](images/studio_create_proj.png)

1.  Clique no bloco **Criar um projeto vazio**.
1.  Dê ao seu projeto um nome e uma descrição, certifique-se de que o serviço Object Storage criado na etapa anterior esteja selecionado no menu **Armazenamento** e clique em **Criar**.

### Associar seus serviços do {{site.data.keyword.Bluemix_notm}} ao seu projeto do Watson
{: #gs-assoc}

1.  Abra seu projeto do Watson Studio e selecione a guia **Configurações**. Na seção **Serviços associados**, clique em **Incluir serviço** e, em seguida, clique em **Watson**.

    ![Incluir Watson Service](images/add_watson_service.png)

1.  Clique no link **Incluir** no bloco **Aprendizado de máquina**.
2.  Na guia **Existente**, na lista suspensa **Instância de serviço existente**, clique no serviço criado anteriormente.
3. Clique em **Selecionar**.

### Incluir o modelo `Credit Risk`
{: #gs-addmod}

1.  No {{site.data.keyword.DSX}}, selecione a guia **Ativos** de seu projeto, role para a seção **Modelos de aprendizado de máquina do Watson** e clique no botão **Novo modelo de aprendizado de máquina do Watson**.

1.  Na seção **Selecionar tipo de modelo**, selecione **Da amostra** e o modelo `Credit Risk` e, em seguida, clique em **Criar**.

    ![o bloco Risco de crédito é mostrado](images/credit-sample-model.png)

### Implementar o modelo `Credit Risk`
{: #gs-depmod}

1.  Na página do modelo `Credit Risk`, clique na guia **Implementações** e, em seguida, clique em **Incluir implementação**.
1.  Insira `credit-risk-deploy` como o nome para sua implementação e selecione o tipo de implementação **Serviço da web**.
1.  Clique em **Salvar**.

## Configurar o {{site.data.keyword.aios_short}}
{: #gs-confaios}

Agora que o modelo de aprendizado de máquina foi implementado, é possível configurar o {{site.data.keyword.aios_short}} para assegurar confiança e transparência com seus modelos.

### Provisionar o {{site.data.keyword.aios_short}}
{: #gs-provaios}

1.  [Provisione uma nova instância de serviço do {{site.data.keyword.aios_short}}](https://{DomainName}/catalog/services/watson-openscale){: external}

    ![{{site.data.keyword.aios_short}}](images/wos-cloud-tile.png)

2.  Forneça um nome ao seu serviço, selecione o **Plano Lite** e clique em **Criar**.

1.  Selecione a guia **Gerenciar** de sua instância do {{site.data.keyword.aios_short}} e clique no botão **Ativar aplicativo**. A página de demo **Bem-vindo ao {{site.data.keyword.aios_short}}** é aberta.
2. Para este tutorial, clique em **Não**.

### Selecionar um banco de dados
{: #gs-db-choice}

Em seguida, é necessário escolher um banco de dados. Você tem duas opções: o banco de dados grátis ou um banco de dados existente ou novo.

2. Para este tutorial, selecione o bloco **Usar o banco de dados do plano Lite grátis**.

   A banco de dados grátis tem algumas limitações importantes. Ele é um banco de dados hospedado
que não concede acesso separado a ele. Ele fornece o acesso do {{site.data.keyword.aios_short}}
ao banco de dados e aos dados. Ele não está em conformidade com o GDPR. Veja detalhes mais completos sobre cada uma dessas opções no tópico [Especificando
um banco de dados](/docs/services/ai-openscale?topic=ai-openscale-connect-db). O banco de dados existente pode ser um banco de dados PostgreSQL ou um banco de dados Db2.
    {: tip}

   ![Select database](images/gs-set-lite-db2.png)

1.  Revise os dados de resumo e clique em **Salvar**. Confirme e, quando solicitado, clique no botão **Continuar com a configuração**.

    Um ID do data mart também é listado, que é a mesma coisa que um ID de instância do {{site.data.keyword.aios_short}}.
    {: tip}

    ![Revisão de resumo](images/gs-setup-summary4.png)

1.  Sua tela pode ser semelhante à captura de tela a seguir. Como você usará um método GUI para classificar seus dados, basta selecionar o botão **Configurar monitores** para concluir essa configuração.

    ![Código de solicitação de pontuação](images/gs-config-send-scoring.png)

### Conectar o {{site.data.keyword.aios_short}} ao seu modelo de aprendizado de máquina
{: #gs-ctmod}


1.  Clique no bloco **Watson Machine Learning** e, em seguida, clique em **Salvar**.

1.  Para este tutorial, selecione sua instância do {{site.data.keyword.pm_full}} no menu e clique em **Avançar**.

    Você também tem a opção de selecionar um local diferente do {{site.data.keyword.pm_short}}. Consulte [Especificando uma instância de serviço do {{site.data.keyword.pm_full}}](/docs/services/ai-openscale?topic=ai-openscale-wml-connect) para obter informações adicionais.
    {: note}

    ![Configurar instância do {{site.data.keyword.pm_short}}](images/gs-set-wml.png)

Agora você está apto a selecionar os modelos implementados que serão monitorados pelo {{site.data.keyword.aios_short}}.


### Forneça um conjunto de dados de amostra para seu modelo
{: #gs-samp}

Antes de poder configurar seus monitores, deve-se gerar pelo menos uma solicitação de pontuação
em seu modelo para gerar a criação de log de carga útil que os monitores possam consumir. Nesta seção, você fornecerá dados de amostra ao Watson Studio na forma de um arquivo JSON para gerar uma solicitação de pontuação.

1.  Faça download do arquivo [credit_payload_data.json](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/ai-openscale/credit_payload_data.json).

1.  Na guia **Implementações** de seu projeto do Watson Studio, clique no
link **credit-risk-deploy**, clique na guia **Teste** e selecione
o ícone de entrada JSON.

    ![Teste JSON](images/json_test02.png)

1.  Agora, abra o arquivo `credit_payload_data.json` transferido por download e copie o conteúdo para o campo JSON na guia **Teste**. Clique no botão **Prever** para enviar e pontuar cargas úteis de treinamento para seu modelo.

    ![Previsão JSON](images/json_test03.png)

## Próximos passos
{: #gs-next-steps-config}

Continue com este tutorial concluindo as etapas a seguir:

1. [Prepare monitores para a implementação](/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-select-deploy).

   Para preparar monitores, deve-se selecionar um dos modelos implementados e incluí-lo no painel. Na guia **Insights**, clique em um bloco de implementação ou no botão **Incluir no painel** para selecionar um modelo implementado e clique em **Configurar**.

2. [Configurar a criação de log de carga útil](/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-work-data).

   Na seção **Criação de log de carga útil**, deve-se especificar o tipo de entrada.

3. [Configure os detalhes do modelo](/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-work-model-dets).

   Na seção **Detalhes do modelo**, deve-se registrar os detalhes do modelo. Para este tutorial, selecione **Configurar monitores manualmente**.

4. [Configure o monitoramento de qualidade](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor).

   Na seção **Qualidade**, configure o limite de alerta de qualidade e os tamanhos de amostra.

5. [Configure o monitoramento de justiça](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor).

   Na seção **Justiça**, escolha quais recursos terão a justiça monitorada. Para cada recurso selecionado, o {{site.data.keyword.aios_short}} monitorará a propensão do modelo implementado para um resultado favorável para um grupo sobre o outro. Embora os recursos sejam monitorados individualmente, a remoção de propensão corrige problemas para todos os recursos.

6. [Configure o monitor de detecção de desvio](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-config).

   Na seção **Desvio**, configure um modelo de detecção de desvio.
   
5. [Forneça um conjunto de dados de feedback de amostra para seu modelo](/docs/services/ai-openscale?topic=ai-openscale-fmt-upld-fdbk-data#fmt-upld-fdbk-data-upld-csv).

   Para permitir o monitoramento da qualidade, deve-se fornecer ao modelo dados de feedback. Os dados de qualidade não serão exibidos no painel até que isso seja feito. É possível gerar as solicitações de uma só vez, incluindo dados de feedback de amostra no modelo para pontuação. Para esta tarefa, você fará download de um arquivo CSV que contém dados de feedback de amostra.

6. [Obter insights](/docs/services/ai-openscale?topic=ai-openscale-io-ov).

   Depois de configurar o monitoramento de precisão, a verificação de precisão é executada após uma hora. Em um sistema de produção, isso faz sentido para que seu painel possa acumular dados de feedback. Para os propósitos deste tutorial, você provavelmente desejará acionar a verificação de precisão manualmente depois de incluir seus dados de feedback, de modo que seja possível ver os resultados no painel **Insights**.

   Para verificar o resultado imediatamente, na página **Insights**, selecione uma implementação, clique em uma das métricas de **Qualidade** e, em seguida, clique em **Verificar qualidade agora**.
