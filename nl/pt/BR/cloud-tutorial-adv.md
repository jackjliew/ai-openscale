---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: tutorial, Jupyter notebooks, Watson Studio projects, projects, models, deploy, 

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

# Python SDK Tutorial (Avançado)
{: #crt-ov}

Neste tutorial, você aprenderá a executar as tarefas a seguir:

- Executar um bloco de notas do Python para criar, treinar e implementar um modelo de aprendizado de máquina.
- Criar um data mart, configurar monitores de desempenho, de precisão e de justiça e criar dados para o monitor.
- Visualizar resultados na guia Insights do {{site.data.keyword.aios_short}}.


## Cliente Python
{: #in-pyc}

O [cliente Python do {{site.data.keyword.aios_short}}](http://ai-openscale-python-client.mybluemix.net/){: external} é uma biblioteca Python que permite que você trabalhe diretamente com o serviço {{site.data.keyword.aios_short}} no {{site.data.keyword.cloud_notm}}. É possível usar o cliente Python, em vez da UI do cliente do {{site.data.keyword.aios_short}}, para configurar diretamente um banco de dados de criação de log, ligar seu mecanismo de aprendizado de máquina e selecionar e monitorar implementações. Para obter exemplos do uso do cliente Python dessa maneira, consulte os [Blocos de notas de amostra do {{site.data.keyword.aios_short}}](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks){: external}.

## Cenário
{: #crt-scenario}

Os concessores tradicionais estão sob pressão para expandir seu portfólio digital de serviços financeiros para um público maior e mais diversificado, o que requer uma nova abordagem da modelagem de risco de crédito. Suas equipes de ciência de dados dependem atualmente de técnicas de modelagem padrão - como árvores de decisão e regressão logística - que funcionam bem para conjuntos de dados moderados e fazem recomendações que podem ser facilmente explicadas. Isso satisfaz os requisitos regulamentares de que as decisões de concessão de crédito devem ser transparentes e explicáveis.

Para fornecer acesso ao crédito para uma população mais ampla e mais arriscada, os históricos de crédito do requerente devem se expandir além do crédito tradicional, como hipotecas e empréstimos de carro, para fontes de crédito alternativo, como históricos de pagamento de serviços de utilidade e de plano telefônico móvel, além educação e cargos. Essas novas fontes de dados oferecem uma promessa, mas também apresentam riscos aumentando a probabilidade de correlações inesperadas que introduzem propensão com base na idade, sexo ou outras características pessoais de um requerente.

As técnicas de ciência de dados mais adequadas a esses diferentes conjuntos de dados, como as árvores impulsionadas por gradiente e as redes neurais, podem gerar modelos de risco altamente precisos, mas a um custo. Esses modelos de "caixa preta" geram predições opacas que devem de alguma forma se tornar transparentes, para garantir a aprovação regulamentar, como o artigo 22 do Regulamento Geral sobre a Proteção de Dados (GDPR) ou o Fair Credit Reporting Act (FCRA) federal gerenciado pelo Departamento de Proteção Financeira do Consumidor.

O modelo de risco de crédito fornecido neste tutorial usa um conjunto de dados de treinamento que contém 20 atributos sobre cada requerente de empréstimo. Dois desses atributos - idade e sexo - podem ser testados para propensão. Para este tutorial, o foco será a propensão com relação a sexo e idade. Para
obter mais informações sobre os dados de treinamento, veja [Por que o {{site.data.keyword.aios_short}} precisa de acesso aos meus dados de treinamento?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)

O {{site.data.keyword.aios_short}} monitorará a propensão do modelo implementado para um resultado favorável ("Sem risco") para um grupo (o Grupo de referência) sobre outro (o Grupo monitorado). Neste tutorial, o Grupo monitorado para sexo é `female`, enquanto o Grupo monitorado para idade é `18 to 25`.

## pré-requisitos
{: #crt-prereqs}

Este tutorial usa um bloco de notas Jupyter que deve ser executado em um projeto do Watson Studio, usando um ambiente de tempo de execução "Python 3.5 com Spark". Isso requer credenciais de serviço para os serviços do {{site.data.keyword.cloud_notm}} a seguir:

- Cloud Object Storage (para armazenar seu projeto do {{site.data.keyword.DSX}})
- {{site.data.keyword.aios_short}}
- {{site.data.keyword.pm_full}}
- (Opcional) Bancos de dados para PostgreSQL ou Db2 Warehouse

O bloco de notas Jupyter treinará, criará e implementará um modelo de Risco de crédito alemão, configurará o {{site.data.keyword.aios_short}} para monitorar essa implementação e fornecerá sete dias de registros históricos e medidas para visualização no painel do {{site.data.keyword.aios_short}} Insights. Também é possível configurar opcionalmente o modelo para aprendizado contínuo com o Watson Studio e o Spark.

## Introduction
{: #crt-intro}

Neste tutorial, você executará as tarefas a seguir:

- [Provisionar os serviços de aprendizado de máquina e de armazenamento do {{site.data.keyword.cloud_notm}}](/docs/services/ai-openscale?topic=ai-openscale-crt-ov#crt-services).
- [Configurar um projeto do Watson Studio e executar um bloco de notas Python para criar, treinar e implementar um modelo de aprendizado de máquina](/docs/services/ai-openscale?topic=ai-openscale-crt-ov#crt-set-wstudio).
- [Provisionar o {{site.data.keyword.aios_short}}](/docs/services/ai-openscale?topic=ai-openscale-crt-ov#crt-wos-adv).
- [Executar um bloco de notas Python para criar um data mart, configurar os monitores de desempenho, de precisão e de justiça e criar dados a serem monitorados](/docs/services/ai-openscale?topic=ai-openscale-crt-ov#crt-edit-notebook).
- [Visualizar os resultados na guia Insights do {{site.data.keyword.aios_short}}](/docs/services/ai-openscale?topic=ai-openscale-crt-ov#crt-view-results).

## Provisionar Serviços do {{site.data.keyword.cloud_notm}}
{: #crt-services}

Efetue login em sua [conta do {{site.data.keyword.cloud_notm}}](https://{DomainName}){: external} com seu {{site.data.keyword.ibmid}}. Ao provisionar
serviços, particularmente se você usar o Db2 Warehouse, verifique se sua organização e espaço selecionados
são os mesmos para todos os serviços.

### Criar uma conta do {{site.data.keyword.DSX}}
{: #crt-wstudio}

- [Crie uma instância do {{site.data.keyword.DSX}}](https://{DomainName}/catalog/services/watson-studio){: external} se você ainda não tiver uma associada à sua conta:

  ![O bloco do Watson Studio é exibido](images/watson_studio.png)

- Dê ao seu serviço um nome, escolha o plano Lite (grátis) e clique no botão **Criar**.

### Provisione um serviço {{site.data.keyword.cos_full_notm}}
{: #crt-cos}

- [Provisione um serviço do {{site.data.keyword.cos_short}}](https://{DomainName}/catalog/services/cloud-object-storage){: external} se você ainda não tiver um associado à sua conta:

  ![O bloco do Object Storage é exibido](images/object_storage.png)

- Dê ao seu serviço um nome, escolha o plano Lite (grátis) e clique no botão **Criar**.

### Provisione um serviço {{site.data.keyword.pm_full}}
{: #crt-wml}

- [Provisione uma instância do {{site.data.keyword.pm_short}}](https://{DomainName}/catalog/services/machine-learning){: external} se você ainda não tiver uma associada à sua conta:

  ![O bloco do Machine Learning é exibido](images/machine_learning.png)

- Dê ao seu serviço um nome, escolha o plano Lite (grátis) e clique no botão **Criar**.

### Provisione um serviço {{site.data.keyword.aios_full}}
{: #crt-wos-adv}

Se você ainda não tiver feito isso, assegure-se de provisionar o {{site.data.keyword.aios_full}}. 

- [Provisione uma instância do {{site.data.keyword.aios_short}}](https://{DomainName}/catalog/services/watson-openscale){: external} se você ainda não tiver uma associada à sua conta:

  ![O bloco do {{site.data.keyword.aios_short}} é exibido](images/wos-cloud-tile.png)

1. Clique em **Catálogo** > **IA** > **{{site.data.keyword.aios_short}}**.
2. Dê um nome ao seu serviço, escolha um plano e clique no botão **Criar**.
3. Para iniciar o {{site.data.keyword.aios_short}}, clique no botão **Introdução**.

### (Opcional) Provisionar um serviço Databases for PostgreSQL ou DB2 Warehouse
{: #crt-db2}

Se você tiver uma conta {{site.data.keyword.cloud_notm}} paga, poderá provisionar um
serviço `Databases for PostgreSQL` ou `Db2 Warehouse` para aproveitar totalmente a integração com o {{site.data.keyword.DSX}} e serviços de aprendizado contínuo. Se você escolher não provisionar um serviço pago, será possível usar o armazenamento PostgreSQL interno grátis com o {{site.data.keyword.aios_short}}, mas não será possível configurar o aprendizado contínuo para seu modelo.

- [Provisione um serviço Databases for PostgreSQL](https://{DomainName}/catalog/services/databases-for-postgresql){: external} ou [um serviço Db2 Warehouse](https://{DomainName}/catalog/services/db2-warehouse){: external} se você ainda não tiver um associado à sua conta:

  ![O bloco do DB for Postgres é exibido](images/dbpostgres.png)

  ![O bloco do Db2 Warehouse é exibido](images/db2_warehouse.png)

- Dê ao seu serviço um nome, escolha o plano Padrão (Databases for PostgreSQL) ou plano de Entrada (Db2 Warehouse) e clique no botão **Criar**.

## Configurar um projeto {{site.data.keyword.DSX}}
{: #crt-set-wstudio}

- Efetue login em sua [conta do {{site.data.keyword.DSX}}](https://dataplatform.ibm.com/){: external}. Clique em {{site.data.keyword.avatar}} e verifique se a conta que você está usando é a mesma que usou para criar seus serviços {{site.data.keyword.cloud_notm}}:

  ![Mesma conta](images/same_account.png)

- No {{site.data.keyword.DSX}}, inicie criando um novo projeto. Selecione "Criar um projeto":

  ![Criar projeto do Watson Studio](images/studio_create_proj.png)

- Selecione o ladrilho **Padrão** para criar o projeto:

  ![O bloco Selecionar projeto Standard do Watson Studio é exibido](images/studio_create_standard.png)

- Dê ao seu projeto um nome e uma descrição, certifique-se de que o serviço Cloud Object Storage que você criou esteja selecionado na lista suspensa **Armazenamento** e clique em **Criar**.

## Criar e implementar um modelo {{site.data.keyword.pm_short}}
{: #crt-make-model}

### Inclua o bloco de notas `Working with Watson Machine Learning` em seu
projeto {{site.data.keyword.DSX}}
{: #crt-add-notebook}

- Acesse o arquivo a seguir. Se tiver uma conta do GitHub, será possível conectar-se para clonar o arquivo e fazer download dele. Caso contrário, é possível visualizar a versão bruta clicando no botão **Bruto** e copiar o texto do arquivo em um novo arquivo com uma extensão .ipynb.

    - [Trabalhando com o Watson Machine Learning](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine.ipynb){: external}

- Na guia **Recursos** em seu projeto {{site.data.keyword.DSX}},
clique no botão **Incluir no projeto** e selecione **Bloco de notas**
na lista suspensa:

  ![o bloco em destaque Escolher um tipo de ativo com um bloco de notas é exibido](images/add_notebook.png)

- Selecione **Do arquivo**:

  ![Formulário de notebook novo](images/new_notebook_name.png)

- Em seguida, clique no botão **Escolher arquivo** e selecione o arquivo do bloco de notas "german_credit_lab.ipynb" transferido por download:

  ![Formulário de notebook novo](images/new_notebook_name2a.png)

- Na seção **Selecionar tempo de execução**, escolha o Python mais recente com a opção do Spark:

- Clique em  ** Criar Notebook **.

### Editar e executar o bloco de notas `Working with Watson Machine Learning`
{: #crt-edit-notebook}

O bloco de notas `Working with Watson Machine Learning` contém instruções detalhadas para cada etapa no código Python que você executará. Conforme você trabalhar no bloco de notas, reserve algum tempo para entender o que cada comando está fazendo.
{: tip}

- Na guia **Ativos** em seu projeto do Watson Studio, clique no ícone **Editar** ao lado do bloco de notas `Working with Watson Machine Learning` para editá-lo.

- Na seção "Provisionar serviços e configurar credenciais", faça as mudanças a seguir:

    - Siga as instruções do bloco de notas para criar, copiar e colar uma chave de API do {{site.data.keyword.cloud_notm}}.

    - Substitua as credenciais de serviço do {{site.data.keyword.pm_full}} por aquelas que você criou anteriormente.

    - Substitua as credenciais do DB pelas que você criou para o Databases for PostgreSQL.

    - Se você configurou anteriormente o {{site.data.keyword.aios_short}} para usar um banco de dados PostgreSQL interno grátis como seu data mart, é possível alternar para um novo data mart que use seu serviço Databases for PostgreSQL. Para excluir a configuração antiga do PostgreSQL e criar uma nova, configure a variável KEEP_MY_INTERNAL_POSTGRES como `False`.

        O bloco de notas removerá seu data mart interno do PostgreSQL existente e criará um novo data mart com as credenciais do DB fornecidas. **Nenhuma migração de dados ocorrerá**.
        {: important}

- Depois de provisionar seus serviços e inserir suas credenciais, seu bloco de notas está pronto para execução. Clique no item de menu **Kernel** e selecione **Reiniciar e limpar saída** no menu:

  ![Reiniciar e limpar](images/restart_and_clear.png)

- Agora, execute cada etapa do bloco de notas em sequência. Observe o que está acontecendo em cada etapa, conforme descrito. Conclua todas as etapas, incluindo as etapas na seção "Dados adicionais para ajudar a depuração".

O resultado líquido é que você terá criado, treinado e implementado o modelo **Implementação de risco alemão do Spark** em sua instância de serviço do {{site.data.keyword.aios_short}}. O {{site.data.keyword.aios_short}} será configurado para verificar o modelo para propensão com relação a sexo (neste caso, Feminino) ou idade (neste caso, 18-25 anos).

## Visualização de resultados
{: #crt-view-results}

### Visualizar insights para sua implementação
{: #crt-view-insights}

Usando o [painel do {{site.data.keyword.aios_short}}](https://aiopenscale.cloud.ibm.com/aiopenscale/){: external}, clique na guia **Insights**:

  ![O ícone Insights é exibido](images/insight-dash-tab.png)

A página Insights fornece uma Visão geral das métricas para seus modelos implementados. É possível ver facilmente os alertas para as métricas de Justiça e Precisão que excedem o conjunto de limites ao executar o bloco de notas. Os dados e configurações usados neste tutorial terão criado as métricas de Precisão e de Justiça semelhantes às mostradas aqui.

  ![O painel de visão geral de insight é exibido com um bloco para o modelo alemão de risco de crédito](images/insight-overview-adv-tutorial-2.png)

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

  ![Visualizar transações](images/view_transactions.png)

  Uma lista de transações em que a implementação agiu de maneira propensa aparece. 
  
2. Selecione uma das transações e, na coluna **AÇÃO**, clique no link **Explicar**.

  ![Transaction list](images/transaction_list_cr.png)

Agora você verá uma explicação de como o modelo chegou à sua conclusão, incluindo o quão confiante o modelo foi, os fatores que contribuíram para o nível de confiança e os atributos alimentados para o modelo.

  ![View Transaction](images/view_transaction_cr.png)
  
## Próximos passos
{: #crt-next-steps}

- Aprenda mais sobre [como visualizar e interpretar os dados](/docs/services/ai-openscale?topic=ai-openscale-it-ov) e [monitorar a explicabilidade](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).
