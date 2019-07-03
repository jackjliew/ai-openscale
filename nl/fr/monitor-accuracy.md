---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: accuracy, 

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

# Configuration du moniteur d'exactitude ou de qualité
{: #acc-monitor}

Le moniteur de qualité (anciennement appelé moniteur d'exactitude) vous permet de savoir si votre modèle prévoit bien les résultats.
{: shortdesc}

## Etapes de configuration
{: #acc-config}

Dans l'onglet **Exactitude**, sur la page **Qu'est-ce que l'exactitude ?**,
cliquez sur **Commencer** pour démarrer le processus de configuration.

![Page Qu'est-ce que l'exactitude ?](images/accuracy-what-is.png)

Configurez les paramètres suivants sur les pages successives de l'onglet de configuration de l'exactitude :

-  Définissez le seuil d'alerte d'exactitude.
Sélectionnez une valeur qui constitue un niveau d'exactitude acceptable.

    L'exactitude est une valeur synthétisée à partir de métriques pertinentes de sciences des données pour chaque type de modèle particulier. Le score est une mesure normalisée qui vous permet de la comparer facilement entre différents types de modèle. Dans les cas ordinaires, un score d'exactitude de 80 est suffisant.
    {: note}

-  Définissez les tailles d'échantillon minimale et maximale.
La taille minimale empêche de mesurer l'exactitude
tant qu'un nombre minimum d'enregistrements n'est pas disponible dans l'ensemble de données d'évaluation,
afin que les résultats ne risquent pas d'être faussés. La taille maximale aide à mieux gérer le temps et l'effort nécessaires à l'évaluation de l'ensemble de données ;
si elle est dépassée, seuls les enregistrements les plus récents sont évalués.


Un récapitulatif de vos sélections est présenté pour vérification.
Pour changer quoi que ce soit, cliquez sur le lien **Modifier** correspondant.
Sinon, cliquez sur **Enregistrer** pour achever la configuration.

### Etapes suivantes
{: #acc-next}

Sur la page **Configurer les moniteurs**, vous pouvez sélectionner une autre catégorie de surveillance.
