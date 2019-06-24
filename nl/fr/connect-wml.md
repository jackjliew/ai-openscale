---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

keywords: Watson Studio, Watson Machine Learning, wml, machine learning, services

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

# Spécification d'une instance de service Watson Machine Learning
{: #wml-connect}

Votre première étape dans l'outil {{site.data.keyword.aios_short}} consiste à spécifier une instance de Watson Machine Learning (WML). Votre instance de WML est l'endroit où vous stockez vos modèles et déploiements d'IA.
{: shortdesc}

## Conditions requises
{: #wml-prereq}

Vous devez avoir mis à disposition une instance de WML dans le compte {{site.data.keyword.Bluemix_notm}}
où se trouve l'instance de service {{site.data.keyword.aios_short}}. Si vous avez mis à disposition une instance de WML dans un autre compte,
vous ne pourrez pas la configurer avec {{site.data.keyword.aios_short}}.

## Connecter votre instance de service Watson Machine Learning
{: #wml-config}

{{site.data.keyword.aios_short}} se connecte aux modèles et déploiements d'IA dans une instance de WML.

1.  Sur la page d'accueil de l'outil {{site.data.keyword.aios_short}}, cliquez sur **Commencer**.

    ![Page d'accueil](images/gs-config-start.png)

2.  Sélectionnez le carreau Watson Machine Learning.

    ![Sélection du carreau](images/connect-wml.png)

3.  {{site.data.keyword.aios_short}} regarde dans votre compte {{site.data.keyword.Bluemix_notm}} s'il y a déjà des instances de WML. Vous pouvez ensuite en sélectionner une dans le menu déroulant **Service Watson Machine Learning**.

    ![Sélection du service WML](images/gs-set-wml.png)

4.  (Facultatif) Vous pouvez aussi **Sélectionner un autre emplacement**
et indiquer un emplacement d'apprentissage automatique en dehors de votre compte {{site.data.keyword.Bluemix_notm}}. Fournissez les identifiants de votre emplacement en JSON valide :

    ![Définition de l'instance de WML](images/gs-get-wml.png)

    Cliquez sur **Suivant**.

5.  {{site.data.keyword.aios_short}} recherche dans l'instance de Machine Learning sélectionnée la liste des déploiements qui y sont stockés. Sélectionnez dans la liste les déploiements que vous surveillerez.

    ![Sélection des déploiements](images/gs-config-deploy.png)

6.  Cliquez sur **Suivant**.
7.  Cliquez sur **Enregistrer**.

### Etapes suivantes
{: #wml-next}

{{site.data.keyword.aios_short}} est maintenant prêt
à ce que vous [spécifiiez une base de données](/docs/services/ai-openscale?topic=ai-openscale-connect-db).
