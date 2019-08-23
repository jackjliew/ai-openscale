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

Neste tutorial, você executará as etapas a seguir:

- [Provisionar os serviços de aprendizado de máquina e de armazenamento do {{site.data.keyword.Bluemix_notm}}](/docs/services/ai-openscale?topic=ai-openscale-gs-obj&locale=en-US#gs-prps).
- [Configurar um projeto do Watson Studio e criar, treinar e implementar um modelo de aprendizado de máquina](/docs/services/ai-openscale?topic=ai-openscale-gs-obj&locale=en-US#gs-setup).
- [Configurar e explorar confiança, transparência e explicabilidade para seu modelo](/docs/services/ai-openscale?topic=ai-openscale-gs-obj&locale=en-US#gs-confaios).

## Provisionar serviços de pré-requisito do {{site.data.keyword.Bluemix_notm}}
{: #gs-prps}

Além do {{site.data.keyword.aios_short}}, para concluir este tutorial, são necessárias as contas e os serviços a seguir.

**Importante**: para obter melhor desempenho, é recomendado que os serviços de pré-requisito sejam criados na mesma região que o {{site.data.keyword.aios_short}}. Para visualizar os locais disponíveis para o {{site.data.keyword.aios_short}}, consulte [Disponibilidade de serviço](/docs/resources?topic=resources-services_region).

1.  Efetue login em sua [conta do {{site.data.keyword.Bluemix_notm}}](https://{DomainName}){: external} com seu {{site.data.keyword.ibmid}}.
1.  Para cada um dos serviços a seguir que você ainda não tenha associado à sua conta, crie uma instância clicando no link, fornecendo um nome ao serviço, selecionando o plano **Lite** (grátis) e clicando no botão **Criar**:

    - [{{site.data.keyword.DSX}}](https://{DomainName}/catalog/services/watson-studio){: external}

      ![Watson Studio](images/watson_studio.png)

    - [{{site.data.keyword.pm_full}}](https://{DomainName}/catalog/services/machine-learning){: external}

      ![Machine Learning](images/machine_learning.png)

    - [Armazenamento de objetos](https://{DomainName}/catalog/services/cloud-object-storage){: external}

      ![Object Storage](images/object_storage.png)


## Configurar um projeto do Watson Studio
{: #gs-setup}

1.  Efetue login em sua [conta do Watson Studio](https://dataplatform.ibm.com/){: external} e inicie criando um novo projeto. Clique em **Criar um projeto**.

    ![Criar projeto do Watson Studio](images/studio_create_proj.png)

1.  Clique no bloco **Padrão**.

    ![Selecionar projeto Padrão do Watson Studio](images/studio_create_standard.png)

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

1.  Agora você está apto a selecionar os modelos implementados que serão monitorados pelo {{site.data.keyword.aios_short}}. Selecione o modelo criado e implementado e clique em **Avançar**.

    ![Selecionar modelos implementados](images/wos-select-model-deployment.png)



### Forneça um conjunto de dados de amostra para seu modelo
{: #gs-samp}

Antes de poder configurar seus monitores, deve-se gerar pelo menos uma solicitação de pontuação
em seu modelo para gerar a criação de log de carga útil que os monitores possam consumir. Nesta seção, você fornecerá dados de amostra no formato de um arquivo JSON para gerar uma solicitação de pontuação.

1.  Faça download do arquivo [credit_payload_data.json](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/ai-openscale/credit_payload_data.json).

1.  Na guia **Implementações** de seu projeto do Watson Studio, clique no
link **credit-risk-deploy**, clique na guia **Teste** e selecione
o ícone de entrada JSON.

    ![Teste JSON](images/json_test02.png)

1.  Agora, abra o arquivo `credit_payload_data.json` transferido por download e copie o conteúdo para o campo JSON na guia **Teste**. Clique no botão **Prever** para enviar e pontuar cargas úteis de treinamento para seu modelo.

    ![Previsão JSON](images/json_test03.png)

### Preparando para Monitoramento
{: #gs-prepmon}

1.  Agora, na instância do {{site.data.keyword.aios_short}}, selecione sua implementação e clique em **Iniciar**.

    ![Selecionar implementação](images/wos-select-model-deployment.png)

1.  Especifique o recurso que contém a resposta que o modelo irá prever. (Em seu banco de dados,
qual coluna da tabela contém valores de predição ou rótulos?) Nesse caso, o modelo prevê risco de crédito, portanto, selecione a coluna **Risco** e clique em **Avançar**.

    ![Preparar-se para o monitoramento](images/wos-select-model-deployment.png)

1.  Em seguida, você fornecerá informações sobre seu modelo e dados de treinamento. Clique em **Avançar**.

    ![Preparar explicação](images/config-what-monitor.png)

1.  No menu **Tipo de dados**, selecione **Numérico/categórico** como o tipo de dados que sua implementação analisa e clique em **Avançar**.

    ![Select input type](images/config-input-monitor.png)

1.  Para dados numéricos ou categóricos, é necessário fornecer informações sobre os dados de treinamento para seu modelo, a fim de configurar os monitores. Selecione **Configurar manualmente monitores** para fornecer informações de conexão para seus dados de treinamento.

    ![Select config type](images/config-manual-monitor.png)

1.  O tipo de algoritmo é importante para monitorar suas métricas de modelo, como Precisão. Como a previsão que o modelo pode fazer é "Risco" ou "Sem risco", selecione o **Classificação binária** [tipo de algoritmo](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-understand) e clique em **Avançar**.

    ![Binário](images/binary.png)

1.  As informações de local para os dados de amostra são pré-preenchidas na tela a seguir. Selecione **Avançar** para continuar.

    ![Especificar o local do Db2 da página de dados de treinamento](images/gs-config-train-db2-monitor.png)

1.  O esquema e a tabela também são pré-preenchidos. Clique em **Avançar** para continuar.

    ![Especificar o local do Db2 do esquema e da tabela de treinamento](images/gs-fair-config-table-db2.png)

1.  Agora, deve-se especificar o recurso que contém a(s) resposta(s) que o modelo irá prever (em outras palavras, em seu banco de dados, qual coluna da tabela contém valores de predição (rótulos)). Nesse caso, o modelo irá prever o risco de crédito, portanto, selecione a coluna **Risco** e clique em **Avançar**.

    Seu banco de dados de treinamento tem os valores que você forneceu para treinar seu modelo.
    {: note}

    ![Prever entrada de rótulo](images/gs-config-label.png)

1.  Selecione as colunas usadas para treinar o modelo. Esses são os dados que a implementação do modelo espera em uma solicitação. Todas as colunas de dados, exceto `_training`, são entradas para o modelo. Selecione todas as outras entradas e clique em **Avançar**.

    ![Entradas de explicabilidade](images/explain_inputs1.png)

1.  Para dados categóricos, deve-se identificar as colunas que agora contêm números inteiros, mas originalmente continham valores de texto. Selecione os valores conforme mostrado aqui.

    ![Entradas de explicabilidade](images/config_categories.png)

1.  Revise o resumo de seleção, clique em **Salvar** e, em seguida, clique em **OK**.

### Configurar monitoramento de justiça
{: #gs-cfgfair}

1.  Clique em **Justiça**.

1.  Leia sobre justiça e clique em **Avançar**. Para obter mais informações, consulte [Justiça](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor).

1.  Agora é possível escolher quais recursos monitorar para justiça. Para cada recurso selecionado, o {{site.data.keyword.aios_short}} monitorará a propensão do modelo implementado para um resultado favorável para um grupo sobre o outro. Neste exemplo, monitoraremos os recursos **Sexo** e **Idade**.

    Os recursos são monitorados individualmente, mas qualquer despropensão corrigirá problemas para todos os recursos juntos. Clique nos blocos **Sexo** e **Idade** e clique em **Avançar**.

1.  O {{site.data.keyword.aios_short}} trabalha para detectar propensão em relação a um grupo monitorado em comparação com um grupo de referência. Para o recurso **Sexo**, inclua o valor `male` no **Grupo de referência** e o valor `female` para o **Grupo monitorado** e clique em **Avançar**.

    O modelo será sinalizado como propenso para **Sexo** se as razões de previsão de Risco para o grupo monitorado forem diferentes das proporções para o grupo de referência. Então, se o modelo prevê risco para clientes do sexo masculino em 60% do tempo e para clientes do sexo feminino em 20% do tempo, ele é propenso.

    ![Grupos de gêneros](images/gender_groups1.png)

1.  Designe um limite de justiça para **Sexo**. O painel de operações exibirá um alerta se a classificação de justiça exceder o limite configurado. Configure o limite em 90% e clique em **Avançar**.

1.  Para o recurso **Idade**, inclua os valores `26-74` no **Grupo de referência** e os valores `19-25` no **Grupo monitorado** e clique em **Avançar**.

    Assim como no caso de **Sexo**, o modelo será sinalizado como propenso para **Idade** se as razões de previsão de Risco para o grupo monitorado forem diferentes das proporções para o grupo de referência. Portanto, se os clientes com idade entre 26 e 74 anos receberem uma previsão de Risco em uma proporção diferente da previsão de clientes com idades entre 19 e 25 anos, o modelo será propenso.

    ![Grupos do BP](images/age_groups.png)

1.  Configure o limite para **Idade** em 90% e clique em **Avançar**.

1.  Arraste e solte valores do campo **Valores de dados de treinamento** para os campos **Valores favoráveis** e **Valores desfavoráveis**. Para este tutorial, o valor favorável é **Nenhum risco** e o valor desfavorável é **Risco**. Clique em **Avançar**.

    O {{site.data.keyword.aios_short}} detecta automaticamente qual coluna no banco de dados de criação de log de carga útil contém os valores de previsão e os apresenta no campo **Valores de dados de treinamento**. Observe que enquanto seu banco de dados de treinamento tem valores que foram fornecidos para treinar seu modelo, o banco de dados de criação de log de carga útil contém dados de feedback coletados no tempo de execução do modelo, que podem, opcionalmente, ser usados para retreinar e reimplementar seu modelo.
    {: note}

    ![Valores positivos e negativos](images/pos_and_neg2.png)

1.  Use a régua de controle para ajustar o tamanho mínimo de amostra para 100, em seguida, clique em **Avançar**.

    ![Tamanho mínimo](images/gs-fair-config-sample.png)

    Para este tutorial, o tamanho mínimo da amostra é configurado para 100. Normalmente, recomenda-se um tamanho de amostra maior para garantir que o tamanho da amostra não seja muito pequeno, o que distorceria os resultados.
    {: note}

1.  Revise suas opções, clique em **Salvar** e, em seguida, clique em **OK**.

    ![Resumo da configuração](images/fair-summary.png)

    A janela a seguir, que fornece um terminal de pontuação despropenso, aparece. Como este tutorial usa o método da GUI e não a CLI para pontuar dados, para continuar, clique em **OK**.

    ![API de despropensão](images/gs-insight-debias-api.png)

### Configurar monitoramento de precisão
{: #gs-cfgac}

1.  Clique em **Precisão**.

1.  Leia sobre precisão e clique em **Avançar**. Para obter mais informações, consulte [Precisão](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor).

1.  Configure o limite de alerta de precisão em 90% e clique em **Avançar**.

1.  Na próxima tela, use a régua de controle para ajustar o tamanho mínimo de amostra para 10, em seguida, clique em **Avançar**.

    Para este tutorial, o tamanho mínimo da amostra é configurado para 10. Normalmente, recomenda-se um tamanho de amostra maior para garantir que o tamanho da amostra não seja muito pequeno, o que distorceria os resultados.
    {: note}

1.  Para o tamanho máximo de amostra, use 10000. Clique em **Avançar**.

1.  Revise suas opções, clique em **Salvar** e, em seguida, clique em **OK**.

1.  Finalmente, você é apresentado a uma opção para incluir dados de feedback, que é coberta na próxima seção. Por enquanto, feche a janela clicando em **OK**, sem clicar no botão **Incluir dados de feedback**.

    Para obter mais detalhes, consulte [Configurando o monitor de precisão](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-config).

## Forneça um conjunto de dados de feedback de amostra para seu modelo
{: #gs-smpfeed}

Para ativar o monitoramento para precisão, deve-se fornecer dados de feedback ao seu modelo. Os dados de precisão não aparecerão no painel até que isso seja feito. É possível gerar as solicitações de uma só vez, incluindo dados de feedback de amostra no modelo para pontuação. Para esta tarefa, você fará download de um arquivo CSV que contém dados de feedback de amostra.

1.  Faça download do arquivo [credit_feedback_data.csv](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/ai-openscale/credit_feedback_data.csv).

1.  No {{site.data.keyword.aios_short}}, clique na guia **Insights**.

    ![Insights](images/insight-dash-tab.png)

1.  Clique no bloco para seu modelo implementado.

    ![Guia Insights - sem dados](images/gs-insight-overview.png)

1.  Em seguida, clique em **Configurar monitores**.

    ![O ícone Editar é exibido](images/gs-insight-edit-icon.png)

1.  Clique em **Precisão** e, em seguida, em **Feedback**.
1.  Clique no botão **Incluir dados de feedback** e selecione o arquivo `credit_feedback_data.csv` que você transferiu por download e clique em **Abrir**. 
2. Selecione o delimitador **Vírgula (,)** e, em seguida, clique em **Selecionar**.

    Os tamanhos dos arquivos são limitados atualmente a 8 MB.
    {: note}

    ![Accuracy delimiter](images/accuracy-delimit.png)

A inclusão do arquivo CSV fornece dados de feedback para seu modelo.

## Configurar o monitor de desvio
{: gs-drift-config}

Para obter informações sobre como configurar o monitor de desvio, consulte [Configurar o monitor de detecção de desvio](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-config).

## Visualização de resultados
{: #gs-viewres}

Depois de configurar o monitoramento de precisão, a verificação de precisão é executada após uma hora. Em um sistema de produção, isso faz sentido para que seu painel possa acumular dados de feedback. Para os propósitos deste tutorial, você provavelmente desejará acionar a verificação de precisão manualmente depois de incluir seus dados de feedback, de modo que seja possível ver os resultados no painel **Insights**.

Para verificar o resultado imediatamente, na página **Insights**, selecione uma implementação e, em seguida, clique em **Verificar justiça agora** ou em **Verificar qualidade agora**.

Para aprender sobre a interpretação dos resultados, consulte [Obtendo insights](/docs/services/ai-openscale?topic=ai-openscale-io-ov)

## Informações Relacionados
{: #wos-info}

- Para aprender sobre os biases, consulte [Equidade](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mf-monitor).
- Para aprender sobre o quão bem o seu modelo prevê resultados, consulte [Precisão](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-acc-monitor).
- Para aprender sobre interpretação de gráficos, dados e transações, consulte [Monitorando a justiça, a média de solicitações por minuto e a precisão](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart).
