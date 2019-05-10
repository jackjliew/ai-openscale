---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

keywords: dashboard, navigating, navigation, insights

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:important: .important}
{:note: .note}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Navigation dans le tableau de bord
{: #io-ov}

Vous pouvez suivre tous les déploiements que vous surveillez au moyen du tableau de bord {{site.data.keyword.aios_short}}.
Le tableau de bord est votre vue principale de {{site.data.keyword.aios_short}}.
Il est constitué de cinq onglets :

  ![Onglets Analyse](images/insight-tabs.png)

{: shortdesc}

## Analyses
{: #io-ins}

L'onglet **Analyses**
( ![Tableau de bord Analyse](images/insight-dash-tab.png) )
vous fournit une vue de haut niveau de votre surveillance des déploiements.

  ![Tableau de bord Analyse](images/insight-dashboard.png)

- ***Déploiements surveillés*** -  Dans cet exemple, 10 déploiements au total sont surveillés.
Huit d'entre eux sont présentés sous forme de carreaux individuels au-dessous.

- ***Alertes d'exactitude*** - Trois alertes d'exactitude au total sont représentées dans les carreaux au-dessous par une nuance violette.
Dans cet exemple, les déploiements `Driver Performance`, `Market Analytics` et `Pricing Risk`
indiquent respectivement des valeurs d'exactitude de `60%`, `65%` et `79%`.

- ***Alertes d'équité*** - Il y a six alertes d'équité au total,
représentées dans les carreaux au-dessous par une nuance violette et une petite étiquette `BIAIS`.
Dans cet exemple, les déploiements `Driver Performance`, `Market Analytics`, `Regulatory Compliance`,
`Fraud Detection`, `Premium Optimization` et `Damage Cost Estimator`
indiquent respectivement des valeurs d'équité de
`59%`, `68%`, `62%`, `64%`, `79%` et `63%`.

Chaque carreau fournit un résumé de l'activité de surveillance pour le déploiement concerné.
Notez que celui du déploiement `Call Center Routing` n'indique aucun problème, ce qui signifie que le modèle est assez stable et exact.

### Etapes suivantes
{: #io-next}

Pour afficher plus de détails sur un déploiement, sélectionnez la tuile correspondante.
Pour plus d'information, voir
[Surveillance de l'équité, du nombre moyen de demandes par minute et de l'exactitude](/docs/services/ai-openscale?topic=ai-openscale-it-ov)
et [Surveillance de l'explicabilité](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).

## Configuration
{: #io-conf}

L'onglet **Configurer** ( ![Onglet Configurer](images/insight-config-tab.png) )
ouvre un Récapitulatif de la configuration pour le déploiement sélectionné.

  ![Récapitulatif de la configuration](images/insight-config-summary.png)

De là, vous pouvez modifier directement les paramètres de configuration de votre moniteur de déploiement.

## Transactions
{: #io-tran}

L'onglet **Expliquer une transaction** ( ![Onglet Expliquer une transaction](images/insight-transact-tab.png) )
vous permet de rechercher un ID de transaction spécifique pour expliquer une transaction de déploiement particulière.
Pour plus d'information, voir [Surveillance de l'explicabilité](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).

## Outils d'IA
{: #io-too}

L'onglet **Outils IA** ( ![Onglet Outils d'IA](images/aitools.png) )
ouvre une boîte de dialogue qui fournit un lien vers d'autres options d'outils d'IA IBM :

- *[Forfait Watson Studio Lite
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://dataplatform.cloud.ibm.com/registration/stepone?apps=all&context=wdp){: new_window} :
Watson Studio vous fournit l'environnement et les outils pour analyser et visualiser les données,
les nettoyer et les mettre en forme,
ingérer des données en flux, ou créer, former et déployer des modèles d'apprentissage automatique.
Pour l'obtenir, cliquez sur le lien "Inscrivez-vous au forfait gratuit Lite de Watson Studio".

- *[NeuNetS
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://dataplatform.cloud.ibm.com/ml/neunets){: new_window}
(*bêta*) : Le Neural Network Synthesizer, ou "NeuNetS", actuellement en édition bêta,
vous permet de synthétiser des modèles d'IA avec la technologie {{site.data.keyword.aios_short}} dans Watson Studio.
Pour l'utiliser, cliquez sur le bouton "Synthétiser un modèle".

  ![Boîte de dialogue NeuNetS](images/neunets-dialog.png)

## Onglet Aide
{: #io-help}

L'onglet Aide ( ![Onglet Transactions](images/insight-help-tab.png) )
fournit une information supplémentaire pour vous aider dans l'utilisation de {{site.data.keyword.aios_short}}.
