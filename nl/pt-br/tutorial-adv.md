---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-11"

keywords: tutorial, Jupyter notebooks, Watson Studio projects, projects, models, deploy, 

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
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Python SDK Tutorial (Avançado)
{: #crt-ov}

## Cenário
{: #crt-scenario}

Os concessores tradicionais estão sob pressão para expandir seu portfólio digital de serviços financeiros para um público maior e mais diversificado, o que requer uma nova abordagem da modelagem de risco de crédito. Suas equipes de ciência de dados dependem atualmente de técnicas de modelagem padrão - como árvores de decisão e regressão logística - que funcionam bem para conjuntos de dados moderados e fazem recomendações que podem ser facilmente explicadas. Isso satisfaz os requisitos regulamentares de que as decisões de concessão de crédito devem ser transparentes e explicáveis.

Para fornecer acesso ao crédito para uma população mais ampla e mais arriscada, os históricos de crédito do requerente devem se expandir além do crédito tradicional, como hipotecas e empréstimos de carro, para fontes de crédito alternativo, como históricos de pagamento de serviços de utilidade e de plano telefônico móvel, além educação e cargos. Essas novas fontes de dados oferecem uma promessa, mas também apresentam riscos aumentando a probabilidade de correlações inesperadas que introduzem propensão com base na idade, sexo ou outras características pessoais de um requerente.

As técnicas de ciência de dados mais adequadas a esses diferentes conjuntos de dados, como as árvores impulsionadas por gradiente e as redes neurais, podem gerar modelos de risco altamente precisos, mas a um custo. Esses modelos de "caixa preta" geram predições opacas que devem de alguma forma se tornar transparentes, para garantir a aprovação regulamentar, como o artigo 22 do Regulamento Geral sobre a Proteção de Dados (GDPR) ou o Fair Credit Reporting Act (FCRA) federal gerenciado pelo Departamento de Proteção Financeira do Consumidor.

O modelo de risco de crédito fornecido neste tutorial usa um conjunto de dados de treinamento que contém 20 atributos sobre cada requerente de empréstimo. Dois desses atributos - idade e sexo - podem ser testados para propensão. Para este tutorial, o foco será a propensão com relação a sexo e idade.

O {{site.data.keyword.aios_short}} monitorará a propensão do modelo implementado para um resultado favorável ("Sem risco") para um grupo (o Grupo de referência) sobre outro (o Grupo monitorado). Neste tutorial, o Grupo monitorado para sexo é `female`, enquanto o Grupo monitorado para idade é `18 to 25`.

## pré-requisitos
{: #crt-prereqs}

Este tutorial usa um bloco de notas Jupyter que deve ser executado em um projeto do Watson Studio, usando um ambiente de tempo de execução "Python 3.5 com Spark". Isso requer credenciais de serviço para os serviços do {{site.data.keyword.cloud_notm}} a seguir:

- Cloud Object Storage (para armazenar o projeto do Watson Studio)
- {{site.data.keyword.aios_short}}
- Watson Machine Learning
- (Opcional) Bancos de dados para PostgreSQL ou Db2 Warehouse

O bloco de notas Jupyter treinará, criará e implementará um modelo de Risco de crédito alemão, configurará o {{site.data.keyword.aios_short}} para monitorar essa implementação e fornecerá sete dias de registros históricos e medidas para visualização no painel do {{site.data.keyword.aios_short}} Insights. Também é possível configurar opcionalmente o modelo para aprendizado contínuo com o Watson Studio e o Spark.

## Introduction
{: #crt-intro}

Nesse tutorial, você irá:

- Oferta de {{site.data.keyword.cloud_notm}} serviços de aprendizado e armazenamento de máquina
- Configurar um projeto do Watson Studio e executar um bloco de notas Python para criar, treinar e implementar um modelo de aprendizado de máquina
- Executar um bloco de notas Python para criar um data mart, configurar monitores de desempenho, de precisão e de justiça e criar dados para monitorar
- Visualizar os resultados na guia {{site.data.keyword.aios_short}} Insights

## Provisionar Serviços do {{site.data.keyword.cloud_notm}}
{: #crt-services}

Efetue login em sua [conta do {{site.data.keyword.cloud_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}){: new_window} com seu IBMid. Ao provisionar serviços, particularmente no caso do Db2 Warehouse, verifique se sua organização e espaço selecionados são os mesmos para todos os serviços.

### Criar uma conta do Watson Studio
{: #crt-wstudio}

- [Crie uma instância do Watson Studio ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/catalog/services/watson-studio){: new_window} se você ainda não tiver uma associada à sua conta:

  ![Watson Studio](images/watson_studio.png)

- Dê ao seu serviço um nome, escolha o plano Lite (grátis) e clique no botão **Criar**.

### Provisão de um serviço Cloud Object Storage
{: #crt-cos}

- [Provisione um serviço Object Storage ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/catalog/services/cloud-object-storage){: new_window} se você ainda não tiver um associado à sua conta:

  ![Object Storage](images/object_storage.png)

- Dê ao seu serviço um nome, escolha o plano Lite (grátis) e clique no botão **Criar**.

### Oferta um serviço Watson Machine Learning
{: #crt-wml}

- [Provisione uma instância do Watson Machine Learning ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/catalog/services/machine-learning){: new_window} se você ainda não tiver uma associada à sua conta:

  ![Machine Learning](images/machine_learning.png)

- Dê ao seu serviço um nome, escolha o plano Lite (grátis) e clique no botão **Criar**.

### (Opcional) Provisionar um serviço Databases for PostgreSQL ou DB2 Warehouse
{: #crt-db2}

Se você tiver uma conta paga do {{site.data.keyword.cloud_notm}}, poderá provisionar um serviço `Databases for PostgreSQL` ou `Db2 Warehouse` para tirar total proveito da integração com o Watson Studio e serviços de aprendizado contínuo. Se você escolher não provisionar um serviço pago, será possível usar o armazenamento PostgreSQL interno grátis com o {{site.data.keyword.aios_short}}, mas não será possível configurar o aprendizado contínuo para seu modelo.

- [Provisione um serviço Databases for PostgreSQL ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/catalog/services/databases-for-postgresql) ou [um serviço Db2 Warehouse ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/catalog/services/db2-warehouse) se você ainda não tiver um associado à sua conta:

  ![DB for Postgres](images/dbpostgres.png)

  ![Db2 Warehouse](images/db2_warehouse.png)

- Dê ao seu serviço um nome, escolha o plano Padrão (Databases for PostgreSQL) ou plano de Entrada (Db2 Warehouse) e clique no botão **Criar**.

## Configurar um projeto do Watson Studio
{: #crt-set-wstudio}

- Efetue login em sua [conta do Watson Studio ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://dataplatform.ibm.com/){: new_window}. Clique no ícone do avatar da conta no canto superior direito e verifique se a conta que você está usando é a mesma conta usada para criar seus serviços do {{site.data.keyword.cloud_notm}}:

  ![Same Account](images/same_account.png)

- No Watson Studio, inicie criando um novo projeto. Selecione "Criar um projeto":

  ![Watson Studio create project](images/studio_create_proj.png)

- Selecione o ladrilho **Padrão** para criar o projeto:

  ![Watson Studio select Standard project](images/studio_create_standard.png)

- Dê ao seu projeto um nome e uma descrição, certifique-se de que o serviço Cloud Object Storage que você criou esteja selecionado na lista suspensa **Armazenamento** e clique em **Criar**.

## Criar e implementar um modelo de aprendizado de máquina
{: #crt-make-model}

### Incluir o bloco de notas `Working with Watson Machine Learning` em seu projeto do Watson Studio
{: #crt-add-notebook}

- Faça download do seguinte arquivo:

    - [Working with Watson Machine Learning ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine.ipynb){: new_window}

- Na guia **Ativos** em seu projeto do Watson Studio, clique no botão **Incluir no projeto** e selecione **Bloco de notas** na lista suspensa:

  ![Add Connection](images/add_notebook.png)

- Selecione **Do arquivo**:

  ![New Notebook Form](images/new_notebook_name.png)

- Em seguida, clique no botão **Escolher arquivo** e selecione o arquivo do bloco de notas "german_credit_lab.ipynb" transferido por download:

  ![New Notebook Form](images/new_notebook_name2a.png)

- Na seção **Selecionar tempo de execução**, escolha uma opção Python 3.5 com Spark:

- Clique em  ** Criar Notebook **.

### Editar e executar o bloco de notas `Working with Watson Machine Learning`
{: #crt-edit-notebook}

O bloco de notas `Working with Watson Machine Learning` contém instruções detalhadas para cada etapa no código Python que você executará. Conforme você trabalhar no bloco de notas, reserve algum tempo para entender o que cada comando está fazendo.
{: tip}

- Na guia **Ativos** em seu projeto do Watson Studio, clique no ícone **Editar** ao lado do bloco de notas `Working with Watson Machine Learning` para editá-lo.

- Na seção "Provisionar serviços e configurar credenciais", faça as mudanças a seguir:

    - Siga as instruções para criar, copiar e colar uma chave de API do {{site.data.keyword.cloud_notm}}.

    - Substitua as credenciais de serviço do Watson Machine Learning (WML) pelas que você criou anteriormente.

    - Substitua as credenciais do DB pelas que você criou para o Databases for PostgreSQL.

    - Se você configurou anteriormente o {{site.data.keyword.aios_short}} para usar um banco de dados PostgreSQL interno grátis como seu data mart, é possível alternar para um novo data mart que use seu serviço Databases for PostgreSQL. Para excluir a configuração antiga do PostgreSQL e criar uma nova, configure a variável KEEP_MY_INTERNAL_POSTGRES como `False`.

        O bloco de notas removerá seu data mart interno do PostgreSQL existente e criará um novo data mart com as credenciais do DB fornecidas. **Nenhuma migração de dados ocorrerá**.
        {: important}

- Depois de provisionar seus serviços e inserir suas credenciais, seu bloco de notas está pronto para execução. Clique no item de menu **Kernel** e selecione **Reiniciar e limpar saída** no menu:

  ![Restart and Clear](images/restart_and_clear.png)

- Agora, execute cada etapa do bloco de notas em sequência. Observe o que está acontecendo em cada etapa, conforme descrito. Conclua todas as etapas, incluindo as etapas na seção "Dados adicionais para ajudar a depuração".

O resultado líquido é que você terá criado, treinado e implementado o modelo **Implementação de risco alemão do Spark** em sua instância de serviço do {{site.data.keyword.aios_short}}. O {{site.data.keyword.aios_short}} será configurado para verificar o modelo para propensão com relação a sexo (neste caso, Feminino) ou idade (neste caso, 18-25 anos).

## Visualização de resultados
{: #crt-view-results}

### Visualizar insights para sua implementação
{: #crt-view-insights}

Usando o [painel do {{site.data.keyword.aios_short}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window}, clique na guia **Insights**:

  ![Insights](images/insight-dash-tab.png)

A página Insights fornece uma visão geral das métricas para seus modelos implementados. É possível ver facilmente os alertas para as métricas de Justiça ou Precisão que ficaram abaixo do conjunto de limites ao executar o bloco de notas. Os dados e configurações usados neste tutorial terão criado as métricas de Precisão e de Justiça semelhantes às mostradas aqui.

  ![Insight overview](images/insight-overview-adv-tutorial-2.png)

### Visualizar dados de monitoramento para sua implementação
{: #crt-view-mon-data}

1. Para visualizar detalhes de monitoramento, na página **Insights**, clique no ladrilho que corresponde à implementação. Os dados de monitoramento para essa implementação aparecem. 
2. Deslize o marcador no gráfico para selecionar dados para uma janela específica de uma hora. 
3. Clique no link **Visualizar Detalhes** .

  ![Monitor data](images/insight-monitor-data2.png)

Agora, é possível revisar os gráficos para os dados monitorados. Para este exemplo, é possível ver que, para o recurso "Sexo", o grupo `female` recebeu o resultado favorável "Sem risco" menor (68%) do que o grupo `male` (78%).

  ![Insight overview](images/insight-review-charts2.png)

### Visualizar explicabilidade para uma transação de modelo
{: #crt-view-explain}

Para cada implementação, é possível ver dados de explicabilidade para transações específicas.

Se você já souber qual transação deseja visualizar, há uma maneira rápida de consultar isso com o ID de transação. Depois de clicar no ladrilho de implementação, no navegador, clique no ícone **Explicar uma transação**![guia Explicar uma transação](images/insight-transact-tab.png), digite o ID de transação e pressione **Enter**.
{: tip}

Se você usar a versão Lite interna do PostgreSQL, talvez não seja possível recuperar suas credenciais do banco de dados. Isso pode impedir que você veja transações.
{: note}

1. Nos gráficos para os dados propensos mais recentes, clique no botão **Visualizar transações**.

  ![View transactions](images/view_transactions.png)

  Uma lista de transações em que a implementação agiu de maneira propensa aparece. 
  
2. Selecione uma das transações e, na coluna **AÇÃO**, clique no link **Explicar**.

  ![Transaction list](images/transaction_list_cr.png)

Agora você verá uma explicação de como o modelo chegou à sua conclusão, incluindo o quão confiante o modelo foi, os fatores que contribuíram para o nível de confiança e os atributos alimentados para o modelo.

  ![View Transaction](images/view_transaction_cr.png)
  
## Próximos passos
{: #crt-next-steps}

- Aprenda mais sobre [como visualizar e interpretar os dados](/docs/services/ai-openscale?topic=ai-openscale-it-ov) e [monitorar a explicabilidade](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).
