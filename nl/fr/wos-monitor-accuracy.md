---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

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

# Configuration du moniteur de qualité (exactitude)
{: #acc-monitor}

Le moniteur de qualité (anciennement appelé moniteur d'exactitude) vous permet de savoir si votre modèle prévoit bien les résultats.
{: shortdesc}

## Etapes de configuration
{: #acc-config}

Dans l'onglet **Qualité**, sur la page **Qu'est-ce que le moniteur de qualité ?**, cliquez sur **Commencer** pour démarrer le processus de configuration.

![Page Qu'est-ce que le moniteur de qualité ? ; elle explique que le moniteur de qualité évalue si votre modèle prévoit bien les résultats](images/wos-quality-what-is.png)

Configurez les paramètres suivants sur les pages successives de l'onglet de configuration de l'exactitude :

-  Définissez le seuil d'alerte d'exactitude. Sélectionnez une valeur qui constitue un niveau d'exactitude acceptable.
Par exemple, si vous utilisez le **modèle German Credit Risk** pour le tutoriel interactif,
définissez l'alerte à **90 %**.

    L'exactitude est une valeur synthétisée à partir de métriques pertinentes de sciences des données pour chaque type de modèle particulier.
Le score est une mesure normalisée qui vous permet de la comparer facilement entre différents types de modèle.
Dans les cas ordinaires, un score d'exactitude de 80 est suffisant.
Pour le tutoriel, nous vous recommandons 90 afin de générer plus de données.
    {: note}

-  Définissez les tailles d'échantillon minimale et maximale. La taille minimale empêche de mesurer l'exactitude
tant qu'un nombre minimum d'enregistrements n'est pas disponible dans l'ensemble de données d'évaluation,
afin que les résultats ne risquent pas d'être faussés. La taille maximale aide à mieux gérer le temps et l'effort nécessaires à l'évaluation de l'ensemble de données ;
si elle est dépassée, seuls les enregistrements les plus récents sont évalués.
Par exemple, si vous utilisez le **modèle German Credit Risk** pour le tutoriel interactif,
définissez la taille d'échantillon minimale à **100** et la taille maximale à **10000**.


Un récapitulatif de vos sélections est présenté pour vérification. Pour changer quoi que ce soit, cliquez sur le lien **Modifier** correspondant. Sinon, cliquez sur **Enregistrer** pour achever la configuration.

### Etapes suivantes
{: #acc-next}

Pour poursuivre la configuration des moniteurs, cliquez sur l'onglet **Equité** puis sur **Commencer**.
Pour plus d'information, voir [Configuration du moniteur d'équité](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor).
