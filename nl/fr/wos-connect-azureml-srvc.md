---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: Microsoft Azure ML service, ml, machine learning, services

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

# Spécification d'une instance Microsoft Azure ML Service
{: #connect-azureservice}

Votre première étape dans l'outil {{site.data.keyword.aios_short}} consiste à spécifier une instance de Microsoft Azure ML Service. Votre instance Azure ML Service est l'endroit où vous stockez vos modèles et déploiements d'IA.
{: shortdesc}

Vous pouvez également ajouter votre fournisseur d'apprentissage automatique avec le SDK Python. Pour savoir comment effectuer cela par programme,
consultez [Lier votre moteur d'apprentissage automatique Microsoft Azure Service](/docs/services/ai-openscale?topic=ai-openscale-cml-azsrvconfig#cml-azsrvbind).

## Connectez votre instance Azure ML Service
{: #ca-connect}

{{site.data.keyword.aios_short}} se connecte aux modèles et déploiements d'IA dans une instance Azure ML Service.

1. Dans l'onglet **Configurer**, cliquez sur **Fournisseur d'apprentissage automatique**. Selon votre environnement, tous les fournisseurs suivants peuvent ne pas être affichés :

   ![L'écran de sélection du fournisseur d'apprentissage automatique est affiché, avec un carreau pour chaque moteur d'apprentissage automatique accepté](images/wos-machine-learning-providers-selection.png)

1.  Cliquez sur le carreau **Microsoft Azure ML Service**.
1.  Entrez et sauvegardez vos identifiants :

    - ID client : chaîne de votre ID client, qui vérifie qui vous êtes et authentifie et autorise les appels que vous faites à Azure Service.
    - Secret client : chaîne du secret, qui vérifie qui vous êtes et authentifie et autorise les appels que vous faites à Azure Service.
    - Locataire : votre ID de locataire correspond à votre organisation et est une instance dédiée d'Azure AD. Pour le trouver, passez la souris sur le nom de votre compte pour obtenir l'ID annuaire / locataire,
ou bien sélectionnez Azure Active Directory > Propriétés > ID annuaire sur le portail Azure.
    - ID d'abonnement : identifiants d'abonnement qui identifient de manière unique votre abonnement à Microsoft Azure. L'ID d'abonnement constitue une partie de l'URI à chaque appel de service.
    - Nom d'instance du fournisseur de services : nom spécifique attribué à ce fournisseur de services.
    - Description : (facultatif) votre description en langage ordinaire de cette instance du fournisseur de services. Si vous avez des environnements de production et de test, c'est un bon endroit pour indiquer ces informations.

    Pour savoir comment obtenir vos identifiants Microsoft Azure, consultez la page
[How to:
Use the portal to create an Azure AD application and service principal that can access resources](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: external}.
    {: note}

1.  {{site.data.keyword.aios_short}} affiche vos modèles déployés ; sélectionnez ceux que vous voulez surveiller et cliquez sur **Configurer**.

Vous avez correctement sélectionné les déploiements.

### Etapes suivantes
{: #ca-next}

{{site.data.keyword.aios_short}} est maintenant prêt
à ce que vous [configuriez les moniteurs](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
