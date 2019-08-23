---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: databases, connections, scoring, requests

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

# Enviando uma Solicitação de Pontuação
{: #cdb-score}

Para configurar os monitores, o {{site.data.keyword.aios_short}} requer que você envie uma carga útil de pontuação para iniciar o registro dos dados que serão monitorados.

- Para modelos implementados no {{site.data.keyword.pm_full}}, eles são enviados automaticamente ao {{site.data.keyword.aios_short}}. Para solicitações de pontuação enviadas automaticamente, não é necessário concluir essa tarefa e nenhum fragmento de código aparecerá.
- Para outros mecanismos de aprendizado de máquina, como o Microsoft Azure, o Amazon SageMaker ou um mecanismo de aprendizado de máquina customizado, a carga útil de pontuação deve ser enviada usando a API de criação de log de carga útil. Para isso, deve-se usar um fragmento de código no formato cURL ou Python, que pode ser recuperado na página Criação de log de carga útil. Para obter mais informações, consulte [Criação de log de carga útil para instâncias de serviço não {{site.data.keyword.pm_full}}](/docs/services/ai-openscale?topic=ai-openscale-cml-connect).

## Etapas para criação de log de carga útil
{: #cdb-score-apisteps}

1. No painel do {{site.data.keyword.aios_short}}, clique em um bloco de implementação.
2. Clique em **Configurar monitores**. 
3. Na área de janela de navegação, clique em **Criação de log de carga útil**.
2. Escolha se deseja usar o código `cURL` ou `Python` clicando na guia `cURL` ou `Python`.
3. Clique em **Copiar para a área de transferência** e cole-o nos dados de solicitação e resposta da implementação do modelo de log. Para obter mais informações, consulte [Criação de log de carga útil para instâncias de serviço não {{site.data.keyword.pm_full}}](/docs/services/ai-openscale?topic=ai-openscale-cml-connect).

Os campos e valores nos fragmentos de código precisam ser substituídos por seus valores reais, uma vez que os fornecidos são apenas exemplos.
{: important}

![Selecionar banco de dados](images/config-send-scoring.png)

Depois de executar a criação de log de carga útil, um visto aparecerá na coluna **Pronto para monitorar** para a implementação selecionada. Clique em **Configurar Monitores** para continuar.

## Entendendo o número de solicitações de pontuação
{: #cdb-score-capacity}

As solicitações de pontuação são uma parte integral do processamento do {{site.data.keyword.aios_short}}. Cada registro de transação enviado para o modelo a ser pontuado gera processamento adicional para que o serviço do {{site.data.keyword.aios_short}} possa executar perturbação e criar explicações.

- Para modelos tabulares, de texto e de imagem, a solicitação de linha de base a seguir gera pontos de dados:

   -ai-open-scale-ibm-aios-scheduling  | 1 | O planejamento da solicitação de pontuação de serviço gera 5000 pontos de dados.

- Somente para modelos de classificação tabular, há solicitações de pontuação adicionais feitas para explicação contrastiva. As solicitações a seguir são incluídas na solicitação de linha de base anterior:

   - 100 solicitações de pontuação geram 51 pontos de dados adicionais por solicitação.
   - 101 solicitações de pontuação geram ai-open-scale-ibm-aios-scheduling  | 1 | Planejamento do ponto de dados adicional de serviço por solicitação.


## Próximos passos
{: #cdb-score-next-steps-scoringreq}

[Configurar monitores](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-mo-config).
