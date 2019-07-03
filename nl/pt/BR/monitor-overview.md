---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: deployment, monitors, data

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

# Preparando Monitores para uma Implementação
{: #mo-config}

Configure e ative os monitores para cada implementação que você está rastreando com o {{site.data.keyword.aios_short}}.
{: shortdesc}

## e Segurança
{: #io-conf}

A guia **Configuração** (![Guia Configuração](images/insight-config-tab.png)) abre um Resumo de configuração para a implementação selecionada.

  ![Config summary](images/insight-config-summary.png)

Daqui, é possível editar diretamente as definições de configuração para seu monitor de implementação.

## Selecionando uma implementação
{: #mo-select-deploy}

1.  Primeiro, você deve selecionar uma implementação.

    1. Clique no botão **Incluir implementações**. Aparecerá uma lista de implementações de modelo disponíveis.
    2. Clique em uma implementação de modelo e, em seguida, clique em **Configurar**.

    Se houver múltiplas implementações para um determinado modelo, ao configurar uma implementação, todas as outras implementações para o mesmo modelo também serão configuradas.
    {: note}

    ![Select deployment page](images/config-select-deploy.png)

1.  Clique no botão **Configurar monitores**.

    ![Preparar-se para o monitoramento](images/config-prep-monitor.png)

## Fornecer detalhes de criação de log de carga útil
{: #mo-work-data}

Deve-se fornecer informações sobre seu modelo e dados de treinamento. Para
obter mais informações sobre os dados de treinamento, veja [Por que o {{site.data.keyword.aios_short}} precisa de acesso aos meus dados de treinamento?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)

![Preparar explicação](images/config-what-monitor.png)

- Se você usar uma instância do {{site.data.keyword.pm_full}} que esteja na mesma região que sua instância do {{site.data.keyword.aios_short}}, suas informações de criação de log de carga útil serão configuradas automaticamente para você.
- Caso contrário, na guia e janelas **Criação de log de carga útil**, deve-se inserir informações sobre os tipos de dados e de algoritmo e sua criação de log de carga útil. 

   Há requisitos específicos, dependendo de suas seleções. Para obter mais informações, consulte [Dados numéricos/categóricos](https://test.cloud.ibm.com/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mo-config#mo-datan).

   Antes de ser possível configurar seus monitores, é necessário copiar um dos fragmentos de código a serem executados. Execute o comando cURL em seu aplicativo cliente ou o comando Python em seu bloco de notas de ciência de dados. Isso fornece uma maneira de registrar solicitações de implementação de modelo e gravar dados de resposta no banco de dados de carga útil.

## Fornecer detalhes do modelo
{: #mo-work-model-dets}

Forneça informações sobre seu modelo para que o {{site.data.keyword.aios_short}} possa acessar o banco de dados e entender como o modelo está configurado.

Especificamente para configurar monitores, deve-se executar as tarefas a seguir:

1. Especifique o local dos dados de treinamento. Isso é feito inserindo o local, o nome do host ou o endereço IP, o nome do banco de dados e as informações sobre autenticação.
2. No banco de dados, deve-se selecionar a tabela de treinamento selecionando o esquema e a tabela.
3. Selecione a coluna do rótulo na tabela de treinamento.
4. Selecione os recursos que foram usados para treinar a implementação de IA.
5. Selecione o texto e os recursos categóricos.
6. Selecione a coluna de predição de implementação.
7. Finalmente, é possível revisar os detalhes de seu modelo antes de salvá-lo.

As seções a seguir fornecem algumas informações específicas que você encontra dependendo do tipo de modelo, [Dados numéricos/categóricos](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mo-config#mo-datan) ou [Imagens e texto não estruturado](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mo-config#mo-datai).


### Dados numéricos / categóricos
{: #mo-nuca}

Para dados numéricos ou categóricos, é necessário fornecer informações sobre os dados de treinamento para seu modelo, a fim de configurar os monitores.

- **Configurar monitores manualmente** - requer que você forneça informações de conexão para seus dados de treinamento.

    - Selecione o [tipo de algoritmo](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-understand) e clique em **Avançar**:

      O formato dos dados de treinamento deve corresponder ao modelo. Por exemplo, se o modelo espera `M` e `F` para o recurso `Gender`, os dados de treinamento devem ter `M` e `F`, não `Male` e `Female`. A liberação atual do {{site.data.keyword.aios_short}} suporta apenas os locais de banco de dados Db2 ou Cloud Object Storage.
        {: important}

    - Especifique o Local (`Db2` ou `Cloud Object Storage`), em seguida:

        - Para um banco de dados Db2, insira as informações a seguir:

            - Nome do host ou Endereço IP
            - Port
            - Banco de dados (nome)
            - Nome de usuário
            - Senha

        - Para o Cloud Object Storage, insira as informações a seguir:

            - URL de login: a URL de login deve corresponder à configuração de região do depósito no qual os dados de treinamento estão localizados. Você especificará o depósito de dados de treinamento na próxima etapa.
            - Instância de recurso (ID)
            - chave de API

    - Para assegurar uma conexão válida, clique no botão **Testar** para se conectar aos dados de treinamento.
    - Especifique o local exato no banco de dados Db2 ou no Cloud Object Storage em que os dados de treinamento estão localizados.

        - Para um banco de dados Db2, selecione um esquema e uma tabela de treinamento que inclua colunas esperadas por seu modelo.
        - Para o Cloud Object Storage, selecione um Depósito e um Conjunto de dados.

- **Fazer upload de um arquivo de configuração** - escolha essa opção se preferir manter seus dados de treinamento privados. É possível usar um bloco de notas Python customizado para fornecer ao {{site.data.keyword.aios_short}} informações para analisar seus dados de treinamento sem fornecer acesso aos dados de treinamento em si.

  A execução do bloco de notas Python permite capturar valores distintos nas colunas do esquema, assim como os nomes de colunas. Além disso, é possível usar o bloco de notas para pré-configurar o monitor de Justiça.

   - Faça download do [bloco de notas customizado](https://github.com/IBM-Watson/aios-data-distribution/blob/master/training_statistics_notebook.ipynb){: external} e substitua quaisquer credenciais por suas próprias credenciais.
   - Revise cuidadosamente o bloco de notas, especificando dados para seu modelo onde apropriado. Salve o bloco de notas.
   - Execute o bloco de notas para gerar um arquivo de configuração formatado por JSON.
   - Faça upload do arquivo de configuração JSON.

     ![Upload config JSON](images/config-json-monitor.png)

- O {{site.data.keyword.aios_short}} localiza seus dados de treinamento nos metadados armazenados com o modelo no {{site.data.keyword.pm_full}}. Escolha a coluna do rótulo nos dados de treinamento que contêm seus valores de predição.
- Selecione as colunas usadas para treinar o modelo - estes são os recursos que sua implementação de modelo espera em uma solicitação.
- Finalmente, selecione as colunas que continham texto e foram convertidas em números inteiros. Por exemplo, se os dados de treinamento originais contiverem `Male` e `Female` para `Gênero` e eles tiverem sido mapeados para `0` e `1` respectivamente, os dados de treinamento agora conterão os valores `0` e `1` para a coluna `Gênero`. Identifique essas colunas que agora contêm números inteiros, mas originalmente continham valores de texto.

### Imagens e Texto Não Estruturado
{: #mo-imun}

- **Imagens**

  Para modelos que aceitam imagens como entrada, a imagem precisa ser representada como um formato (altura) x (largura) x (# canais), em que cada ponto representa valores monocromáticos ou RGB para cada pixel.

- **Texto sem estrutura**

   Para modelos que aceitam texto como entrada, espera-se que o modelo aceite o texto inteiro, e não uma representação vetorizada do texto.

## Revisar e Salvar Configuração
{: #mo-save}

Revise o resumo da seleção e clique em **Salvar** para continuar.

  ![Select data table](images/config-summary-monitor.png)

### Próximos passos
{: #mo-next}

Para iniciar a configuração de monitores, clique na guia **Precisão** e depois em **Iniciar**.
