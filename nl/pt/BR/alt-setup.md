---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: Python, install, python module, setup, set up, insights, explainability

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

# Instalando um módulo Python para configurar o {{site.data.keyword.aios_short}}
{: #as-module}

Para automatizar o fornecimento e a configuração dos serviços necessários do {{site.data.keyword.cloud_notm}} e ver um aplicativo {{site.data.keyword.aios_full}}, incluindo dados de amostra, é possível instalar um módulo Python.
{: shortdesc}

## Sobre este Módulo
{: #as-about}

- O módulo fornece uma maneira alternativa para que os usuários técnicos vejam uma instância do {{site.data.keyword.aios_short}} em execução sem que precisem provisionar e configurar os próprios serviços, conforme descrito no tutorial [Introdução](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted).
- O módulo Python é executado por meio do processo de verificação dos serviços que você tem e da criação dos que são necessários, incluindo {{site.data.keyword.aios_short}}. Após o módulo ser executado com êxito, no painel do {{site.data.keyword.cloud_notm}}, é possível ativar o {{site.data.keyword.aios_short}} para ver como ele monitora um modelo.

## Antes de começar
{: #as-prereqs}

1. [Crie uma chave de API do {{site.data.keyword.cloud_notm}} e faça download dele](/docs/iam?topic=iam-userapikey#create_user_key). Será necessário inserir a chave de API em uma etapa posterior.

2. [Instale qualquer liberação do Python 3](https://www.python.org/downloads/){: external}.

  O Python 3 inclui o sistema de gerenciamento de pacote pip necessário.
  {: note}

3. Instale o pacote `ibm-ai-openscale-cli` executando o comando a seguir:

    ```
    pip install -U ibm-ai-openscale-cli
    ```
    {: codeblock}

    Se mais de uma versão do pip estiver instalada em seu sistema, talvez seja necessário executar `pip3` em vez de `pip`, como em `pip3 install -U ibm-ai-openscale-cli`.
    {: tip}

4. Se você tiver uma instância de serviço existente do {{site.data.keyword.pm_short}}, verifique o [painel do {{site.data.keyword.cloud_notm}}](https://{DomainName}){: external} para assegurar que o serviço seja gerenciado pelo {{site.data.keyword.iamshort}} (IAM), não o Cloud Foundry.

  **Importante**: o módulo verifica uma instância do {{site.data.keyword.pm_short}}. Se você tiver uma instância, o módulo a usará. Mas, se sua instância é gerenciada pelo Cloud Foundry, deve-se primeiro [migrá-la para um grupo de recursos do IAM antes de executar o módulo](/docs/resources?topic=resources-migrate#migrate).

## Executando o módulo
{: #as-run}

Execute o
seguinte comando:

```
ibm-ai-openscale-cli --apikey <Your API key>
```
{: codeblock}

## Visualizando resultados no
{{site.data.keyword.aios_short}}
{: #as-open}

Para visualizar insights sobre a justiça e a precisão do modelo, os detalhes de dados que são monitorados e a explicabilidade para uma transação individual, abra o [painel do {{site.data.keyword.aios_short}}](https://aiopenscale.cloud.ibm.com/aiopenscale/){: external}.

- Para entender o cenário para os dados de amostra, leia [Caso de uso e o valor de {{site.data.keyword.aios_short}}](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted#gs-use).

### Visualizar insights
{: #as-insights}

No [painel do {{site.data.keyword.aios_short}}](https://aiopenscale.cloud.ibm.com/aiopenscale/){: external}, clique na guia **Insights**, que mostra uma visão geral de métricas para modelos implementados: ![Insights](images/insight-dash-tab.png)

- Em uma visão rápida, a página Insights mostra quaisquer problemas com justiça e precisão, conforme determinado pelos limites que estão configurados.

- Cada implementação é mostrada como um ladrilho. O módulo configurou uma implementação chamada `GermanCreditRiskModel`, conforme mostrado na captura de tela a seguir:

  ![Insight overview](images/setup01-0206.png)

### Visualizar dados de monitoramento
{: #as-monitoring}

1. Na página Insights, clique no ladrilho `GermanCreditRiskModel` para visualizar detalhes sobre os dados monitorados.
2. Deslize o marcador no gráfico para visualizar um período de dia e horário que mostra os dados e, em seguida, clique no link **Visualizar detalhes**.

   - Por exemplo, a tela a seguir mostra os dados para uma data e um horário específicos. As datas e os horários variam, dependendo de quando você executa o módulo.

   - Para obter informações sobre como interpretar o gráfico de séries temporais, consulte [Monitorando a justiça, a média de solicitações por minuto e a precisão](/docs/services/ai-openscale?topic=ai-openscale-it-ov).

    ![Monitor data](images/setup02-0206.png)

3. Para ver detalhes sobre o monitoramento de dados `AGE`, assegure-se de que `AGE` esteja selecionado no menu suspenso.

  - Observe que, na captura de tela a seguir, não existe nenhuma propensão.

  - Para obter informações sobre como interpretar o gráfico dos pontos de dados em uma hora específica, consulte [Monitorando a justiça, a média de solicitações por minuto e a precisão](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-intp).

    ![View details](images/setup03-0206.png)

### Visualizar explicabilidade
{: #as-explain}

Para entender os fatores que contribuem quando a propensão está presente por um determinado período, na tela de visualização mostrada na seção anterior, selecione o botão **Visualizar transações**.

Os IDs de transação para a hora passada são listados para as transações que têm propensões. Para o modelo usado neste módulo, não existe nenhuma propensão para solicitações que estão disponíveis. Portanto, nenhuma transação é mostrada para o período na captura de tela a seguir.

  ![Lista de transações sem nenhuma transação](images/setup06-0206.png)

Para obter informações sobre como localizar e explicar transações, consulte [Explicando transações](/docs/services/ai-openscale?topic=ai-openscale-ie-ov#ie-view).

## Informações Relacionados
{: #as-info}

- Para aprender sobre os biases, consulte [Equidade](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor).
- Para aprender sobre o quão bem o seu modelo prevê resultados, consulte [Precisão](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor).
- Para aprender sobre interpretação de gráficos e dados, consulte [Monitorando a justiça, a média de solicitações por minuto e a precisão](/docs/services/ai-openscale?topic=ai-openscale-it-ov).
- Para aprender como os fatores subjacentes influenciam os resultados, consulte [Monitorando a explicabilidade](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).
