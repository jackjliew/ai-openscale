---

title: Confiança e transparência para os modelos de aprendizado de máquina com o {{site.data.keyword.aios_short}}
description: Monitor your machine learning deployments for bias, accuracy, and explainability
duration: 120
intro: In this tutorial, you will provision {{site.data.keyword.Bluemix}} machine learning and data services, create and deploy machine learning models in Watson studio, and configure the new IBM {{site.data.keyword.aios_full}} product to monitor your models for trust and transparency.
takeaways:
- See how {{site.data.keyword.aios_short}} provides trust and transparency for AI models
- Understand how {{site.data.keyword.Bluemix}} services and Watson Studio technologies can provide a seamless, AI-driven customer experience

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: ai, getting started, tutorial, understanding, video

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:hide-dashboard: .hide-dashboard}
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

# Tutorial de introdução (configuração automatizada)
{: #gettingstarted}

O {{site.data.keyword.aios_full}} permite que as empresas automatizem e operacionalizem o ciclo de vida de IA em aplicativos de negócios, assegurando que os modelos de IA sejam livres de propensão, possam ser facilmente explicados e entendidos pelos usuários de negócios e sejam auditáveis em transações de negócios. O {{site.data.keyword.aios_short}} suporta modelos de AI construídos e executados nas ferramentas e estruturas de entrega de modelo de sua escolha.
{: shortdesc}

## Visão geral
{: #gs-view-demo}

Obtenha uma visão geral rápida do {{site.data.keyword.aios_short}} assistindo a este vídeo.

<p>
  <div class="embed-responsive embed-responsive-16by9">
    <iframe class="embed-responsive-item" id="youtubeplayer" title="Confiança e transparência em IA" type="text/html" width="640" height="390" src="https://www.youtube.com/embed/6Ei8rPVtCf8" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>
  </div>
</p>

## Caso de uso do {{site.data.keyword.aios_short}}
{: #gs-use}

Os concessores tradicionais estão sob pressão para expandir seu portfólio digital de serviços financeiros para um público maior e mais diversificado, o que requer uma nova abordagem da modelagem de risco de crédito. Suas equipes de ciência de dados dependem atualmente de técnicas de modelagem padrão - como árvores de decisão e regressão logística - que funcionam bem para conjuntos de dados moderados e fazem recomendações que podem ser facilmente explicadas. Isso satisfaz os requisitos regulamentares de que as decisões de concessão de crédito devem ser transparentes e explicáveis.

Para fornecer acesso ao crédito para uma população mais ampla e mais arriscada, os históricos de crédito do requerente devem se expandir além do crédito tradicional, como hipotecas e empréstimos de carro, para fontes de crédito alternativo, como históricos de pagamento de serviços de utilidade e de plano telefônico móvel, além educação e cargos. Essas novas fontes de dados oferecem uma promessa, mas também apresentam riscos aumentando a probabilidade de correlações inesperadas que introduzem propensão com base na idade, sexo ou outras características pessoais de um requerente.

As técnicas de ciência de dados mais adequadas a esses diferentes conjuntos de dados, como as árvores impulsionadas por gradiente e as redes neurais, podem gerar modelos de risco altamente precisos, mas a um custo. Esses modelos de "caixa preta" geram predições opacas que devem de alguma forma se tornar transparentes, para garantir a aprovação regulamentar, como o artigo 22 do Regulamento Geral sobre a Proteção de Dados (GDPR) ou o Fair Credit Reporting Act (FCRA) federal gerenciado pelo Departamento de Proteção Financeira do Consumidor.

O modelo de risco de crédito fornecido neste tutorial usa um conjunto de dados de treinamento que contém 20 atributos sobre cada requerente de empréstimo. Dois desses atributos - idade e sexo - podem ser testados para propensão. Para este tutorial, o foco será a propensão com relação a sexo e idade. Para
obter mais informações sobre os dados de treinamento, veja [Por que o {{site.data.keyword.aios_short}} precisa de acesso aos meus dados de treinamento?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)

O {{site.data.keyword.aios_short}} monitorará a propensão do modelo implementado para um resultado favorável ("Sem risco") para um grupo (o Grupo de referência) sobre outro (o Grupo monitorado). Neste tutorial, o Grupo monitorado para sexo é `female`, enquanto o Grupo monitorado para idade é `19 to 25`.

## Opções de configuração
{: #gs-module}

Há várias opções de configuração, dependendo de sua preferência e nível de conhecimento.

- [A configuração automatizada a seguir](/docs/services/ai-openscale?topic=ai-openscale-wos-fast-start) conduz você pelo processo, executando tarefas no segundo plano.

   O uso de um tour significa que é possível assistir e clicar até a próxima parte do tour.
   
- [A configuração interativa](/docs/services/ai-openscale?topic=ai-openscale-gs-obj#gs-obj) permite que você tome o controle com um script fácil de seguir.

   Use a interface para executar tarefas comuns com um modelo de amostra e dados injetados.
   
- [O tutorial avançado](/docs/services/ai-openscale?topic=ai-openscale-crt-ov) permite que usuários mais técnicos instalem um módulo Python que automatiza o fornecimento e a configuração de serviços de pré-requisito. Esse tutorial avançado destina-se a cientistas de dados ou usuários que estão familiarizados com codificação, Python e Blocos de notas. É um exemplo de como o cliente do {{site.data.keyword.aios_short}} pode ser usado para executar a funcionalidade programaticamente. O bloco de notas que é usado neste tutorial resulta no mesmo local que seguir a [configuração automatizada](/docs/services/ai-openscale?topic=ai-openscale-wos-fast-start).

   Este módulo requer que o Python 3 esteja instalado, o que inclui o sistema de gerenciamento de pacote pip. Para obter instruções, consulte [Instalando um módulo Python para configurar o {{site.data.keyword.aios_short}}](/docs/services/ai-openscale?topic=ai-openscale-as-module).

Para obter links adicionais do tutorial, consulte [Recursos adicionais](/docs/services/ai-openscale?topic=ai-openscale-arsc-ov).

## Configuração Automatizada
{: #wos-fast-start}

Para ver rapidamente como o {{site.data.keyword.aios_short}} monitora um modelo, execute a opção de cenário demo que é fornecida quando você efetua login pela primeira vez na IU do {{site.data.keyword.aios_short}}.  Consulte [Trabalhando com a demo de UI](#wos-work-demo).
{: shortdesc}

## Antes de começar
{: #wos-prereqs}

Antes de iniciar o tour, deve-se ter os recursos a seguir configurados:

- [{{site.data.keyword.ibmid}}](/docs/account?topic=account-signup)
- [{{site.data.keyword.aios_full}}](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted#crt-wos-faststart)

O tour de configuração automatizada foi projetado para trabalhar com a mínima interação possível do usuário. Ele toma automaticamente as decisões a seguir para você:

- Se você tiver várias instâncias do {{site.data.keyword.pm_full}} configuradas, o processo de instalação executará uma chamada da API para listar as instâncias e escolherá a instância do {{site.data.keyword.pm_short}} que aparecer primeiro na lista resultante. 
- Para criar uma nova versão Lite do {{site.data.keyword.pm_full}}, o instalador do {{site.data.keyword.aios_short}} usa o grupo de recursos padrão para sua conta do {{site.data.keyword.Bluemix}}.

### Provisione um serviço {{site.data.keyword.aios_full}}
{: #crt-wos-faststart}

Se você ainda não tiver feito isso, assegure-se de provisionar o {{site.data.keyword.aios_full}}. 

- [Provisione uma instância do {{site.data.keyword.aios_short}}](https://{DomainName}/catalog/services/watson-openscale){: external} se você ainda não tiver uma associada à sua conta:

  ![Bloco do {{site.data.keyword.aios_short}}](images/wos-cloud-tile.png)

1. Clique em **Catálogo** > **IA** > **{{site.data.keyword.aios_short}}**.
2. Dê um nome ao seu serviço, escolha um plano e clique no botão **Criar**.
3. Para iniciar o {{site.data.keyword.aios_short}}, clique no botão **Introdução**.

## Trabalhando com a demo de UI
{: #wos-work-demo}

1.  Conecte-se à sua instância do {{site.data.keyword.aios_short}} no {{site.data.keyword.Bluemix}}.
1.  Para trabalhar com o cenário demo, clique em **Executar demo**.

   ![Demo welcome](images/fastpath_demo_11.31.04.png)

   À medida que os serviços do {{site.data.keyword.aios_short}} estão sendo provisionados, é possível revisar o cenário demo:

   ![visualização prévia de demo](images/fastpath_demo_11.31.58.png)

Quando o fornecimento estiver concluído, clique no botão **Vamos** para fazer o tour pelo painel do {{site.data.keyword.aios_short}} e continue com [Visualizando resultados no {{site.data.keyword.aios_short}}](#wos-open).

   ![Demo Vamos](images/fastpath_demo_11.33.45.png)


## Visualizando resultados no
{{site.data.keyword.aios_short}}
{: #wos-open}

Para visualizar insights sobre a justiça e a precisão do modelo, os detalhes de dados que são monitorados e a explicabilidade para uma transação individual, abra o painel do {{site.data.keyword.aios_short}}. Cada implementação é mostrada como um ladrilho. O tour configurou uma implementação chamada `GermanCreditRiskModel`, conforme mostrado na captura de tela a seguir:


   ![Demo Lets go](images/fastpath_demo_11.33.54.png)


### Visualizar insights
{: #wos-insights}

Em uma visão rápida, a página Insights mostra quaisquer problemas com justiça e precisão, conforme determinado pelos limites que estão configurados.

   ![Demo Lets go](images/fastpath_demo_11.34.00.png)

### Visualizar dados de monitoramento
{: #wos-monitoring}

1.  Na página Insights, clique no ladrilho `GermanCreditRiskModelICP` para visualizar detalhes sobre os dados monitorados.
1.  Clique e arraste o marcador no gráfico para visualizar um período de dia e horário que mostra os dados e, em seguida, clique no link **Visualizar detalhes**. Como alternativa, é possível clicar em diferentes períodos no gráfico para mudar os dados que você vê.

     - Por exemplo, a tela a seguir mostra os dados para uma data e um horário específicos. As datas e os horários variam, dependendo de quando você executa o módulo.

     - Para obter informações sobre como interpretar o gráfico de séries temporais, consulte [Monitorando a justiça, a média de solicitações por minuto e a precisão](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart).

   ![Demo Lets go](images/fastpath_demo_11.34.17.png)

1.  Para ver detalhes sobre o monitoramento de dados `SEX`, certifique-se de que `SEX` esteja selecionado no menu suspenso.

    - Observe que, na captura de tela a seguir, a propensão existe.
    
   ![Demo Lets go](images/fastpath_demo_11.34.27.png)

    - Para obter informações sobre como interpretar o gráfico dos pontos de dados em uma hora específica, consulte [Visualização de dados](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-itc-timechart#itc-data-visual).


### Visualizar explicabilidade
{: #wos-explain}

Para entender os fatores que contribuem quando a propensão está presente por um determinado período de tempo, na tela de visualização mostrada na seção anterior, clique no botão de opções **Transações sem propensão**.

   ![Demo Lets go](images/fastpath_demo_11.35.06.png)

Os IDs de transação para a hora passada são listados para as transações que têm propensões. Para o modelo usado neste módulo, existe uma propensão para solicitações que estão disponíveis.

   ![Demo Lets go](images/fastpath_demo_11.35.12.png)

Para obter informações sobre como localizar e explicar transações, consulte [Monitorando a explicabilidade](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-ie-ov).

   ![Demo Lets go](images/fastpath_demo_11.35.50.png)

## Concluindo o tour
{: #wos-done-demo}

1. Clique no botão **Pronto**.

   ![Demo Lets go](images/fastpath_demo_11.37.22.png)

2. Clique no botão **Vamos** para começar a trabalhar com o {{site.data.keyword.aios_short}}.

   ![Demo Lets go](images/fastpath_demo_11.33.45.png)

## Próximos passos
{: #gs-next}

- Aprenda mais sobre [como visualizar e interpretar os dados](/docs/services/ai-openscale?topic=ai-openscale-it-ov) e [monitorar a explicabilidade](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).
