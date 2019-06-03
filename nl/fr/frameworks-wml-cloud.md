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

# Infrastructures WML
{: #frmwrks-wml}

{{site.data.keyword.aios_full}} prend intégralement en charge les infrastructures {{site.data.keyword.pm_full}} suivantes : 
{: shortdesc}

Tableau 1. Détails des infrastructures prises en charge

| Infrastructure | Type de problème | Type de données |
|:---|:---:|:---:|
| Apache Spark MLlib | Classification | Structuré |
| Fonction Python | Classification | Structuré |
| Fonction Python | Régression | Structuré |
| XGBoost | Classification | Structuré |
| XGBoost | Régression | Structuré |
| scikit-learn | Classification | Structuré |
| scikit-learn | Régression | Structuré |
| Keras with TensorFlow<sup>1</sup> | Classification | Non structuré (image, texte) |
| Keras with TensorFlow<sup>1</sup> | Régression | Non structuré (image, texte) |
{: caption="Détails des infrastructures prises en charge" caption-side="top"}

<sup>1</sup>La prise en charge de l'équité n'est pas incluse dans le support Keras.
{: note}



