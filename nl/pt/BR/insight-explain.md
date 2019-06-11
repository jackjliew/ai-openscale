---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: explainability, monitoring, explain, explaining, transactions, transaction ID

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

# Explicando transações
{: #ie-ov}

Para cada implementação, é possível ver dados de explicabilidade para transações específicas.
{: shortdesc}

## Explicando transações
{: #ie-view}

No ladrilho de implementação selecionado, selecione a guia **Explicar uma transação** (![guia Explicar uma transação](images/insight-transact-tab.png)) no navegador e insira um ID de transação.

Sempre que os dados são enviados ao modelo para pontuação, ele define um ID de transação no cabeçalho de HTTP configurando o campo `X-Global-Transaction-Id`. Esse ID de transação é armazenado na tabela de carga útil. Para localizar uma explicação do comportamento do modelo para uma pontuação específica, especifique o ID de transação associado a essa solicitação de pontuação. Note que esse comportamento se aplica somente a transações do Watson Machine Learning (WML) e não é aplicável a transações não WML.
{: note}

### Localizando um ID de transação em {{site.data.keyword.aios_short}}
{: #ie-find}

1.  No gráfico de horário para sua implementação, deslize o marcador no gráfico e clique no link **Visualizar detalhes** para [visualizar dados para uma hora específica](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet).
1.  Clique no botão **Visualizar transações** para [visualizar a lista de IDs de transação](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-tra).
1.  Copie um dos IDs de transação da lista, cole-o na caixa de procura na página **Explicar uma transação** e pressione Enter.

    A lista de IDs de transação também tem a opção de simplesmente clicar no link **Explicar** na coluna Ação para qualquer ID de transação, que abrirá essa transação na guia Explicabilidade.
    {: note}

  Consulte as seções a seguir para obter exemplos de explicações para diferentes tipos de modelos.

  ![Explainability transaction ID](images/insight-explain-trans-id.png)

## Exemplo de modelo categórico
{: #ie-class}

Este exemplo de explicabilidade é para um modelo de classificação binária que aprova ou nega as solicitações de seguro. É possível ver os fatores que contribuíram de forma positiva ou negativa para o resultado final de `DENIED` neste caso.

O recurso *POLICY AGE* que tem um valor de `< 1 year` teve o impacto máximo no modelo que decide um resultado DENIED. Os outros recursos que contribuíram para esse resultado foram *CLAIM FREQUENCY* (`High`) e *AGE* (`18`), com somente um impacto menor de *CAR VALUE* (`$50,000`).

![Explainability binary classification](images/insight-explain-binary.png)

Embora os gráficos sejam úteis para mostrar os fatores mais significativos na determinação do resultado de uma transação, os modelos de classificação também podem incluir explicações avançadas, detalhadas nas seções `Minimum changes for Approved outcome` e `Minimum changes for this outcome`.

Explicações avançadas não estão disponíveis para modelos de texto de regressão, imagem e não estruturados.
{: note}

O `Minimum changes for Approved outcome` nos informa que, se os valores dos recursos foram mudados para os valores listados nesta seção, a predição do modelo mudará.

Da mesma forma, o `Minimum changes for this outcome` nos informa que, mesmo se os valores dos recursos fossem mudados para aqueles listados nessa seção, a predição do modelo não teria mudado.

Assim, esses dois valores nos informa o comportamento do modelo na proximidade do ponto de dados para o qual a explicação está sendo gerada.

![Explainability binary classification](images/insight-explain-binary2.png)

## Exemplo de modelo de imagem
{: #ie-image}

Para obter um exemplo de modelo de classificação de imagem de explicabilidade, é possível ver quais partes de uma imagem contribuíram de forma positiva para o resultado previsto e quais contribuíram de forma negativa. No exemplo abaixo, a imagem à direita mostra as partes que afetaram de forma positiva a predição e a imagem à esquerda mostra as partes de imagens que tiveram um impacto negativo no resultado.

- Para o {{site.data.keyword.pm_full}}, a carga útil de imagens perturbadas que estão
sendo enviadas por meio do gateway de aprendizado de máquina não pode exceder 1 MB. Para evitar problemas
de tempo limite, as imagens não devem exceder 125 x 125 pixels e devem ser enviadas sequencialmente, de
modo que a explicação para a segunda imagem seja solicitada quando a primeira for concluída.
{: note}

![Explainability image classification](images/insight-explain-image.png)

## Exemplo de modelo de texto não estruturado
{: #ie-unstruct}

Por último, este exemplo de explicabilidade mostra um modelo de classificação que avalia texto não estruturado. A explicação mostra as palavras-chave que tiveram um impacto positivo e também negativo na predição do modelo. Mostramos também a posição das palavras-chave identificadas no texto original que foi alimentado como entrada para o modelo.

![Explainability image classification](images/insight-explain-text.png)
