---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: Microsoft Azure, ml, machine learning, services

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

# Spécification d'une instance Microsoft Azure ML Studio
{: #connect-azure}

Votre première étape dans l'outil {{site.data.keyword.aios_short}} consiste à spécifier une instance de Microsoft Azure ML Studio. Votre instance Azure ML Studio est l'endroit où vous stockez vos modèles et déploiements d'IA.
{: shortdesc}

## Connectez votre instance Azure ML Studio
{: #ca-connect}

{{site.data.keyword.aios_short}} se connecte aux modèles et déploiements d'IA dans une instance Azure ML Studio.

1.  Sur la page d'accueil de l'outil {{site.data.keyword.aios_short}}, cliquez sur **Commencer**.

    ![Page d'accueil](images/gs-config-start.png)

1.  Sélectionnez le carreau **Microsoft Azure ML Studio** et cliquez sur **Suivant**.

    ![Sélection d'Azure ML Studio](images/connect-azure.png)

1.  Entrez vos identifiants :

    Pour savoir comment obtenir vos identifiants Microsoft Azure, consultez la page
[How to:
Use the portal to create an Azure AD application and service principal that can access resources
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: new_window}.
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
