---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

keywords: fairness, fairness monitor

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

# Justiça
{: #mf-monitor}

A Justiça monitora sua implementação para propensões, para ajudar a assegurar resultados justos em diferentes populações.
{: shortdesc}

## Entendendo a Equidade
{: #mf-understand}

O {{site.data.keyword.aios_short}} verifica seu modelo implementado para propensão no tempo de execução. Para detectar a propensão para um modelo implementado, deve-se definir os atributos de justiça, como Idade ou Gênero, conforme detalhado em [Configurando o monitor de Justiça](#mf-config) abaixo.

É obrigatório especificar o esquema de saída para um modelo ou função no Watson {{site.data.keyword.pm_short}}, para que a verificação de propensão seja ativada no {{site.data.keyword.aios_short}}. O esquema de saída pode ser especificado usando a propriedade `client.repository.ModelMetaNames.OUTPUT_DATA_SCHEMA` na parte de metadados da API `store_model`. Para obter mais informações, consulte a [documentação do cliente WML ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://wml-api-pyclient-dev.mybluemix.net/#repository){: new_window}.

### Como ele funciona
{: #mf-works}

Antes de configurar o monitor de Justiça, há alguns conceitos chave que são críticos para entender:

- *Atributos de justiça*: estes são os atributos de modelo para os quais o modelo provavelmente exibirá propensão. Como um exemplo, para o atributo de justiça **`Gender`**, o modelo pode ser propenso com relação a valores de gênero específicos (`Female`, `Transgender` etc.) Outro exemplo de um atributo de justiça é **`Age`**, em que o modelo pode exibir propensão com relação a pessoas em um grupo de idade, como `18 to 25`.

- *Valor de referência/monitorado*: os valores de atributos de justiça são divididos em duas categorias distintas: Referência e Monitorado. Os valores Monitorados são aqueles que provavelmente serão discriminados. No caso de um atributo de justiça como **`Gender`**, os valores Monitorados podem ser `Female` e `Transgender`. Para um atributo de justiça numérico, como **`Age`**, os valores Monitorados podem ser `[18-25]`. Todos os outros valores para um determinado atributo de justiça são, então, considerados como valores de Referência, por exemplo, `Gender=Male` ou `Age=[26,100]`.

- *Resultado favorável/desfavorável*: a saída do modelo é categorizada como Favorável ou Desfavorável. Como um exemplo, se o modelo estiver prevendo se uma pessoa deve obter um empréstimo ou não, o resultado Favorável poderá ser `Loan Granted` ou `Loan Partially Granted`, enquanto o resultado Desfavorável pode ser `Loan Denied`. Portanto, o resultado Favorável é aquele que é considerado como um resultado positivo, enquanto o resultado Desfavorável é considerado como sendo negativo.

O algoritmo do {{site.data.keyword.aios_short}} calcula a propensão em uma base por hora, usando os últimos `N` registros presentes na tabela de criação de log de carga útil; o valor de `N` é especificado ao configurar a Justiça. O algoritmo perturba esses últimos `N` registros para gerar dados adicionais.

A perturbação é feita mudando o valor do atributo fairness de Reference para Monitored ou vice-versa. Os dados perturbados são então enviados para o modelo para avaliar seu comportamento. O algoritmo examina os últimos `N` registros na tabela de carga útil e o comportamento do modelo nos dados perturbados para decidir se o modelo está agindo de uma maneira propensa.

Um modelo será considerado como propenso se, nesse conjunto de dados combinado, a porcentagem de resultados Favoráveis para a classe Monitorada for menor que a porcentagem de resultados Favoráveis para a classe de Referência, por algum valor do limite. Esse valor do limite deve ser especificado ao configurar a Justiça.

Os valores de justiça podem ser mais de 100%. Isso significa que o grupo Monitorado recebeu resultados mais favoráveis do que o grupo de Referência. Além disso, se nenhuma nova solicitação de escoragem for enviada, o Valor de justiça permanecerá constante.
{: note}

### Por exemplo
{: #mf-ex1}

Considere um ponto de dados em que, para `Gender=Male` (valor de Referência), o modelo prevê um resultado Favorável, mas quando o registro é perturbado mudando `Gender` para `Female` (valor Monitorado), enquanto mantém todos os outros valores de recurso iguais, o modelo prevê um resultado Desfavorável. Um modelo geral é indicado para exibir propensão se houver pontos de dados suficientes (nos últimos `N` registros na tabela de carga útil, mais os dados perturbados) em que o modelo estava agindo de uma maneira propensa.

### Modelos suportados
{: #mf-supmo}

 O {{site.data.keyword.aios_short}} suporta a detecção de propensão somente para os modelos e funções Python que esperam algum tipo de dados estruturados em seu vetor de recurso.

## Configurando o Monitor de Equidade
{: #mf-config}

1.  Na página *O que é justiça?*, clique em **Avançar** para iniciar o processo de configuração.

    ![O que é justiça? página](images/fair-what-is.png)

1.  Na página *Selecionar os recursos a serem monitorados*, localize e selecione os atributos de justiça que você deseja usar e clique em **Avançar**.

    Somente os recursos que são do tipo de dados de justiça categórico, numérico (inteiro), flutuante ou duplo são suportados. Os recursos com outros tipos de dados não são suportados.
    {: note}

    Neste exemplo, os recursos `Age`, `Gender` e `Ethnicity` foram selecionados.

    ![Selecione os recursos para monitorar a página com seleções](images/fair-select-feature.png)

    Clique em **Avançar** para continuar.

1.  Cada recurso tem requisitos específicos para configurar. Neste exemplo, você define os intervalos de **`Age`** para um Grupo de referência e um Grupo monitorado, inserindo de forma manual os valores diretamente em cada grupo.

    Neste exemplo, para o atributo de justiça **`Age`**, se você sentir que seu modelo provavelmente será propenso com relação a pessoas com idades entre 18 e 25, o valor do Grupo monitorado será `[18-25]` e o valor do Grupo de referência será `[26-100]`. No caso do atributo de justiça **`Gender`**, o valor do Grupo de referência pode ser `Male`, enquanto os valores do Grupo monitorado podem ser `Female` e `Transgender`.

    ![Configure age settings](images/fair-config-age.png)

    Clique em **Avançar** para continuar

1.  Configure o limite para Justiça para **`Age`**.

    Um limite de Justiça é usado para especificar uma diferença aceitável entre a porcentagem de resultados Favoráveis para o grupo Monitorado em comparação com a porcentagem de resultados Favoráveis para o grupo de Referência.

    Considere um modelo que prevê quem deve obter um empréstimo (`favorable outcome=loan granted`) e quem não deve (`unfavorable outcome=loan denied`). Além disso, o valor Monitorado para a idade é `[18,25]` e o valor de Referência é `[26,100]`. Quando o algoritmo de detecção de propensão é executado, se ele descobre que a porcentagem de resultados Favoráveis para pessoas no grupo de idade `[18,25]` nos últimos `N` registros mais os dados perturbados é `50%`, enquanto a porcentagem de resultados Favoráveis para as pessoas no grupo de idade `[26,100]` é `70%`, a Justiça é calculada como 50*100/70 = 71,42.

    Se o limite de Justiça for configurado como 80%, o algoritmo sinalizará o modelo como sendo propenso, porque a Justiça calculada é inferior ao limite. No entanto, se o limite for configurado como 70%, ele não relatará o modelo como sendo propenso.

    ![Definir configurações de idade](images/fair-config-age-limit.png)

    Clique em **Avançar** depois de ter selecionado um limite de Justiça.

1.  Configure os recursos `Gender` e `Ethnicity` da mesma maneira:

     ![Configure gender settings](images/fair-config-gender.png)

     ![Configure ethnicity settings](images/fair-config-ethnic.png)

     **Nota**: os valores inseridos nessas telas devem ser aqueles que são enviados para o terminal de pontuação do modelo (e, consequentemente, serão incluídos na tabela de carga útil). Se os dados estiverem sendo manipulados antes de serem enviados para o terminal de pontuação, insira os valores manipulados. Por exemplo, se os dados originais tinham valores de `Male` e `Female` para *Gênero* e eles foram manipulados para que os dados enviados ao terminal de pontuação fossem `M` e `F`, insira `M` e `F` nessa tela.

     Clique em **Avançar** quando tiver concluído com cada recurso.

1.  Agora, especifique valores que representam um resultado favorável para o modelo. Os valores serão derivados da coluna `label` nos dados de treinamento, se o esquema de saída do modelo contiver uma coluna de mapeamento. No WML, a coluna `prediction` sempre tem um valor duplo. A coluna de mapeamento é usada para especificar o mapeamento desse valor `prediction` para o rótulo de classe.

    Por exemplo, se o valor `prediction` for `1.0`, a coluna de mapeamento poderá ter um valor de `Loan denied`; isso implica que a predição do modelo é `Loan denied`. Portanto, se o esquema de saída do modelo contiver uma coluna de mapeamento, especifique os valores Favoráveis e Desfavoráveis usando aqueles presentes na coluna de mapeamento.

    Se, no entanto, a coluna de mapeamento não estiver presente no esquema de saída do modelo, os valores Favoráveis e Desfavoráveis precisarão ser especificados usando o valor da coluna `prediction` (`0.0`, `1.0` etc.)

     ![Configure outcome](images/fair-config-outcome.png)

     Clique em **Avançar**.

1.  Finalmente, configure um tamanho mínimo de amostra para evitar a medição de Justiça até que um número mínimo de registros esteja disponível no conjunto de dados de avaliação. Isso assegura que o tamanho da amostra não seja muito pequeno para distorcer os resultados. Toda vez que a verificação de propensão for executada, ela usará o tamanho mínimo de amostra para decidir o número de registros nos quais ela fará o cálculo de propensão.

     ![Configure sample size](images/fair-config-sample.png)

1.  Clique no botão **Avançar**.

    Um resumo de suas seleções é apresentado para revisão. Se você desejar mudar alguma coisa, clique no link **Editar** para essa seção.

    Também é possível selecionar o link **Incluir outro recurso** para retornar à tela de seleção de recurso e incluir mais recursos no monitor de Justiça, por exemplo: `City`, `Zip Code` ou `Account Balance`.

1.  Clique em **Salvar** para concluir a configuração.

### Entender como funciona a desbiasing
{: #mf-debias}

Em seguida, você será apresentado com uma tela que fornece um terminal de pontuação despropensa.

  ![Debias API](images/fair-debias-api.png)

O terminal de pontuação despropensa pode ser usado exatamente como o terminal de pontuação normal de seu modelo implementado. Além de retornar a resposta de seu modelo implementado, ele também retorna duas colunas extras chamadas `debiased_prediction` e `debiased_probability`.

- A coluna `debiased_prediction` contém o valor de predição propensa. No caso do Watson Machine Learning (WML), essa é uma representação codificada da predição. Por exemplo, se a predição do modelo for "Loan Granted" ou "Loan Denied", o WML poderá codificar esses dois valores como "0.0" e "1.0", respectivamente. A coluna `debiased_prediction` contém uma representação codificada como codificada da predição despropensa.

- A coluna `debiased_probability`, por outro lado, representa a probabilidade da predição despropensa. Esta é uma matriz de valor duplo, em que cada valor representa a probabilidade da predição despropensa pertencente a uma das classes de predição.

Uma outra coluna, `debiased_decoded_target`, também é retornada, caso você tenha uma coluna em seu esquema de saída que contenha uma coluna com `modeling-role` como `decoded-target`.

- A coluna `debiased_decoded_target` contém a representação de sequência da predição despropensa. No exemplo acima, em que o valor prediction era "0.0" ou "1.0", o `debiased_decoded_target` conterá "Loan Granted" ou "Loan Denied".

Idealmente, você chamaria diretamente esse terminal por meio de seu aplicativo de produção, em vez de chamar diretamente o terminal de pontuação de seu modelo implementado no mecanismo de entrega de modelo (Watson Machine Learning, Amazon Sagemaker, Microsoft Azure ML Studio, etc.) Dessa forma, o {{site.data.keyword.aios_short}} também armazenará os valores `debiased` na tabela de criação de log de carga útil de sua implementação de modelo. Em seguida, toda a pontuação feita por meio desse terminal seria automaticamente despropensa.

Como esse terminal lida com a propensão de tempo de execução, ele continuará a executar verificações de segundo plano para os dados de pontuação mais recentes da tabela de criação de log de carga útil e continuará atualizando o modelo de mitigação de propensão que é usado para a despropensão das solicitações de pontuação enviadas. Dessa forma, o {{site.data.keyword.aios_short}} é sempre atualizado com os dados recebidos mais recentes e com seu comportamento para detectar e minimizar a propensão.

Finalmente, o {{site.data.keyword.aios_short}} usa um limite para decidir que os dados são agora aceitáveis e considerados como imparciais. Esse limite é tomado como o menor valor dos limites configurados no monitor de Justiça para todos os atributos de justiça configurados.

### Próximos passos
{: #mf-next}

Na página *Configurar monitores*, é possível selecionar outra categoria de monitoramento.
