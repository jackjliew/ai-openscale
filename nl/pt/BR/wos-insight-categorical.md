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

# Explicando um modelo categórico
{: #ie-class}

Este exemplo de explicabilidade é para um modelo de classificação binária que aprova ou nega as solicitações de seguro. É possível ver os fatores que contribuíram de forma positiva ou negativa para o resultado final de `DENIED` neste caso.
{: shortdesc}

O recurso *POLICY AGE* que tem um valor de `<ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling serviceyear` teve o impacto máximo no modelo que decide um resultado DENIED. Os outros recursos que contribuíram para esse resultado foram *CLAIM FREQUENCY* (`High`) e *AGE* (`18`), com somente um impacto menor de *CAR VALUE* (`$50,000`).

![A classificação binária de explicabilidade é exibida com detalhes sobre solicitações negadas e aprovadas](images/insight-explain-binary.png)

Embora os gráficos sejam úteis para mostrar os fatores mais significativos na determinação do resultado de uma transação, os modelos de classificação também podem incluir explicações avançadas, detalhadas nas seções `Minimum changes for Approved outcome` e `Minimum changes for this outcome`.

Explicações avançadas não estão disponíveis para modelos de texto de regressão, imagem e não estruturados.
{: note}

O `Minimum changes for Approved outcome` nos informa que, se os valores dos recursos foram mudados para os valores listados nesta seção, a predição do modelo mudará.

Da mesma forma, o `Minimum changes for this outcome` nos informa que, mesmo se os valores dos recursos fossem mudados para aqueles listados nessa seção, a predição do modelo não teria mudado.

Assim, esses dois valores nos informa o comportamento do modelo na proximidade do ponto de dados para o qual a explicação está sendo gerada.

![Detalhes da classificação binária de explicabilidade com mudanças mínimas necessárias para mudar os resultados](images/insight-explain-binary2.png)
