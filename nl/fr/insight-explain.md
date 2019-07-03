---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: explainability, monitoring, explain, explaining, transactions, transaction ID

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Explication des transactions
{: #ie-ov}

Pour chaque déploiement, vous pouvez voir les données d'explicabilité des différentes transactions.
{: shortdesc}

## Explication des transactions
{: #ie-view}

Dans le carreau de déploiement sélectionné,
sélectionnez l'onglet **Expliquer une transaction** ( ![Onglet Expliquer une transaction](images/insight-transact-tab.png) )
dans le navigateur et entrez un ID de transaction.

Lorsque des données sont envoyées au modèle pour évaluation, un ID de transaction est défini dans l'en-tête HTTP en définissant la zone `X-Global-Transaction-Id`. Cet ID de transaction est stocké dans la table de contenu. Pour trouver une explication du comportement du modèle pour une évaluation donnée, spécifiez l'ID de transaction associé à la demande d'évaluation. Notez que ce comportement ne s'applique qu'aux transactions {{site.data.keyword.pm_full}}, et non aux transactions non-WML.
{: note}

### Recherche d'un ID de transaction dans {{site.data.keyword.aios_short}}
{: #ie-find}

1.  Sur le graphe de temps de votre déploiement,
déplacez le marqueur dans le graphe et cliquez sur le lien **Afficher les détails**
pour [visualiser les données d'une heure particulière](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet).
1.  Cliquez sur le bouton **Afficher les transactions**
pour [voir la liste des ID de transaction](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-tra).
1.  Copiez un des ID de transaction de la liste, collez-le dans la zone de recherche sur la page **Expliquer une transaction** et appuyez sur Entrée.

    Dans la liste des ID de transaction, vous pouvez aussi
cliquer simplement sur le lien **Expliquer** dans la colonne Action pour un ID de transaction,
et la transaction s'ouvre dans l'onglet Explicabilité.
    {: note}

  Les sections suivantes fournissent des exemples d'explications pour différents types de modèles.

  ![Explicabilité - ID de transaction](images/insight-explain-trans-id.png)

## Exemple de modèle catégoriel
{: #ie-class}

Cet exemple d'explicabilité concerne un modèle de classification binaire qui approuve ou refuse des demandes d'indemnisation au titre d'une assurance. Vous pouvez voir les facteurs qui ont contribué positivement ou négativement au résultat final, `DENIED` (refusé) ici.

C'est la fonction *POLICY AGE* (âge du contrat), avec une valeur de `< 1 year`, qui a eu le plus d'influence dans la décision de refus du modèle. Les autres fonctions qui ont contribué à ce résultat sont
*CLAIM FREQUENCY* (fréquence des demandes) (`High`) (élevée) et *AGE* (`18`) ;
*CAR VALUE* (valeur du véhicule) (`$50,000`) n'a eu qu'une influence mineure.

![Explicabilité - classification binaire](images/insight-explain-binary.png)

Les graphes sont utiles pour voir les facteurs les plus importants dans le résultat d'une transaction,
mais les modèles de classification peuvent également inclure des explications avancées,
détaillées dans les sections `Modifications minimales pour le résultat Approved` et `Modifications minimales pour ce résultat`.

Les explications avancées ne sont pas disponibles pour les modèles de régression, d'image et de texte non structuré.
{: note}

La section `Modifications minimales pour le résultat Approved` nous indique que
si les valeurs des fonctions étaient remplacées par celles indiquées, la prévision du modèle changerait.

De même, la section `Modifications minimales pour ce résultat` nous indique que
même si les valeurs des fonctions étaient remplacées par celles indiquées, la prévision du modèle ne changerait pas.

Ainsi, ces deux valeurs nous indiquent le comportement du modèle autour du point de données pour lequel l'explication est générée.

![Explicabilité - classification binaire](images/insight-explain-binary2.png)

## Modèles d'image
{: #ie-image}

{{site.data.keyword.aios_short}} prend en charge l'explicabilité pour les données d'image.

### Utilisation d'un modèle d'image
{: #ie-image-working}

1. Configurez votre environnement.
   2. Installez les packages {{site.data.keyword.aios_short}} et {{site.data.keyword.pm_full}}.
   3. Configurez vos identifiants.
   4. Installez les bibliothèques nécessaires à la création des modèles et à l'analyse.
Cela comprend les bibliothèques suivantes :
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

### Explication des transactions de modèle d'image
{: #ie-image-workingviewing}

Vous pouvez voir pour un exemple d'explicabilité d'un modèle de classification d'image
les parties d'une image qui ont contribé positivement au résultat prévu et celles qui ont contribué négativement. Dans l'exemple suivant, l'image du panneau positif montre les parties qui ont influencé positivement la prévision
et celle du panneau négatif, les parties des images qui ont eu une influence négative sur le résultat.

![Explicabilité - classification d'image](images/insight-explain-image.png)

Pour {{site.data.keyword.pm_full}}, l'entrée d'évaluation pour les modèles de classification d'image envoyés pour journalisation de contenu ne peut pas dépasser 1 Mo.
Afin d'éviter des problèmes de dépassement de délai, les images ne doivent pas dépasser 125 x 125 pixels
et doivent être envoyées séquentiellement pour que l'explication de la seconde image soit demandée lorsque la première est terminée.
{: note}


### Exemples de modèle d'image
{: #ie-image-working-ntbks}

Reportez-vous aux deux bloc-notes suivants pour voir des exemples de code détaillés et développer vos propres déploiements {{site.data.keyword.aios_short}} :

- [Tutoriel sur la génération d'une explication pour un modèle image](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/image_explanation.ipynb){: external}
- [Tutoriel sur la génération d'une explication pour un modèle image à discriminant binaire](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/image_explanation_binary.ipynb){: external}


## Modèles de texte non structuré
{: #ie-unstruct}

{{site.data.keyword.aios_short}} prend en charge l'explicabilité pour les données de texte non structuré.

### Utilisation de modèles de texte non structuré
{: #ie-unstruct-steps}

1. Configurez votre environnement.
   2. Installez les packages {{site.data.keyword.aios_short}} et {{site.data.keyword.pm_full}}.
   3. Configurez vos identifiants.
   4. Installez les bibliothèques nécessaires à la création des modèles et à l'analyse.
Cela comprend les bibliothèques suivantes :
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

### Explication des transactions de texte non structuré
{: #ie-unstruct-xplan}

L'exemple suivant d'explicabilité présente un modèle de classification qui évalue du texte non structuré.
L'explication indique les mots-clés qui ont une influence positive ou négative sur la prévision du modèle. Nous indiquons également la position des mots-clés identifiés dans le texte fourni en entrée du modèle.

![Explicabilité - classification d'image](images/insight-explain-text.png)

### Exemple de modèle de texte non structuré
{: #ie-unstruct-ntbkssample}

Reportez-vous au bloc-notes suivant pour voir des exemples de code détaillés et développer vos propres déploiements {{site.data.keyword.aios_short}} :

- [Tutoriel sur la génération d'une explication pour un modèle texte](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/text_explanation.ipynb){: external}
