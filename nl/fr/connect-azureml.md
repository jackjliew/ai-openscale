---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: Microsoft Azure, ml, machine learning, services

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

# Spécification d'une instance Microsoft Azure ML Studio
{: #connect-azure}

Votre première étape dans l'outil {{site.data.keyword.aios_short}} consiste à spécifier une instance de Microsoft Azure ML Studio. Votre instance Azure ML Studio est l'endroit où vous stockez vos modèles et déploiements d'IA.
{: shortdesc}

Vous pouvez également ajouter votre fournisseur d'apprentissage automatique avec le SDK Python.
Pour savoir comment effectuer cela par programme, voir
[Lier votre moteur d'apprentissage automatique Microsoft Azure](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind).

## Connectez votre instance Azure ML Studio
{: #ca-connect}

{{site.data.keyword.aios_short}} se connecte aux modèles et déploiements d'IA dans une instance Azure ML Studio.

1.  Sur la page d'accueil de l'outil {{site.data.keyword.aios_short}}, cliquez sur **Commencer**.

    ![Page d'accueil](images/gs-config-start.png)

1.  Sélectionnez le carreau **Microsoft Azure ML Studio** et cliquez sur **Suivant**.

    ![Sélection d'Azure ML Studio](images/connect-azure.png)

1.  Entrez vos identifiants :

    - ID client : chaîne de votre ID client, qui vérifie qui vous êtes et authentifie et autorise les appels que vous faites à Azure Studio.
    - Secret client : chaîne du secret, qui vérifie qui vous êtes et authentifie et autorise les appels que vous faites à Azure Studio.
    - Locataire : votre ID de locataire correspond à votre organisation et est une instance dédiée d'Azure AD.
Pour le trouver, passez la souris sur le nom de votre compte pour obtenir l'ID annuaire / locataire,
ou bien sélectionnez Azure Active Directory > Propriétés > ID annuaire sur le portail Azure.
    - ID d'abonnement : identifiants d'abonnement qui identifient de manière unique votre abonnement à Microsoft Azure.
L'ID d'abonnement constitue une partie de l'URI à chaque appel de service.

    Pour savoir comment obtenir vos identifiants Microsoft Azure, consultez la page
[How to:
Use the portal to create an Azure AD application and service principal that can access resources](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: external}.
    {: note}

    ![Entrée des identifiants Azure ML Studio](images/connect-azure-cred.png)

1.  Cliquez sur **Suivant**.

1.  {{site.data.keyword.aios_short}} affiche vos modèles déployés ; sélectionnez ceux que vous voulez surveiller

    ![Sélection des modèles déployés MS Azure](images/connect-azure-deploys.png)

1.  Cliquez sur **Suivant**.

### Etapes suivantes
{: #ca-next}

{{site.data.keyword.aios_short}} est maintenant prêt
à ce que vous [spécifiiez votre base de données](/docs/services/ai-openscale?topic=ai-openscale-connect-db#connect-db).
