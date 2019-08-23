---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

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
Des transactions n'apparaissent que s'il y a des données pour les moniteurs ;
elles dépendent des seuils que vous avez définis,
de l'heure à laquelle est planifiée l'exécution des moniteurs, et de la disponibilité de données de contenu utile d'{{site.data.keyword.pm_full}}.
{: shortdesc}

## Affichage des explications par ID de transaction
{: #ie-view}

1. Cliquez sur un carreau de déploiement.
2. Cliquez sur l'onglet **Expliquer une transaction**
(![onglet Expliquer une transaction](images/insight-transact-tab.png) ) dans le navigateur.
3. Entrez un ID de transaction.

Lorsque des données sont envoyées au modèle pour évaluation, un ID de transaction est défini dans l'en-tête HTTP en définissant la zone `X-Global-Transaction-Id`. Cet ID de transaction est stocké dans la table de contenu utile. Pour trouver une explication du comportement du modèle pour une évaluation donnée, spécifiez l'ID de transaction associé à la demande d'évaluation. Notez que ce comportement ne s'applique qu'aux transactions {{site.data.keyword.pm_full}}, et non aux transactions non-WML.
{: note}

## Recherche d'un ID de transaction dans {{site.data.keyword.aios_short}}
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

## Trouver les explications dans les détails du graphique
{: #ie-view-ui}

Comme il y a des explications pour les métriques d'équité et de dérive,
vous pouvez cliquer sur les graphiques pour obtenir une vue détaillée de l'ensemble de données,
puis cliquer sur le bouton **Afficher les transactions** pour les métriques d'équité
ou sur un carreau de transaction à dérive pour voir les explications.

- Cliquez sur l'un des attributs d'équité, comme le sexe ou l'âge,
puis sur le graphique, et enfin sur le bouton **Afficher les transactions**.
- Pour le moniteur de dérive, cliquez sur **Ampleur de la dérive**,
puis sur le graphique, et enfin sur un carreau pour voir les transactions associées au groupe de dérive concerné.

## Etapes suivantes
{: #ie-trans-id-next}

- [Explication des modèles catégoriels](/docs/services/ai-openscale?topic=ai-openscale-ie-class)
- [Explication des modèles d'image](/docs/services/ai-openscale?topic=ai-openscale-ie-image)
- [Explication des modèles de texte non structuré](/docs/services/ai-openscale?topic=ai-openscale-ie-unstruct)
- [Explications contrastives](/docs/services/ai-openscale?topic=ai-openscale-ie-pp-pn)
