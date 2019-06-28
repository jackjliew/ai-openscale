---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: fairness, monitoring, charts, de-biasing, bias, accuracy

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

# Monitorando a justiça, a média de solicitações por minuto e a precisão
{: #it-ov}

Os dados de monitoramento para implementações individuais são exibidos em um gráfico de séries temporais. O gráfico rastreia Justiça, média de solicitações por minuto e precisão durante os últimos sete dias.
{: shortdesc}

## Visualizando dados para uma implementação
{: #it-vdep}

Selecione uma implementação no painel para ver os dados de monitoramento para essa implementação. A parte superior do gráfico de dados de monitoramento exibe informações sobre o modelo implementado, incluindo quando o modelo foi avaliado pela última vez para Justiça e Precisão e quando ele será avaliado em seguida.

![Time series chart](images/insight-time-chart.png)

Como as verificações de algoritmo são executadas somente a cada hora, também há botões fornecidos para permitir que você verifique a Justiça e a Precisão on demand. Se não tiver fornecido registros de carga útil suficientes (Justiça) ou registros de feedback (Precisão), você verá a mensagem a seguir, por exemplo:

![Accuracy button](images/accuracy-button.png)

Em seguida, mova o marcador do outro lado do gráfico para ver estatísticas por uma hora individual. Neste exemplo, o horário selecionado é 13h CST em 18 de setembro, o que revela as estatísticas a seguir:

![Detalhe do gráfico de séries temporais](images/insight-time-detail.png)

- ***Justiça***: dois dos três recursos de Justiça, Valor do carro e Código de área, atendem seus limites configurados para aprovação. O terceiro recurso de Justiça, Idade, foi sinalizado para propensão. Também é possível ver o número de resultados esperados (neste caso, porcentagens Aprovadas vs. Negadas) para uma população individual nos recursos monitorados para justiça.
- ***Precisão***: a métrica de Precisão com média de 78%.
- ***Méd. Requisitos/min***: em média, 300 registros foram processados por minuto entre 13h e 14h CST. O rendimento é calculado a cada minuto e seu valor médio durante o curso da hora é relatado no gráfico.

## Visualizando dados para uma hora específica
{: #it-vdet}

Para ver os detalhes por trás de uma determinada estatística de Justiça, clique no link **Visualizar detalhes** para a hora selecionada.

Uma visualização é aberta dos pontos de dados para um recurso monitorado na hora selecionada. Seguindo o exemplo anterior, o recurso Idade, que foi sinalizado para propensão, é mostrado.

Observe os três filtros na parte superior da página (Recurso, Data e Hora) que permitem selecionar um recurso ou horário diferente para revisar os detalhes.

![Time series chart](images/insight-data-detail.png)

### Interpretando o gráfico
{: #it-intp}

O gráfico mostra várias coisas:

- Você pode observar a propensão de experiência da população (clientes entre 18 e 23 anos). O gráfico também mostra a porcentagem do resultado esperado (52%) para essa população.

- O gráfico mostra a percentagem do resultado esperado (70%) para a população de referência. Essa é a média do resultado esperado entre todas as populações de referência.

- O gráfico está indicando a presença de propensão, porque a proporção entre a porcentagem de resultados esperados para as populações de 18 a 23 anos de idade para a porcentagem de resultados esperados para a população de referência está abaixo do limite. Em outras palavras, 0,52/0,7 = 0,74, que é menor que o limite de 0,8.

- O gráfico também mostra a distribuição dos valores de referência e monitorados para cada valor distinto do atributo nos dados da tabela de carga útil que foi analisada para identificar a propensão. Em outras palavras, se o algoritmo de detecção de propensão analisou os últimos 1790 registros da tabela de carga útil, 120 desses registros tiveram idade de cliente entre 18 e 23 e, fora dessa distribuição, os resultados `Approved` e `Denied` são representados pelo gráfico de barras. A distribuição dos dados de carga útil é mostrada para cada valor distinto do atributo de justiça (mesmo os valores de referência são mostrados). Essas informações podem ser usadas para correlacionar a propensão com a quantia de dados recebidos pelo modelo.

- O gráfico mostra, adicionalmente, que a população com idades entre 31 e 35 anos recebeu 91% de resultados esperados. Isso significa a origem da propensão, o que significa que os dados nesse grupo distorceram os resultados e levaram a um aumento na porcentagem de resultados esperados para a classe de referência. Essas informações podem ser usadas para identificar partes dos dados que podem, em seguida, ser subamostrados ao treinar novamente o modelo.

- Outra coisa importante que o gráfico mostra é o nome da tabela que contém os dados que foram identificados para rotulagem manual. Sempre que o algoritmo detecta propensão em um modelo, ele também identifica os pontos de dados que podem ser enviados para rotulagem manual por humanos. Esses dados rotulados manualmente podem então ser usados juntamente com os dados de treinamento originais para treinar novamente o modelo. Esse modelo treinado novamente provavelmente não terá a propensão. A tabela de rotulagem manual está presente no banco de dados associado à instância do {{site.data.keyword.aios_short}}.

## Dados de Tempo de Execução e Treinamento
{: #it-rtsw}

O comutador de Dados de tempo de execução/Dados de treinamento permite alternar as diferenças entre seu modelo treinado e os dados coletados no tempo de execução que está acionando um aviso de propensão. Para
obter mais informações sobre os dados de treinamento, veja [Por que o {{site.data.keyword.aios_short}} precisa de acesso aos meus dados de treinamento?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)

![Runtime Training toggle](images/runtime_train_data.png)

## Visualizar Transações
{: #it-tra}

Essa opção permite visualizar as transações individuais que contribuíram para a propensão quando você clica no botão **Visualizar transações**.

![View transactions](images/view_transactions.png)

Uma lista de transações em que a implementação agiu de uma maneira propensa é especificada. Clique no link **Explicar** para qualquer um dos IDs de transação para obter detalhes sobre essa transação na guia Explicabilidade. Para obter mais informações, consulte [Monitorando a explicabilidade](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).

Selecione a visualização **Todas as transações** para ver todas as transações do recurso selecionado (neste exemplo, "AGE") e o período selecionado (neste exemplo, "September 15, 2018 1:00 PM"):

![Toda a lista de transações](images/transaction_list1.png)

Selecione a visualização **Transações propensas** para ver somente o subconjunto de transações que receberam resultados propensos. Cada transação propensa é comparada a uma transação semelhante, mas ligeiramente alterada (perturbada), que mostra como a mudança do valor do recurso monitorado (AGE) resultará em um resultado favorável para a transação propensa:

![Transaction list biased](images/transaction_list2.png)

## Modelo de Produção e Modelo De-Biased
{: #it-prdb}

É possível usar essas duas guias para alternar entre o seu modelo de produção e um modelo despropenso criado pelo {{site.data.keyword.aios_short}}. Consulte [Entendendo como despropensão funciona](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor#mf-debias) para obter mais detalhes.

![Runtime Training toggle](images/bias-debias.png)

Selecionar a guia **Modelo despropenso** mostrará as mudanças no modelo despropenso versus o modelo em produção. Neste exemplo, o modelo Justiça aumentou de 74% para 93%, com uma queda de somente 1% em Precisão. O gráfico também reflete o status de resultado melhorado para grupos com idades entre 18 e 23 anos.

![Runtime Training toggle](images/insight-data-detail2.png)

### Opções de Desprebimento
{: #it-dbo}

- *Despropensão passiva* - quando o {{site.data.keyword.aios_short}} faz a verificação de propensão, ele também faz uma despropensão dos dados, analisando o comportamento do modelo e identificando os dados em que o modelo está agindo de uma maneira propensa.

  O {{site.data.keyword.aios_short}} então constrói um modelo de aprendizado de máquina para prever se o modelo provavelmente agirá de uma maneira propensa em um determinado ponto de dados novo. O {{site.data.keyword.aios_short}} então analisa os dados que são recebidos pelo modelo, em uma base por hora, e localiza os pontos de dados em que o {{site.data.keyword.aios_short}} acredita que o modelo está agindo de uma maneira propensa. Para esses pontos de dados, o atributo de justiça é perturbado da minoria para a maioria e os dados perturbados são enviados para o modelo original para predição. Essa predição do modelo original é usada como a saída despropensa.

  O {{site.data.keyword.aios_short}} executa essa despropensão por hora, em todos os dados que foram recebidos pelo modelo na última hora. Ele também calcula a justiça para a saída despropensa e exibe-a na guia **Modelo despropenso**.

- *Despropensão ativa* - na despropensão ativa, é possível fazer uso de um terminal da API de REST de despropensão por meio de seu aplicativo. Esse terminal da API de REST chamará internamente seu modelo e verificará seu comportamento.

  Se o {{site.data.keyword.aios_short}} acreditar que o modelo está agindo de uma maneira propensa, ele fará a perturbação de dados conforme mencionado acima e os enviará de volta para o modelo original. A saída do modelo original nos dados perturbados será retornada como a predição despropensa. Se o {{site.data.keyword.aios_short}} determinar que o modelo original não está agindo de uma maneira propensa, o {{site.data.keyword.aios_short}} retornará a predição do modelo original como a predição despropensa. Assim, usando esse terminal da API de REST, é possível assegurar que seu aplicativo não tome decisões com base na saída propensa de seus modelos.

Selecione o link **Terminal de pontuação despropensa** para localizar seu terminal da API de REST de despropensão

![Debias API endpoint](images/insight-debias-api.png)
