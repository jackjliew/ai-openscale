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

# Affichage des données d'un déploiement
{: #it-vdep}

Pour afficher les données de surveillance d'un déploiement, sélectionnez-le dans le tableau de bord. L'en-tête affiche des informations sur le modèle déployé, telles que l'**ID du modèle** et la **Date de création**.
{: shortdesc}

![Graphe de temps avec les heures d'une journée et un score d'équité](images/insight-time-chart.png)

Comme les contrôles de l'algorithme ne sont exécutés qu'une fois par heure,
des liens sont également fournis pour vous permettre de contrôler, à la demande, l'équité et la qualité. Dans le panneau **Planning**, vous pouvez cliquer sur les liens suivants et effectuer un contrôle immédiat de vos données :

![bouton de vérification de l'équité](images/wos-fairness-button.png)


![bouton de vérification de la qualité](images/wos-quality-button.png)

Cliquez ensuite sur le graphe et déplacez-y le marqueur horizontalement pour voir les statistiques d'une heure particulière :

![Détails du graphe de temps avec un point de données spécifique sélectionnée et une infobulle disant de cliquer pour voir les détails](images/wos-insight-time-detail.png)

- ***Equité*** : deux caractéristiques d'équité, Sex et Age, ont atteint ou dépassé le seuil fixé pour l'approbation.
- ***Quality*** : la métrique **Aire sous la courbe ROC** affiche une alerte car elle n'était pas dans les limites configurées.
- ***Nombre moyen de demandes/min*** : cliquez sur la métrique **Débit** pour voir le
nombre d'enregistrements traités par minute. Le débit est calculé toutes les minutes et sa valeur moyenne sur l'heure est indiquée sur le graphe.


## Afficher les transactions
{: #it-tra}

Cette option vous permet d'afficher les différentes transactions qui ont contribué au biais lorsque vous cliquez sur le bouton **Afficher les transactions**.

![bouton d'affichage des transactions](images/view_transactions.png)

La liste des transactions où le déploiement a agi de manière biaisée s'affiche. Pour obtenir des détails sur une transaction dans l'onglet Explicabilité, cliquez sur le lien **Expliquer** pour son ID. Pour plus d'informations, consultez [Surveillance de l'explicabilité](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).

Vous pouvez voir toutes les transactions de la caractéristique (ici "AGE") et de la période (ici "15 septembre 2018 13:00") sélectionnées
en sélectionnant la vue **Toutes les transactions** :

![Transaction répertorie toutes les transactions pour un point de données spécifique](images/transaction_list1.png)

Vous pouvez n'afficher que les transactions qui ont obtenu un résultat biaisé
en sélectionnant la vue **Transactions biaisées**. Chaque transaction biaisée est comparée à une transaction similaire mais légèrement modifiée (perturbée)
qui montre comment le changement de la valeur de la caractéristique surveillée (AGE)
donnera un résultat favorable :

![Transaction répertorie seulement les transactions biaisées](images/transaction_list2.png)


