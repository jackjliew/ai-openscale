---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

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

# Framework WML
{: #frmwrks-wml}

{{site.data.keyword.aios_full}} supporta completamente i seguenti framework {{site.data.keyword.pm_full}}: 
{: shortdesc}

Tabella 1. Dettagli supporto framework

| Framework | Tipo di problema | Tipo di dati |
|:---|:---:|:---:|
| Apache Spark MLlib | Classificazione | Strutturato |
| Python function | Classificazione | Strutturato |
| Python function | Regressione | Strutturato |
| XGBoost | Classificazione | Strutturato |
| XGBoost | Regressione | Strutturato |
| scikit-learn | Classificazione | Strutturato |
| scikit-learn | Regressione | Strutturato |
| Keras con TensorFlow<sup>1</sup> | Classificazione | Non strutturato (immagine, testo) |
| Keras con TensorFlow<sup>1</sup> | Regressione | Non strutturato (immagine, testo) |
{: caption="Dettagli supporto framework" caption-side="top"}

<sup>1</sup>Il supporto di Keras non include il supporto per la correttezza.
{: note}



