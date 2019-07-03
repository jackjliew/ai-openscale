---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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

- Para modelos implementados no {{site.data.keyword.pm_full}}, basta pontuar sua implementação. O {{site.data.keyword.pm_short}} envia automaticamente a carga útil de pontuação para o {{site.data.keyword.aios_short}}. 
- Para outros mecanismos de aprendizado de máquina, como o Microsoft Azure, o Amazon SageMaker ou um mecanismo de aprendizado de máquina customizado, a carga útil de pontuação deve ser enviada usando a API de criação de log de carga útil. Para obter mais informações, consulte [Criação de log de carga útil para instâncias de serviço não {{site.data.keyword.pm_full}}](/docs/services/ai-openscale?topic=ai-openscale-cml-connect).

Como os modelos implementados no {{site.data.keyword.pm_full}} são pontuados automaticamente pelo {{site.data.keyword.aios_short}}, se você tiver apenas modelos implementados no {{site.data.keyword.pm_short}}, aparecerá um visto para indicar que essa etapa está concluída na coluna **Pronto para monitorar**.
{: note}

## Etapas para criação de log de carga útil
{: #cdb-score-apisteps}

1. Selecione uma implementação. No exemplo a seguir, **Detector de fraude** é a implementação.
2. Escolha se deseja usar o código `cURL` ou `Python` clicando na guia `cURL` ou `Python`.
3. Clique em **Copiar para a área de transferência** e cole-o nos dados de solicitação e resposta da implementação do modelo de log. Para obter mais informações, consulte [Criação de log de carga útil para instâncias de serviço não {{site.data.keyword.pm_full}}](/docs/services/ai-openscale?topic=ai-openscale-cml-connect).

Os campos e valores nos fragmentos de código precisam ser substituídos por seus valores reais, uma vez que os fornecidos são apenas exemplos.
{: important}

![Selecionar banco de dados](images/config-send-scoring.png)

Depois de executar a criação de log de carga útil, aparecerá um visto na coluna "Pronto para monitorar" para a implementação selecionada. Clique em **Configurar Monitores** para continuar.

## Entendendo o número de solicitações de pontuação
{: #cdb-score-capacity}

As solicitações de pontuação são uma parte integral do processamento do {{site.data.keyword.aios_short}}. Cada registro de transação enviado para o modelo a ser pontuado gera processamento adicional para que o serviço do {{site.data.keyword.aios_short}} possa executar perturbação e criar explicações.

- Para modelos tabulares, de texto e de imagem, a solicitação de linha de base a seguir gera pontos de dados:

   - 1 solicitação de pontuação gera 5000 pontos de dados.

- Somente para modelos de classificação tabular, há solicitações de pontuação adicionais feitas para explicação contrastiva. As solicitações a seguir são incluídas na solicitação de linha de base anterior:

   - 100 solicitações de pontuação geram 51 pontos de dados adicionais por solicitação.
   - 101 solicitações de pontuação geram 1 ponto de dados adicional por solicitação.


## Próximos passos
{: #cdb-score-next-steps-scoringreq}

[Configurar monitores](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-mo-config).
