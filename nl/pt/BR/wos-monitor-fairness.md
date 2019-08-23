---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: fairness, fairness monitor, payload, perturbation, training data, debiased

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

# Configurando o monitor de justiça
{: #mf-monitor}

No {{site.data.keyword.aios_full}}, o monitor de justiça varre a sua implementação em busca de propensões a fim de garantir resultados justos em diferentes populações.
{: shortdesc}

## Etapas
{: #mf-config}

Na guia **Justiça**, na página **O que é Justiça?**, clique em **Iniciar** para começar o processo de configuração.

![O que é justiça? página](images/fair-what-is.png)

Em todo esse processo, o {{site.data.keyword.aios_full}} analisa seu modelo e faz recomendações com base no resultado mais lógico. Nas páginas sucessivas da guia **Justiça**, deve-se executar as tarefas a seguir:

1. Selecione os recursos a serem monitorados. Somente os recursos que são do tipo de dados de justiça categórico, numérico (inteiro), flutuante ou duplo são suportados. Os recursos com outros tipos de dados não são suportados.

1. Especifique os grupos de referência e monitorados.

   Cada recurso tem requisitos específicos para configurar. Por exemplo, caso você escolha `age` como um de seus recursos monitorados, deve-se definir os intervalos de duração para um **Grupo de referência** e um **Grupo monitorado** inserindo valores diretamente em cada grupo.

1.  Configure o limite de alerta de justiça para o recurso.

    Um limite de Justiça é usado para especificar uma diferença aceitável entre a porcentagem de resultados Favoráveis para o grupo Monitorado em comparação com a porcentagem de resultados Favoráveis para o grupo de Referência.

    Considere um modelo que prevê quem deve obter um empréstimo (`favorable outcome=loan granted`) e quem não deve (`unfavorable outcome=loan denied`). Além disso, o valor Monitorado para a idade é `[18,25]` e o valor de Referência é `[26,100]`. Quando o algoritmo de detecção de propensão é executado, se ele descobre que a porcentagem de resultados Favoráveis para pessoas no grupo de idade `[18,25]` nos últimos `N` registros mais os dados perturbados é `50%`, enquanto a porcentagem de resultados Favoráveis para as pessoas no grupo de idade `[26,100]` é `70%`, a Justiça é calculada como 50*100/70 = 71,42.

    Se o limite de Justiça for configurado como 80%, o algoritmo sinalizará o modelo como sendo propenso, porque a Justiça calculada excede o limite. No entanto, se o limite for configurado como 70%, ele não relatará o modelo como sendo propenso.

     Os valores inseridos nessas telas devem ser aqueles enviados para o terminal de pontuação do modelo (e, consequentemente, serão incluídos na tabela de carga útil). Se os dados estiverem sendo manipulados antes de serem enviados para o terminal de pontuação, insira os valores manipulados. Por exemplo, se os dados originais tinham valores de `Male` e `Female` para *Gênero* e eles foram manipulados para que os dados enviados ao terminal de pontuação fossem `M` e `F`, insira `M` e `F` nessa tela.

1.  Especifique valores que representem um resultado favorável para o modelo. Os valores serão derivados da coluna `label` nos [dados de treinamento](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata), se o esquema de saída do modelo contiver uma coluna de mapeamento. No {{site.data.keyword.pm_full}}, a coluna `prediction` sempre tem um valor duplo. A coluna de mapeamento é usada para especificar o mapeamento desse valor `prediction` para o rótulo de classe.

    Por exemplo, se o valor `prediction` for `1.0`, a coluna de mapeamento poderá ter um valor de `Loan denied`; isso implica que a predição do modelo é `Loan denied`. Portanto, se o esquema de saída do modelo contiver uma coluna de mapeamento, especifique os valores Favoráveis e Desfavoráveis usando aqueles presentes na coluna de mapeamento.

    Se, no entanto, a coluna de mapeamento não estiver presente no esquema de saída do modelo, os valores Favoráveis e Desfavoráveis precisarão ser especificados usando o valor da coluna `prediction` (`0.0`, `1.0` etc.)

1.  Finalmente, configure um tamanho mínimo de amostra para evitar a medição de Justiça até que um número mínimo de registros esteja disponível no conjunto de dados de avaliação. Isso assegura que o tamanho da amostra não seja muito pequeno para distorcer os resultados. Toda vez que a verificação de propensão for executada, ela usará o tamanho mínimo de amostra para decidir o número de registros nos quais ela fará o cálculo de propensão.

    Um resumo de suas seleções é apresentado para revisão. Se desejar mudar alguma coisa, clique no link **Editar** dessa seção, caso contrário, clique em **Salvar**.

    Também é possível clicar em **Incluir outro recurso** para retornar à tela de seleção de variável e incluir mais recursos, como `City`, `Zip Code` ou `Account Balance` no monitor de Justiça.

### Entender como funciona a desbiasing
{: #mf-debias}

Para verificar o terminal de remoção de propensão, clique no botão **Terminal de remoção de propensão**. Em seguida, é possível visualizar e copiar o terminal em diferentes formatos, como cURL, Java ou Python. 

O terminal de pontuação despropensa pode ser usado exatamente como o terminal de pontuação normal de seu modelo implementado. Além de retornar a resposta de seu modelo implementado, ele também retorna as colunas `debiased_prediction` e `debiased_probability`.

- A coluna `debiased_prediction` contém o valor de predição propensa. No caso do {{site.data.keyword.pm_full}}, esta é uma representação codificada da predição. Por exemplo, se a predição do modelo for "Loan Granted" ou "Loan Denied", o {{site.data.keyword.pm_full}} poderá codificar esses dois valores como "0.0" e "1.0", respectivamente. A coluna `debiased_prediction` contém uma representação codificada como codificada da predição despropensa.

- A coluna `debiased_probability`, por outro lado, representa a probabilidade da predição despropensa. Esta é uma matriz de valor duplo, em que cada valor representa a probabilidade da predição despropensa pertencente a uma das classes de predição.

Uma outra coluna, `debiased_decoded_target`, também é retornada, caso você tenha uma coluna em seu esquema de saída que contenha uma coluna com `modeling-role` como `decoded-target`.

- A coluna `debiased_decoded_target` contém a representação de sequência da predição despropensa. No exemplo anterior, em que o valor de predição era "0.0" ou "1.0", o `debiased_decoded_target` conterá "Loan Granted" ou "Loan Denied".

Idealmente, você chamaria diretamente esse terminal por meio de seu aplicativo de produção, em vez de chamar diretamente o terminal de pontuação de seu modelo implementado em seu mecanismo de entrega de modelo ({{site.data.keyword.pm_full}}, Amazon Sagemaker, Microsoft Azure ML Studio, etc.) Dessa forma, o {{site.data.keyword.aios_short}} também armazenará os valores `debiased` na tabela de criação de log de carga útil de sua implementação de modelo. Em seguida, toda a pontuação feita por meio desse terminal seria automaticamente despropensa.

Como esse terminal lida com a propensão de tempo de execução, ele continuará a executar verificações de segundo plano para os dados de pontuação mais recentes da tabela de criação de log de carga útil e continuará atualizando o modelo de mitigação de propensão que é usado para a despropensão das solicitações de pontuação enviadas. Dessa forma, o {{site.data.keyword.aios_short}} é sempre atualizado com os dados recebidos mais recentes e com seu comportamento para detectar e minimizar a propensão.

Finalmente, o {{site.data.keyword.aios_short}} usa um limite para decidir que os dados são agora aceitáveis e considerados como imparciais. Esse limite é tomado como o menor valor dos limites configurados no monitor de Justiça para todos os atributos de justiça configurados.

## Próximos passos
{: #mf-next}

Para continuar configurando monitores, clique na guia **Desvio** e em **Começar**. Para obter mais informações, consulte [Configurando o monitor de detecção de desvio](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-config).
