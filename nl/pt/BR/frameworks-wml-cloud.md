---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: supported frameworks, models, model types, limitations, limits

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
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Estruturas WML
{: #frmwrks-wml}

{{site.data.keyword.aios_full}} suporta totalmente as seguintes estruturas do {{site.data.keyword.pm_full}}: 
{: shortdesc}

Tabela 1. Detalhes do suporte da estrutura

| Estrutura | Tipo de problema | Tipo de Dados |
|:---|:---:|:---:|
| Apache Spark MLlib | Classificação | Estruturados |
| função Python | Classificação | Estruturados |
| função Python | Procedimento de | Estruturados |
| XGBoost | Classificação | Estruturados |
| XGBoost | Procedimento de | Estruturados |
| scikit-learn | Classificação | Estruturados |
| scikit-learn | Procedimento de | Estruturados |
| Keras com TensorFlow<sup>1</sup> | Classificação | Não estruturados (imagem, texto) |
| Keras com TensorFlow<sup>1</sup> | Procedimento de | Não estruturados (imagem, texto) |
{: caption="Detalhes do suporte da estrutura" caption-side="top"}

<sup>1</sup>O suporte do Keras não inclui suporte para justiça.
{: note}



