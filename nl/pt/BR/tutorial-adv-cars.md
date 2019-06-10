---

title: Confiança e transparência para os modelos de aprendizado de máquina com o {{site.data.keyword.aios_short}}
description: Monitor your machine learning deployments for bias, accuracy, and explainability
duration: 120
intro: In this extended tutorial, you will provision IBM Cloud machine learning and data services, create and deploy machine learning models in Watson studio, and configure the new IBM {{site.data.keyword.aios_full}} product to monitor your models for trust and transparency.
takeaways:
- See how {{site.data.keyword.aios_short}} provides trust and transparency for AI models
- Understand how IBM Cloud services and Watson Studio technologies can provide a seamless, AI-driven customer experience

copyright:
  years: 2018, 2019
lastupdated: "2019-02-05"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Tutorial (Avançado)
{: #tadv-tutorial-advanced}

## Cenário
{: #tadv-scenario}

Uma empresa de aluguel de carros coletou dados de feedback sobre a satisfação do cliente. O modelo apresentado usa esses dados para prever um curso de ação para acompanhar um cliente, por exemplo, para fornecer um voucher para seu próximo aluguel.

O modelo usa o ID de campos de dados do cliente (um número de ID), GÊNERO, STATUS (solteiro ou casado), FILHOS (número), IDADE, STATUS DO CLIENTE (ativo ou inativo), PROPRIETÁRIO DO CARRO (sim ou não), ATENDIMENTO AO CLIENTE (comentário do cliente), SATISFAÇÃO (satisfeito ou insatisfeito) e ÁREA DE NEGÓCIOS (relacionada ao produto ou serviço) para prever um dos quatro valores (NA, voucher, upgrade grátis, coleta on demand) para o campo de dados AÇÃO.

## Pré-requisitos
{: #tadv-prereqs}

Para concluir este tutorial, você precisará:

- Uma conta do [Watson Studio ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://dataplatform.ibm.com/){: new_window}.
- Uma conta do [{{site.data.keyword.cloud_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}){: new_window}.

Durante o tutorial, você provisionará os serviços do {{site.data.keyword.cloud_notm}} Lite (grátis) a seguir:

- Aprendizado da Máquina
- Apache Spark
- Armazenamento de objetos

Você também provisionará o Serviço do {{site.data.keyword.cloud_notm}} **pago**:

- PostgreSQL

  Um crédito de $200 do {{site.data.keyword.cloud_notm}} pode ser obtido convertendo para uma conta paga com um cartão de crédito. Se você já tiver uma conta paga, receberá um reembolso único de US$16 do custo para o seu primeiro GB de armazenamento, por um mês.
  {: tip}

O banco de dados PostgreSQL e a instância do {{site.data.keyword.pm_full}} devem ser implementados na mesma conta do {{site.data.keyword.cloud_notm}}.
{: important}

Se você já provisionou os serviços necessários, por exemplo, se tiver concluído o outro tutorial, continue com [Configurar um projeto do Watson Studio](#tadv-setup-ws) abaixo.

## Introduction
{: #tadv-intro}

Nesse tutorial, você irá:

- Oferta de {{site.data.keyword.cloud_notm}} serviços de aprendizado e armazenamento de máquina
- Configurar um projeto do Watson Studio e executar um bloco de notas Python para criar, treinar e implementar um modelo de aprendizado de máquina
- Executar um bloco de notas Python para criar um data mart, configurar monitores de desempenho, de precisão e de justiça e criar dados para monitorar
- Visualizar os resultados na guia {{site.data.keyword.aios_short}} Insights

## Provisionar Serviços do {{site.data.keyword.cloud_notm}}
{: #tadv-svcs}

Efetue login em sua [conta do {{site.data.keyword.cloud_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}){: new_window} com seu IBMid. Ao provisionar serviços, particularmente no caso do Apache Spark, Object Storage e Db2 Warehouse, verifique se sua organização e espaço selecionados são os mesmos para todos os serviços.

### Criar uma conta do Watson Studio
{: #tadv-stac}

- [Crie uma instância do Watson Studio ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/catalog/services/watson-studio){: new_window} se você ainda não tiver uma associada à sua conta:

  ![Watson Studio](images/watson_studio.png)

- Dê ao seu serviço um nome, escolha o plano Lite (grátis) e clique no botão **Criar**.

### Fornecer um serviço de Aprendizado de Máquina
{: #tadv-pml}

- [Provisione uma instância do Watson Machine Learning ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/catalog/services/machine-learning){: new_window} se você ainda não tiver uma associada à sua conta:

  ![Machine Learning](images/machine_learning.png)

- Dê ao seu serviço um nome, escolha o plano Lite (grátis) e clique no botão **Criar**.

- Anote as credenciais de serviço do Machine Learning. Em sua instância de aprendizado de máquina, clique no link **Credenciais de serviço** no lado esquerdo da página. Nomeie a credencial e clique em **Incluir**. Em seguida, na lista de credenciais, clique em **Visualizar credencial** e copie as credenciais para uso posterior.

### Provisão de um serviço Spark
{: #tadv-ps}

- [Provisione um serviço Spark ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/catalog/services/apache-spark){: new_window} se você ainda não tiver um associado à sua conta:

  ![Apache Spark](images/spark.png)

- Designe ao seu serviço um nome, escolha o plano Lite (grátis) e clique no botão **Criar**.

- Anote as credenciais de serviço para sua instância do Spark. Abra sua instância do Spark e clique em **Credenciais de serviço** no menu à esquerda. Clique no botão **Nova credencial**, nomeie suas credenciais e clique em **Incluir**. Em seguida, clique no link **Visualizar credenciais** próximo ao conjunto que você acabou de criar e copie essas credenciais para uso posterior.

### Provisionar um serviço Object Storage
{: #tadv-pos}

- [Provisione um serviço Object Storage ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/catalog/services/cloud-object-storage){: new_window} se você ainda não tiver um associado à sua conta:

  ![Object Storage](images/object_storage.png)

- Dê ao seu serviço um nome, escolha o plano Lite (grátis) e clique no botão **Criar**.

### Fornecer um serviço PostgreSQL pago
{: #tadv-ppgs}

- [Provisione um serviço PostgreSQL pago ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/catalog/services/compose-for-postgresql){: new_window} se você ainda não tiver um associado à sua conta.

  ![Compose for PostgreSQL](images/postgres.png)

- Dê ao seu serviço um nome, escolha o plano Padrão e clique no botão **Criar**.

  Um crédito de $200 do {{site.data.keyword.cloud_notm}} pode ser obtido convertendo para uma conta paga com um cartão de crédito. Se você já tiver uma conta paga, receberá um reembolso único de US$16 do custo para o seu primeiro GB de armazenamento, por um mês.
  {: tip}

- Anote as credenciais de serviço para sua instância do PostgreSQL. Abra sua instância do PostgreSQL existente (ou recém-criada) e clique em **Credenciais de serviço** no menu à esquerda. Clique no botão **Nova credencial**, nomeie suas credenciais e clique em **Incluir**. Em seguida, clique no link **Visualizar credenciais** próximo ao conjunto que você acabou de criar e copie essas credenciais para uso posterior.

<!---

### Provision a Db2 Warehouse service
{: #tadv-pdb2}

- [Provision a Db2 Warehouse service ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/catalog/services/db2-warehouse){: new_window} if you do not already have one associated with your account:

  ![Db2 Warehouse](images/db2_warehouse.png)

- Give your service a name, choose the Entry plan, and click the **Create** button.

- Make note of the service credentials for your Db2 Warehouse instance. Open your existing (or newly-created) Db2 Warehouse instance and click on **Service credentials** in the left-hand menu. Click the **New credential** button, name your credentials, and click **Add**. Then, click the **View credentials** link next to the set you just created, and copy these credentials for later use.

### Upload training and feedback data to Db2 Warehouse
{: #tadv-uptf}

- Download the [car_rental_training_data.csv](https://github.com/watson-developer-cloud/doc-tutorial-downloads/blob/master/ai-openscale/car_rental_training_data.csv){: new_window} file.

- Open your existing (or newly-created) Db2 Warehouse from the [IBM Cloud console ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}){: new_window}, click **Manage** from the left side panel, and then click the green **Open** button.

- If necessary, use your Db2 credentials `username` and `password` to log in to Db2 Warehouse.

- Once Db2 Warehouse has opened, click the **Menu** button and select **Load** from the dropdown:

  ![Load Menu](images/db2_load.png)

- Browse to the training data file, or drag and drop it into the appropriate area on the form. Click **Next**. Select a Schema from the list of load targets; this is usually in a format like `DASH12345`. Then click **New Table** on the right:

  ![New Table](images/new_table.png)

- Name your table CAR\_RENTAL\_TRAINING, and click the **Create** button:

  ![New Table Create](images/new_table_create.png)

- Click **Next** to preview the data. On the preview screen, set the **Separator** field to a semicolon (;) and make sure the **Header in first row** option is checked:

  ![Separator and Header](images/separator.png)

  **NOTE**: By default, the **Detect data types** option is selected.

  ![Data type](images/data-type.png)

  When selected, for columns set with the `VARCHAR` data type, the maximum number of characters allowed for that column is automatically determined by the largest data point uploaded for that column. If you expect that future data for a table column may exceed the automatically-determined maximum, simply unselect the **Detect data types** option, and edit the maximum column value manually.

  ![Configurar o tipo de dados manualmente](images/data-type-manual.png)

- Os dados de treinamento devem agora ser exibidos corretamente em colunas. Clique em **Avançar** para continuar e, em seguida, clique em **Iniciar carregamento** para carregar os dados.

--->

## Configurar um projeto do Watson Studio
{: #tadv-setup-ws}

- Efetue login em sua [conta do Watson Studio ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://dataplatform.ibm.com/){: new_window}. Clique no ícone do avatar da conta no canto superior direito e verifique se a conta que você está usando é a mesma conta usada para criar seus serviços do {{site.data.keyword.cloud_notm}}:

  ![Mesma conta](images/same_account.png)

- No Watson Studio, inicie criando um novo projeto. Selecione "Criar um projeto":

  ![Criação de projeto do Watson Studio](images/studio_create_proj.png)

- Selecione o ladrilho **Padrão** para criar o projeto:

  ![Seleção de projeto Padrão do Watson Studio](images/studio_create_standard.png)

- Dê ao seu projeto um nome e uma descrição, certifique-se de que o serviço Object Storage que você criou na etapa anterior esteja selecionado na lista suspensa **Armazenamento** e clique em **Criar**.

### Associe seus serviços do {{site.data.keyword.cloud_notm}} ao seu projeto do Watson
{: #tadv-acsw}

- Abra seu projeto do Watson Studio e selecione a guia **Configurações**. Na seção **Serviços associados**, clique na lista suspensa **Incluir serviço** e selecione **Watson**:

  ![Incluir Serviço do Watson](images/add_watson_service.png)

- Clique no link **Incluir** no ladrilho **Machine Learning** e selecione a guia **Existente**. Escolha o serviço que você criou na seção anterior na lista suspensa **Instância de serviço existente** e clique em **Selecionar**.

- Na guia de configurações do projeto, selecione **Incluir serviço** novamente e escolha **Spark** na lista suspensa. Na guia **Existente**, escolha o serviço Spark que você criou e clique em **Selecionar**.

## Criar e implementar um modelo de aprendizado de máquina
{: #tadv-deploy-ml}

### Incluir o bloco de notas `CARS4U Action Recommendation - model` em seu projeto do Watson Studio

- Faça download do arquivo a seguir:

    - [CARS4U Action Recommendation - model ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/CARS4U%20action%20recommendation%20-%20model.ipynb){: new_window}

- Na guia **Ativos** em seu projeto do Watson Studio, clique no botão **Incluir no projeto** e selecione **Bloco de notas** na lista suspensa:

  ![Incluir conexão](images/add_notebook.png)

- Selecione **Do arquivo**:

  ![Novo formulário de bloco de notas](images/new_notebook_name.png)

- Em seguida, clique no botão **Escolher arquivo** e selecione o "CARS4U Action Recommendation - model" transferido por download:

  ![Novo formulário de bloco de notas](images/new_notebook_name2.png)

- Na seção **Selecionar tempo de execução**, escolha a instância do Spark que você criou anteriormente na lista suspensa:

  ![Tempo de execução do Spark](images/spark_runtime.png)

- Clique em **Criar bloco de notas**.

### Editar e executar o bloco de notas `CARS4U Action Recommendation - model`
{: #tadv-ern}

O bloco de notas `CARS4U Action Recommendation - model` contém instruções detalhadas para cada etapa no código python que você executará. Conforme você trabalhar no bloco de notas, reserve algum tempo para entender o que cada comando está fazendo.
{: tip}

- Na guia **Ativos** em seu projeto do Watson Studio, clique no ícone **Editar** ao lado do bloco de notas `CARS4U Action Recommendation - model` para editá-lo.

- Na seção 2.2, "Fazer upload de dados no banco de dados PostgreSQL", substitua as credenciais de serviço do Postgres por aquelas criadas na seção anterior.

- Na seção 4, "Armazenar o modelo no repositório", em **DICA**, substitua as credenciais do Watson Machine Learning por aquelas criadas na seção anterior.

- Depois de inserir suas credenciais, seu bloco de notas está pronto para execução. Clique no item de menu **Kernel** e selecione **Reiniciar e executar todos** no menu:

  ![Reiniciar e executar](images/restart_and_run.png)

  Isso criará, treinará e implementará o **CARS4U - Action Recommendation Model** em seu projeto. É possível verificar se o modelo foi implementado selecionando a guia **Implementações** de seu projeto do Watson Studio e clicando no link **CARS4U - Area and Action Model Deployment**.

## Configurar o {{site.data.keyword.aios_short}}
{: #tadv-config-aios}

### Provisão {{site.data.keyword.aios_short}}
{: #tadv-paios}

- Se você ainda não tiver provisionado uma instância do {{site.data.keyword.aios_short}}, clique no link **Catálogo** em sua conta do {{site.data.keyword.cloud_notm}} e filtre no "OpenScale". Selecione o ladrilho para {{site.data.keyword.aios_short}}.

<!---
  ![{{site.data.keyword.aios_short } } ] (images/openscale.png)
--->

- Dê ao seu serviço um nome, selecione o plano Lite e clique em **Criar**.

### Conectar o {{site.data.keyword.aios_short}} ao seu modelo de aprendizado de máquina
{: #tadv-cmlm}

Como o modelo de aprendizado de máquina foi implementado, é possível configurar o {{site.data.keyword.aios_short}} para assegurar confiança e transparência com seus modelos. Selecione a guia **Gerenciar** de sua instância do {{site.data.keyword.aios_short}} e clique no botão **Ativar aplicativo**. A página Introdução do {{site.data.keyword.aios_full}} é aberta; clique em **Iniciar**.

- Selecione o ladrilho "Watson Machine Learning" e clique em **Avançar**.

  ![Configurar instância do WML](images/gs-wml-default.png)

- Selecione sua instância do Watson Machine Learning na lista suspensa e clique em **Avançar**.

  ![Configurar instância do WML](images/gs-set-wml.png)

- Agora você está apto a selecionar quais modelos implementados serão monitorados pelo {{site.data.keyword.aios_short}}. Verifique o modelo que você criou e implementou; clique em **Avançar** para aceitar isso:

  ![Selecionar modelos implementados](images/gs-set-deploy.png)

- Em seguida, é necessário escolher um banco de dados PostgreSQL. Você tem duas opções: o banco de dados do plano Lite grátis ou um banco de dados novo ou existente. Para este tutorial, selecione o ladrilho **Usar banco de dados existente ou comprar um novo**.

    ![Selecionar banco de dados](images/gs-set-lite-db1.png)

  Consulte detalhes mais completos sobre cada uma dessas opções no tópico [Especificando um banco de dados](/docs/services/ai-openscale?topic=ai-openscale-connect-db).
  {: note}

- Depois de ter selecionado a opção "Usar banco de dados existente ou comprar um novo", {{site.data.keyword.aios_short}} verifica a sua conta do {{site.data.keyword.cloud_notm}} para localizar o banco de dados Compose for PostgreSQL existente.

  Selecione o esquema "data_mart" no menu suspenso **Esquema**.

  ![Selecionar banco de dados](images/gs-set-schema1.png)

- Depois de ter selecionado o banco de dados e o esquema, clique em **Avançar** para revisar os dados de resumo e clique em **Salvar**.

  ![Selecionar banco de dados](images/gs-setup-summary3.png)

  Clique em **Sair para o painel** quando solicitado.

## Criar um data mart e configurar monitores de desempenho, precisão e justiça
{: #tadv-config-monitors}

### Incluir o bloco de notas `{{site.data.keyword.aios_short}} e mecanismo Watson ML` em seu projeto do Watson Studio
{: #tadv-aomn}

O bloco de notas `{{site.data.keyword.aios_short}} e mecanismo Watson ML` contém instruções detalhadas para cada etapa no código python que você executará. Conforme você trabalhar no bloco de notas, reserve algum tempo para entender o que cada comando está fazendo.
{: tip}

- Faça download do arquivo a seguir:

    - [{{site.data.keyword.aios_short}} e mecanismo Watson ML ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Watson%20ML%20Engine.ipynb){: new_window}

- Na guia **Ativos** em seu projeto do Watson Studio, clique no botão **Incluir no projeto** e selecione **Bloco de notas** na lista suspensa:

  ![Incluir conexão](images/add_notebook.png)

- Selecione **Do arquivo**:

  ![Novo formulário de bloco de notas](images/new_notebook_name.png)

- Em seguida, clique no botão **Escolher arquivo** e selecione o "{{site.data.keyword.aios_short}} e mecanismo Watson ML" transferido por download:

  ![Novo formulário de bloco de notas](images/new_notebook_name3.png)

- Na seção **Selecionar tempo de execução**, escolha a instância do Spark que você criou anteriormente na lista suspensa:

  ![Tempo de execução do Spark](images/spark_runtime.png)

- Clique em **Criar bloco de notas**.

### Editar e executar o bloco de notas `{{site.data.keyword.aios_short}} e mecanismo Watson ML`
{: #tadv-eromn}

- Na guia **Ativos** em seu projeto do Watson Studio, clique no ícone **Editar** ao lado do bloco de notas `{{site.data.keyword.aios_short}} e mecanismo Watson ML` para editá-lo.

- Na seção 1.1, "Instalação e autenticação":

    - Em **AÇÃO: obter instance_id (GUID) e apikey**, siga as instruções para obter suas credenciais. Substitua `aios_credentials` por sua própria.

    - Em seguida, em **AÇÃO: incluir suas credenciais do Watson Machine Learning aqui**, substitua as credenciais do Watson Machine Learning por aquelas criadas anteriormente.

    - Finalmente, em **AÇÃO: incluir suas credenciais do PostgreSQL aqui**, substitua as credenciais do Postgres por aquelas criadas anteriormente.

- Depois de inserir suas credenciais, seu bloco de notas está pronto para execução. Clique no item de menu **Kernel** e selecione **Reiniciar e executar todos** no menu:

  ![Reiniciar e executar](images/restart_and_run.png)

  Isso configurará seu data mart, ativará a criação de log de carga útil, configurará e pontuará os monitores de desempenho, precisão e justiça e fornecerá essas métricas à sua instância do {{site.data.keyword.aios_short}}.

## Visualizando resultados
{: #tadv-results}

### Visualizar insights para sua implementação
{: #tadv-vide}

Usando o [painel do {{site.data.keyword.aios_short}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window}, clique na guia **Insights**:

  ![Insights](images/insight-dash-tab.png)

A página Insights fornece uma visão geral das métricas para seus modelos implementados. É possível ver facilmente os alertas para as métricas de Justiça ou Precisão que ficaram abaixo do conjunto de limites ao executar o bloco de notas (70%). Os dados e configurações usados neste tutorial terão criado as métricas de Precisão e de Justiça semelhantes às mostradas aqui.

  ![Visão geral do Insight](images/insight-overview-adv-tutorial.png)

### Visualizar dados de monitoramento para sua implementação
{: #tadv-vmdd}

Selecione uma implementação clicando no bloco na página Insights. Os dados de monitoramento para essa implementação aparecerão. Deslize o marcador no gráfico para selecionar dados para o intervalo de tempo durante o qual você executou o bloco de notas. Em seguida, selecione o link **Visualizar detalhes**.

  ![Dados do monitor](images/insight-monitor-data1.png)

Agora, é possível revisar os gráficos para os dados monitorados. Para este exemplo, é possível usar o menu suspenso **Recurso** para selecionar "Filhos" ou "Gênero" para ver detalhes sobre os dados monitorados.

  ![Visão geral do Insight](images/insight-review-charts1.png)

<!---

### Visualizar explicabilidade para uma transação de modelo
{: #tadv-vemt}

Selecione o botão **Visualizar transações** nos gráficos para os dados monitorados.

  ![Visualizar transações](images/view_transactions.png)

  uma lista de transações para a hora passada é listada. Copie um dos IDs de transação.

  ![Lista de transações ] (images/transaction_list.png)

Usando o painel [ { }![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window}, clique na guia **Explicabilidade**:

  ![Explainability ] (images/explainability.png)

Cole o valor do ID de transação copiado na caixa de procura e pressione **Retornar** em seu teclado. Agora você verá uma explicação de como o modelo chegou à sua conclusão, incluindo o quão confiante o modelo foi, os fatores que contribuíram para o nível de confiança e os atributos alimentados para o modelo.

  ![Visualizar Transação ] (images/view_transaction1.png)

--->

## Próximos passos
{: #tadv-next}

- Aprenda mais sobre [como visualizar e interpretar os dados](/docs/services/ai-openscale?topic=ai-openscale-it-ov) e [monitorar a explicabilidade](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).
