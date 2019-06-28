---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: Python, install, python module, setup, set up, insights, explainability

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

# Installation d'un module Python pour configurer {{site.data.keyword.aios_short}}
{: #as-module}

Pour automatiser la mise à disposition et la configuration des services {{site.data.keyword.cloud_notm}} requis
et voir une application {{site.data.keyword.aios_full}}, avec des exemples de données,
vous pouvez installer un module Python.
{: shortdesc}

## A propos de ce module
{: #as-about}

- Ce module fournit un autre moyen pour les utilisateurs techniques
de mettre en service une instance de {{site.data.keyword.aios_short}}
sans avoir à mettre à disposition et configurer les services eux-mêmes
comme expliqué dans le tutoriel [Initiation](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted).
- Le module Python vérifie les services dontvous disposez et crée ceux qui sont nécessaires, y compris {{site.data.keyword.aios_short}}. Une fois qu'il est en fonctionnement, vous pouvez lancer {{site.data.keyword.aios_short}} depuis le tableau de bord {{site.data.keyword.cloud_notm}}
pour voir comment il surveille un modèle.

## Avant de commencer
{: #as-prereqs}

1. [Créez une clé d'API {{site.data.keyword.cloud_notm}} et téléchargez-la](/docs/iam?topic=iam-userapikey#create_user_key). Vous aurez à l'entrer plus loin.

2. [Installez une édition quelconque de Python 3
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.python.org/downloads/){: new_window}.

  Python 3 comprend le système de gestion de package pip requis.
  {: note}

3. Installez le package `ibm-ai-openscale-cli` en exécutant la commande suivante :

    ```
    pip install -U ibm-ai-openscale-cli
    ```
    {: codeblock}

    Si plusieurs versions de pip sont installées sur votre système,
il peut être nécessaire d'exécuter `pip3` au lieu de `pip` : `pip3 install -U ibm-ai-openscale-cli`.
    {: tip}

4. Si vous disposez d'une instance de service {{site.data.keyword.pm_short}} existante,
consultez le [tableau de bord {{site.data.keyword.cloud_notm}}
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}){: new_window}
pour vérifier que le service est géré par {{site.data.keyword.iamshort}} (IAM) et non par Cloud Foundry.

  **Important** :
Le module regarde si une instance de {{site.data.keyword.pm_short}} est présente. Si c'est le cas, il l'utilise. Mais si votre instance est gérée par Cloud Foundry, vous devez d'abord
[la migrer dans un groupe de ressources IAM avant d'exécuter le module](/docs/resources?topic=resources-migrate#migrate).

## Exécution du module
{: #as-run}

Exécutez la commande suivante :

```
ibm-ai-openscale-cli --apikey <votre clé d'API>
```
{: codeblock}

## Affichage des résultats dans {{site.data.keyword.aios_short}}
{: #as-open}

Pour voir les analyses de l'équité et de l'exactitude du modèle, les détails des données surveillées ou l'explicabilité d'une transaction donnée,
ouvrez le [tableau de bord {{site.data.keyword.aios_short}}
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window}.

- Pour comprendre le scénario des exemples de données, lisez
[Scénario d'utilisation et valeur de {{site.data.keyword.aios_short}}](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted#gs-use).

### Afficher les analyses
{: #as-insights}

Dans le [tableau de bord {{site.data.keyword.aios_short}}
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://aiopenscale.cloud.ibm.com/aiopenscale/){: new_window},
cliquez sur l'onglet **Analyses**,
qui affiche une vue d'ensemble des métriques des modèles déployés :
![Analyses](images/insight-dash-tab.png)

- La page Analyses permet de voir d'un coup d'oeil les problèmes d'équité et d'exactitude déterminés par les seuils configurés.

- Chaque déploiement est affiché sous la forme d'un carreau. Le module a configuré un déploiement nommé `GermanCreditRiskModel`, montré par la capture d'écran suivante :

  ![Vue d'ensemble des analyses](images/setup01-0206.png)

### Afficher les données de surveillance
{: #as-monitoring}

1. Sur la page Analyses, cliquez sur le carreau `GermanCreditRiskModel`
pour afficher les détails sur les données surveillées.
2. Faites glisser le marqueur sur le graphique
jusqu'à un jour et une heure montrant des données et cliquez sur le lien **Afficher les détails**.

   - Par exemple, l'écran suivant affiche les données d'une date/heure donnée. Les dates et heures varient en fonction du moment où vous exécutez le module.

   - Pour savoir comment interpréter le graphe de temps,
voir [Surveillance de l'équité, du nombre moyen de demandes par minute et de l'exactitude](/docs/services/ai-openscale?topic=ai-openscale-it-ov).

    ![Surveiller les données](images/setup02-0206.png)

3. Pour voir les détails de la surveillance des données d'`AGE`, sélectionnez `AGE` dans le menu déroulant.

  - Remarquez que la capture d'écran suivante ne présente pas de biais.

  - Pour savoir comment interpréter le graphe des points de données à une heure spécifique,
voir [Surveillance de l'équité, du nombre moyen de demandes par minute et de l'exactitude](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-intp).

    ![Afficher les détails](images/setup03-0206.png)

### Afficher l'explicabilité
{: #as-explain}

Pour comprendre les facteurs contributeurs s'il y a du biais pour une certaine période,
sélectionnez le bouton **Afficher les transactions** dans l'écran de visualisation présenté à la section précédente.

Les ID des transactions de la dernière heure qui présentent un biais s'affichent. Pour le modèle utilisé dans ce module, il n'y a aucun biais pour les demandes disponibles. Par conséquent, aucune transaction n'est affichée pour la période dans la capture d'écran suivante.

  ![Liste des transactions sans transaction](images/setup06-0206.png)

Pour savoir comment trouver et expliquer les transactions, voir [Explication des transactions](/docs/services/ai-openscale?topic=ai-openscale-ie-ov#ie-view).

## Informations connexes
{: #as-info}

- Pour découvrir ce que sont les biais, voir [Equité](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor).
- Pour savoir si votre modèle prévoit bien les résultats, voir [Exactitude](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor).
- Pour savoir comment interpréter les graphes et les données, voir
[Surveillance de l'équité, du nombre moyen de demandes par minute et de l'exactitude](/docs/services/ai-openscale?topic=ai-openscale-it-ov).
- Pour savoir comment les facteurs sous-jacents influencent les résultats, voir
[Surveillance de l'explicabilité](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).
