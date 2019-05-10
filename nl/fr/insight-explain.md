---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

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

# Surveillance de l'explicabilité
{: #ie-ov}

Pour chaque déploiement, vous pouvez voir les données d'explicabilité des différentes transactions.
{: shortdesc}

## Explication des transactions
{: #ie-view}

Dans le carreau de déploiement sélectionné,
sélectionnez l'onglet **Expliquer une transaction** ( ![Onglet Expliquer une transaction](images/insight-transact-tab.png) )
dans le navigateur et entrez un ID de transaction.

Lorsque des données sont envoyées au modèle pour évaluation, un ID de transaction est défini dans l'en-tête HTTP en définissant la zone `X-Global-Transaction-Id`.
Cet ID de transaction est stocké dans la table de contenu.
Pour trouver une explication du comportement du modèle pour une évaluation donnée, spécifiez l'ID de transaction associé à la demande d'évaluation.
Notez que ce comportement ne s'applique qu'aux transactions Watson Machine Learning (WML), et non aux transactions non-WML.
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

Cet exemple d'explicabilité concerne un modèle de classification binaire qui approuve ou refuse des demandes d'indemnisation au titre d'une assurance.
Vous pouvez voir les facteurs qui ont contribué positivement ou négativement au résultat final, `DENIED` (refusé) ici.

C'est la fonction *POLICY AGE* (âge du contrat), avec une valeur de `< 1 year`, qui a eu le plus d'influence dans la décision de refus du modèle.
Les autres fonctions qui ont contribué à ce résultat sont
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

## Exemple de modèle d'image
{: #ie-image}

Vous pouvez voir pour un exemple d'explicabilité d'un modèle de classification d'image
les parties d'une image qui ont contribé positivement au résultat prévu et celles qui ont contribué négativement.
Dans l'exemple ci-dessous, l'image de droite montre les parties qui ont influencé positivement la prévision
et celle de gauche, les parties des images qui ont eu une influence négative sur le résultat.

Actuellement la génération d'explication n'est pas possible pour les images de plus de 1 Mo.
{: note}

![Explicabilité - classification d'image](images/insight-explain-image.png)

## Exemple de modèle de texte non structuré
{: #ie-unstruct}

Enfin, cet exemple d'explicabilité présente un modèle de classification qui évalue du texte non structuré.
L'explication indique les mots-clés qui ont une influence positive ou négative sur la prévision du modèle.
Nous indiquons également la position des mots-clés identifiés dans le texte fourni en entrée du modèle.

![Explicabilité - classification d'image](images/insight-explain-text.png)
