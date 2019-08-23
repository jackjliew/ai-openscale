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

# Explicando modelos de texto não estruturado
{: #ie-unstruct}

O {{site.data.keyword.aios_short}} suporta explicabilidade para dados de texto não estruturados.
{: shortdesc}

## Trabalhando com modelos de texto não estruturados
{: #ie-unstruct-steps}

1. Configure o seu ambiente.
   2. Instale os pacotes do {{site.data.keyword.aios_short}} e do {{site.data.keyword.pm_full}}.
   3. Configure as suas credenciais.
   4. Instale as bibliotecas que são necessárias para criar os modelos e executar a análise. Essas incluem as bibliotecas a seguir:
      - `pandas`
      - `pyspark` (se não estiver usando o {{site.data.keyword.DSX}})

1. Crie e implemente o seu modelo baseado em imagem.
   2. Carregue dados de treinamento em um quadro pandas.
   2. Treine o modelo com os dados.
   3. Publique o modelo.
   4. Implemente e pontue o modelo.

7. Configure o {{site.data.keyword.aios_short}} designando o `APIClient`, assinando o ativo e pontuando o modelo.
8. Configure a explicabilidade.
   9. Ative a explicabilidade.
   10. Obtenha explicações para as transações.

## Explicando transações de texto não estruturadas
{: #ie-unstruct-xplan}

O exemplo de explicabilidade a seguir mostra um modelo de classificação que avalia texto não estruturado. A explicação mostra as palavras-chave que tiveram um impacto positivo e também negativo na predição do modelo. Mostramos também a posição das palavras-chave identificadas no texto original que foi alimentado como entrada para o modelo.

![O gráfico de classificação de imagem de explicabilidade é exibido. Ele mostra níveis de confiança para o texto não estruturado](images/insight-explain-text.png)

## Exemplo de modelo de texto não estruturado
{: #ie-unstruct-ntbkssample}

Use as anotações a seguir para ver amostras de código detalhadas e desenvolver suas próprias implementações do {{site.data.keyword.aios_short}}:

- [Tutorial sobre como gerar uma explicação para um modelo baseado em texto](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/text_explanation.ipynb){: external}

