---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: Watson Studio, Watson Machine Learning, wml, machine learning, services

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

# Spécification d'une instance de service {{site.data.keyword.ibmwatson_notm}} {{site.data.keyword.pm_short}}
{: #wml-connect}

Votre première étape dans l'outil {{site.data.keyword.aios_short}} consiste à spécifier une instance d'{{site.data.keyword.pm_full}}. Votre instance de {{site.data.keyword.pm_short}} est l'endroit où vous stockez vos modèles et déploiements d'IA.
{: shortdesc}

## Conditions requises
{: #wml-prereq}

Vous devez avoir mis à disposition une instance d'{{site.data.keyword.pm_full}} dans le compte {{site.data.keyword.Bluemix_notm}}
où se trouve l'instance de service {{site.data.keyword.aios_short}}.
Si vous avez mis à disposition une instance de {{site.data.keyword.pm_full}} dans un autre compte,
vous ne pourrez pas la configurer avec la journalisation automatique du contenu avec {{site.data.keyword.aios_short}}.

## Connecter votre instance de service {{site.data.keyword.pm_short}}
{: #wml-config}

{{site.data.keyword.aios_short}} se connecte aux modèles et déploiements d'IA dans une instance d'{{site.data.keyword.pm_full}}.

1.  Sur la page d'accueil de l'outil {{site.data.keyword.aios_short}}, cliquez sur **Commencer**.

    ![Page d'accueil](images/gs-config-start.png)

2.  Sélectionnez le carreau {{site.data.keyword.pm_full}}.

    ![Sélection du carreau](images/connect-wml.png)

3.  {{site.data.keyword.aios_short}} regarde dans votre compte {{site.data.keyword.Bluemix_notm}} s'il y a déjà des instances de {{site.data.keyword.pm_full}}. Vous pouvez ensuite en sélectionner une dans le menu déroulant **Service Watson Machine Learning**.

    ![Sélection du service {{site.data.keyword.pm_short}}](images/gs-set-wml.png)

4.  (Facultatif) Vous pouvez aussi **Sélectionner un autre emplacement**
et indiquer un emplacement d'apprentissage automatique en dehors de votre compte {{site.data.keyword.Bluemix_notm}}. Fournissez les identifiants de votre emplacement en JSON valide :

    ![Définition de l'instance de {{site.data.keyword.pm_short}} ](images/gs-get-wml.png)

    Cliquez sur **Suivant**.

5.  {{site.data.keyword.aios_short}} recherche dans l'instance de Machine Learning sélectionnée la liste des déploiements qui y sont stockés. Sélectionnez dans la liste les déploiements que vous surveillerez.

    ![Sélection des déploiements](images/gs-config-deploy.png)

6.  Cliquez sur **Suivant**.
7.  Cliquez sur **Enregistrer**.

### Etapes suivantes
{: #wml-next}

{{site.data.keyword.aios_short}} est maintenant prêt
à ce que vous [spécifiiez une base de données](/docs/services/ai-openscale?topic=ai-openscale-connect-db).
