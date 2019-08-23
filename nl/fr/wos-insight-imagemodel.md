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

# Explication des modèles d'image
{: #ie-image}

{{site.data.keyword.aios_short}} prend en charge l'explicabilité pour les données d'image.
{: shortdesc}

## Utilisation d'un modèle d'image
{: #ie-image-working}

1. Configurez votre environnement.
   2. Installez les packages {{site.data.keyword.aios_short}} et {{site.data.keyword.pm_full}}.
   3. Configurez vos identifiants.
   4. Installez les bibliothèques nécessaires à la création des modèles et à l'analyse. Cela comprend les bibliothèques suivantes :
      - `keras`
      - `tensorflow`
      - `keras_sequential_ascii`
      - `numpy`
      - `pillow`

1. Créez et déployez votre modèle d'image.
   2. Créez des dossiers pour les images en fonction de la manière dont vous voulez les classez.
       - Dans le répertoire `data` principal, vous devez avoir des sous-répertoires `train` et `validation`.
       - Dans chacun des sous-répertoires, vous devez avoir vos répertoires de classification.
  2. Standardisez la taille d'image puis définissez les sous-répertoires à utiliser pour la formation et la validation.
  3. Prétraitez les données pour redimensionner et récupérer les images et leur classe.
  4. Définissez et formez le modèle.
  5. Stockez le modèle.
  6. Déployez le modèle.

7. Configurez {{site.data.keyword.aios_short}} en affectant l'`APIClient`, en abonnant l'actif et en évaluant le modèle.
8. Configurez l'explicabilité.
   9. Activez l'explicabilité.
   10. Obtenez des explications pour les transactions.
   11. Affichez les images expliquées. 

## Explication des transactions de modèle d'image
{: #ie-image-workingviewing}

Vous pouvez voir pour un exemple d'explicabilité d'un modèle de classification d'image
les parties d'une image qui ont contribé positivement au résultat prévu et celles qui ont contribué négativement. Dans l'exemple suivant, l'image du panneau positif montre les parties qui ont influencé positivement la prévision
et celle du panneau négatif, les parties des images qui ont eu une influence négative sur le résultat.

![Détails de la confiance de classification image d'explicabilité, avec une image d'un chien comportant des parties mises en évidence pour montrer la partie de l'image qui a aidé à déterminer qu'il s'agissait d'un chien](images/insight-explain-image.png)

Pour {{site.data.keyword.pm_full}}, l'entrée d'évaluation pour les modèles de classification d'image envoyés pour journalisation de contenu utile ne peut pas
dépasserai-open-scale-ibm-aios-scheduling  | 1 | Scheduling serviceMo.
Afin d'éviter des problèmes de dépassement de délai, les images ne doivent pas dépasser 125 x 125 pixels
et doivent être envoyées séquentiellement pour que l'explication de la seconde image soit demandée lorsque la première est terminée.
{: note}


## Exemples de modèle d'image
{: #ie-image-working-ntbks}

Reportez-vous aux deux bloc-notes suivants pour voir des exemples de code détaillés et développer vos propres déploiements {{site.data.keyword.aios_short}} :

- [Tutoriel sur la génération d'une explication pour un modèle image](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/image_explanation.ipynb){: external}
- [Tutoriel sur la génération d'une explication pour un modèle image à discriminant binaire](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/image_explanation_binary.ipynb){: external}

