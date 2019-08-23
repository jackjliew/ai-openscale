---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: Amazon SageMaker, machine learning, services, AWS

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

# Spécification d'une instance de service Amazon SageMaker ML
{: #csm-connect}

Votre première étape dans l'outil {{site.data.keyword.aios_short}} consiste à spécifier une instance de service Amazon SageMaker. Votre instance de service Amazon SageMaker est l'endroit où vous stockez vos modèles et déploiements d'IA.
{: shortdesc}

Vous pouvez également ajouter votre fournisseur d'apprentissage automatique avec le SDK Python. Pour savoir comment effectuer cela par programme, consultez [Lier votre moteur d'apprentissage automatique Amazon SageMaker](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind).

## Connectez votre instance de service Amazon SageMaker
{: #csm-config}

{{site.data.keyword.aios_short}} se connecte aux modèles et déploiements d'IA dans une instance de service Amazon SageMaker.

1. Dans l'onglet **Configurer**, cliquez sur **Fournisseur d'apprentissage automatique**. Selon votre environnement, tous les fournisseurs suivants peuvent ne pas être affichés :

   ![L'écran de sélection du fournisseur d'apprentissage automatique est affiché, avec un carreau pour chaque moteur d'apprentissage automatique accepté](images/wos-machine-learning-providers-selection.png)

1.  Cliquez sur le carreau **Amazon SageMaker**.

    ![Entrée des identifiants du service Amazon SageMaker](images/connect-sage-cred.png)

1.  Entrez et sauvegardez vos identifiants :

    - ID clé d'accès : votre ID clé d'accès AWS, `aws_access_key_id`,
qui vérifie qui vous êtes et authentifie et autorise les appels que vous faites à AWS.
    - Clé d'accès secrète : votre clé d'accès secrète AWS, `aws_secret_access_key`,
qui est nécessaire pour vérifier qui vous êtes et pour authentifier et autoriser les appels que vous faites à AWS.
    - Région : entrez la région où votre ID clé d'accès a été créé. Les clés sont stockées et utilisées dans la région dans laquelle elles ont été créées et elles ne peuvent pas être transférées dans une autre région. 
    - Nom d'instance du fournisseur de services : nom spécifique attribué à ce fournisseur de services.
    - Description : (facultatif) votre description en langage ordinaire de cette instance du fournisseur de services. Si vous avez des environnements de production et de test, c'est un bon endroit pour indiquer ces informations.

1.  {{site.data.keyword.aios_short}} affiche vos modèles déployés ; sélectionnez ceux que vous voulez surveiller.

### Etapes suivantes
{: #csm-next}

{{site.data.keyword.aios_short}} est maintenant prêt
à ce que vous [configuriez les moniteurs](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
