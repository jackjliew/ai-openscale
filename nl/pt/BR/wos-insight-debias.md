---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: fairness, monitoring, charts, de-biasing, bias, accuracy

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

# Opções de Desprebimento
{: #it-dbo}

O {{site.data.keyword.aios_short}} usa dois tipos de remoção de propensão: passivo e ativo. A remoção de propensão passiva permite que você saiba como era sua propensão, enquanto a remoção de propensão ativa evita que você passe essa propensão para a frente, mudando o modelo em tempo real para o aplicativo atual.

- *Remoção de propensão passiva* - é o trabalho que o OpenScale faz por si só, automaticamente, a cada hora. É considerada passiva porque acontece sem intervenção do usuário. Quando o {{site.data.keyword.aios_short}} faz a verificação de propensão, ele também faz uma remoção de propensão dos dados, analisando o comportamento do modelo e identificando os dados em que o modelo está agindo de maneira propensa.

  O {{site.data.keyword.aios_short}} então constrói um modelo de aprendizado de máquina para prever se o modelo provavelmente agirá de uma maneira propensa em um determinado ponto de dados novo. O {{site.data.keyword.aios_short}} então analisa os dados que são recebidos pelo modelo, em uma base por hora, e localiza os pontos de dados em que o {{site.data.keyword.aios_short}} acredita que o modelo está agindo de uma maneira propensa. Para esses pontos de dados, o atributo de justiça é perturbado da minoria para a maioria e os dados perturbados são enviados para o modelo original para predição. Essa predição do modelo original é usada como a saída despropensa.

  O {{site.data.keyword.aios_short}} executa essa despropensão por hora, em todos os dados que foram recebidos pelo modelo na última hora. Ele também calcula a justiça para a saída despropensa e exibe-a na guia **Modelo despropenso**.

- *Remoção de propensão ativa* - é uma maneira de você solicitar e trazer resultados sem propensão para seu aplicativo por meio do terminal da API de REST. Você está direcionando ativamente o {{site.data.keyword.aios_short}} para executar a remoção de propensão e alterar o modelo para que seja possível executar o aplicativo de uma maneira sem propensão. Na remoção de propensão ativa, é possível usar um terminal de API de REST de remoção de propensão por meio de seu aplicativo. Esse terminal da API de REST chamará internamente seu modelo e verificará seu comportamento.

  Se o {{site.data.keyword.aios_short}} detectar que o modelo está agindo de uma maneira propensa, isso perturbará os dados conforme mencionado anteriormente e os enviará de volta para o modelo original. A saída do modelo original nos dados perturbados será retornada como a predição despropensa. Se o {{site.data.keyword.aios_short}} determinar que o modelo original não está agindo de uma maneira propensa, o {{site.data.keyword.aios_short}} retornará a predição do modelo original como a predição despropensa. Assim, usando esse terminal da API de REST, é possível assegurar que seu aplicativo não tome decisões com base na saída propensa de seus modelos.

Selecione o link **Terminal de pontuação despropensa** para localizar seu terminal da API de REST de despropensão

![A tela Detalhes do terminal da API de remoção de propensão é exibida com o exemplo cURL exibido na caixa de fragmento de código](images/insight-debias-api.png)

## Próximos passos
{: #it-dbo-nextsteps}

- Para minimizar a propensão, depois de ela ter sido detectada, deve-se criar uma nova versão do modelo que corrija o problema. O {{site.data.keyword.aios_short}} armazena registros com propensão na tabela de rotulagem manual. Esses registros com propensão precisam ser rotulados manualmente e, em seguida, o modelo precisa ser treinado novamente usando esses dados adicionais para criar uma nova versão do modelo que não tenha propensão.


