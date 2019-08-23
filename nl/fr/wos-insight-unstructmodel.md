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

# Explication des modèles de texte non structuré
{: #ie-unstruct}

{{site.data.keyword.aios_short}} prend en charge l'explicabilité pour les données de texte non structuré.
{: shortdesc}

## Utilisation de modèles de texte non structuré
{: #ie-unstruct-steps}

1. Configurez votre environnement.
   2. Installez les packages {{site.data.keyword.aios_short}} et {{site.data.keyword.pm_full}}.
   3. Configurez vos identifiants.
   4. Installez les bibliothèques nécessaires à la création des modèles et à l'analyse. Cela comprend les bibliothèques suivantes :
      - `pandas`
      - `pyspark` (si vous n'utilisez pas {{site.data.keyword.DSX}})

1. Créez et déployez votre modèle d'image.
   2. Chargez les données de formation dans un cadre pandas.
   2. Formez le modèle sur les données.
   3. Publiez le modèle.
   4. Déployez et évaluez le modèle.

7. Configurez {{site.data.keyword.aios_short}} en affectant l'`APIClient`, en abonnant l'actif et en évaluant le modèle.
8. Configurez l'explicabilité.
   9. Activez l'explicabilité.
   10. Obtenez des explications pour les transactions.

## Explication des transactions de texte non structuré
{: #ie-unstruct-xplan}

L'exemple suivant d'explicabilité présente un modèle de classification qui évalue du texte non structuré. L'explication indique les mots-clés qui ont une influence positive ou négative sur la prévision du modèle. Nous indiquons également la position des mots-clés identifiés dans le texte fourni en entrée du modèle.

![Graphique de classification image d'explicabilité. Il indique les niveaux de confiance pour le texte non structuré](images/insight-explain-text.png)

## Exemple de modèle de texte non structuré
{: #ie-unstruct-ntbkssample}

Reportez-vous au bloc-notes suivant pour voir des exemples de code détaillés et développer vos propres déploiements {{site.data.keyword.aios_short}} :

- [Tutoriel sur la génération d'une explication pour un modèle texte](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/text_explanation.ipynb){: external}

