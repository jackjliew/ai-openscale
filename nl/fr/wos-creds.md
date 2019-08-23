---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: credentials, REST API, datamart ID, IDs, binding ID,  deployment ID, subscription ID

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

# Création d'identifiants pour {{site.data.keyword.aios_short}}
{: #cred-create}

Pour accéder aux API REST {{site.data.keyword.aios_full}},
il faut une clé d'API de plateforme et un ID de magasin de données (instance de service). La clé d'API de plateforme donne à un utilisateur la possibilité d'accéder aux ressources {{site.data.keyword.cloud_notm}}.
{: shortdesc}

Pour les comptes d'entreprise,
un administrateur peut créer le magasin de données, inviter les utilisateurs dans le compte
et leur donner accès à un magasin de données {{site.data.keyword.aios_short}} spécifique. Chaque utilisateur peut alors créer sa propre clé d'API de plateforme et accéder au même magasin de données {{site.data.keyword.aios_short}}. Il n'y a aucun risque de conflit ou de sécurité.

## Création de la clé d'API de plateforme
{: #cred-create-apikey}

Pour créer une clé d'API IBM Cloud, procédez comme suit :

- Connectez-vous à [{{site.data.keyword.cloud_notm}}](https://{DomainName}){: external}.
- Sélectionnez **Gérer** --> **Accès (IAM)** --> Clés d'API **{{site.data.keyword.cloud_notm}}**
- Cliquez sur le bouton **Créer une clé d'API IBM Cloud**.
- Donnez un nom et une description à votre clé et cliquez sur **Créer**.

## Trouver les ID de service :
{: #cred-find-datamart-id}

Trouvez l'ID de votre magasin de données, déploiement, abonnement ou liaison sur la page {{site.data.keyword.aios_short}} **Journalisation du contenu utile**,
qui s'affiche lorsque vous sélectionnez **Configurer les moniteurs** pour un déploiement.

1. Cliquez sur le carreau de déploiement du modèle. 
2. Cliquez sur **Configurer les moniteurs** ![icône de configuration](images/configure-deployment-button.png).
3. Cliquez sur **Journalisation du contenu utile**.
4. Sur la page {{site.data.keyword.aios_short}} **Journalisation du contenu utile**,
dans le volet **Détails**, trouvez l'ID que vous recherchez.
Par exemple, le champ **ID magasin de données** :

    ![ID de magasin de données](images/data-mart-id.png)

## Création des identifiants de l'instance de service avec la console de commandes
{: #cred-creds}

Pour créer des identifiants pour {{site.data.keyword.aios_short}}, effectuez les étapes suivantes avec la
{{site.data.keyword.cloud_notm}} [console de commande](/docs/cli?){: external} :

1. Récupérez votre clé d'API en exécutant la commande suivante :

    ```curl
    ibmcloud login --sso
    ibmcloud iam api-key-create 'my_key'
    ```

    Les informations suivantes s'affichent :

    ```bash
    Name         my_key
    Created At   2018-10-09T14:04+0000
    API Key      Tg4Gxxxxxxxxxxxxxxxxx_xxxxxxxxxxxxxxxxxQU-nE
    Locked       false
    UUID         ApiKey-xxxxxxxxx-afd7-xxxxx-b0e1-xxxxxxxxxxx
    ```

2. Vérifiez le groupe de ressources que vous utilisez dans votre compte {{site.data.keyword.cloud_notm}}.

   1. Accédez au tableau de bord.
   2. Dans le **Menu de navigation**, cliquez sur **Liste des ressources**.
   3. Dans la colonne **Groupe**, cliquez sur l'option de menu déroulant **Filtrer par groupe ou organisation**
et cochez la case **Par défaut**.

  ![Groupe de ressources dans le cloud](images/cloud-resource.png)

  Si vous n'utilisez pas le groupe de ressources `par défaut`, exécutez la commande suivante pour obtenir vos identifiants pour {{site.data.keyword.aios_short}} :

   ```curl
   ibmcloud target -g myResourceGroup
   ```

  où `myResourceGroup` est le nom du groupe de ressources associé à votre instance {{site.data.keyword.aios_short}}.

3. Récupérez votre ID d'instance {{site.data.keyword.aios_short}} en exécutant la commande suivante :

    ```curl
    ibmcloud resource service-instance '<Nom_de_votre_instance_Watson_OpenScale>'
    ```

    **Remarque** :
Si vous utilisez la console de commandes {{site.data.keyword.cloud_notm}} sous Windows,
remplacez les apostrophes (') par des guillemets (") dans les commandes précédentes.

    Les informations suivantes s'affichent :

    ```bash
    Nom :                         AI OpenScale-my_instance
    ID :                          crn:v1:ibmcloud:public:aiopenscale:us-south:a/c2f2xxxxxxxxxxxx867::
    GUID :                        03daxxxx-xxxx-xxxx-xxxx-xxxxxxxx38a7
    Site :                        us-south
    Nom du service :              aiopenscale
    Nom du forfait de service :   lite
    Nom du groupe de ressources : Default
    Etat :                        actif
    Type :                        service_instance
    Sous-type :
    Etiquettes :
    Date/heure de création :      2018-09-17T13:58:43Z
    Mise à jour :
    ```

    La valeur `GUID` est l'ID de votre instance {{site.data.keyword.aios_short}}.
        
## Etapes suivantes
{: #cred-create-next-steps}

Spécifier votre fournisseur d'apprentissage automatique :

- [Spécification d'une instance de service IBM Watson Machine Learning](/docs/services/ai-openscale?topic=ai-openscale-wml-connect)
- [Spécification d'une instance Microsoft Azure ML Studio](/docs/services/ai-openscale?topic=ai-openscale-connect-azure)
- [Spécification d'une instance Microsoft Azure ML Service](/docs/services/ai-openscale?topic=ai-openscale-connect-azureservice)
- [Spécification d'une instance de service Amazon SageMaker ML](/docs/services/ai-openscale?topic=ai-openscale-csm-connect)
- [Spécification d'une instance de service ML personnalisé](/docs/services/ai-openscale?topic=ai-openscale-co-connect)
