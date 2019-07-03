---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: deployment, monitors, data

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

# Préparation des moniteurs pour un déploiement
{: #mo-config}

Configurez et activez les moniteurs pour chaque déploiement que vous suivez avec {{site.data.keyword.aios_short}}.
{: shortdesc}

## Configuration
{: #io-conf}

L'onglet **Configurer** ( ![Onglet Configurer](images/insight-config-tab.png) )
ouvre un Récapitulatif de la configuration pour le déploiement sélectionné.

  ![Récapitulatif de la configuration](images/insight-config-summary.png)

De là, vous pouvez modifier directement les paramètres de configuration de votre moniteur de déploiement.

## Sélection d'un déploiement
{: #mo-select-deploy}

1.  Vous devez d'abord sélectionner un déploiement.

    1. Cliquez sur le bouton **Ajouter des déploiements**.
La liste des déploiements de modèle disponibles s'affiche.
    2. Cliquez sur un déploiement de modèle, puis sur **Configurer**.

    S'il y a plusieurs déploiements pour un modèle donné, lorsque vous en configurez un, tous les autres pour le même modèle sont également configurés.
    {: note}

    ![Page de sélection de déploiement](images/config-select-deploy.png)

1.  Cliquez sur le bouton **Configurer les moniteurs**.

    ![Préparer la surveillance](images/config-prep-monitor.png)

## Fournissez les informations pour la journalisation du contenu
{: #mo-work-data}

Vous devez fournir des information sur votre modèle et les données de formation.
Pour plus d'informations sur les données de formation, voir [Pourquoi {{site.data.keyword.aios_short}} a-t-il besoin d'accéder à mes données de formation ?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)

![Préparation de l'explication](images/config-what-monitor.png)

- Si vous utilisez une instance d'{{site.data.keyword.pm_full}}
qui se trouve dans la même région que votre instance de {{site.data.keyword.aios_short}},
les informations de journalisation du contenu sont configurées automatiquement pour vous.
- Dans le cas contraire,
vous devez entrer les informations sur vos données et vos types d'algorithme et sur votre journalisation du contenu
dans l'onglet et les fenêtres **Journalisation du contenu**. 

   Il y a des exigences spécifiques en fonction de vos sélections.
Pour plus d'information, voir
[Données numériques/catégorielles](https://test.cloud.ibm.com/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mo-config#mo-datan).

   Avant de configurer vos moniteurs, vous devez copier l'un des fragments de code à exécuter.
Exécutez la commande cURL dans votre application client ou la commande Python dans votre bloc-notes de sciences des données.
Cela fournit un moyen de journaliser les demandes du déploiement de modèle et d'écrire les données de réponse dans la base de données de contenu.

## Fournissez les informations sur le modèle
{: #mo-work-model-dets}

Fournissez les informations relatives à votre modèle afin que {{site.data.keyword.aios_short}}
puisse accéder à la base de données et comprendre comment le modèle est configuré.

Spécifiquement pour configurer les moniteurs, vous devez effectuer les opérations suivantes :

1. Indiquez l'emplacement des données de formation.
Vous devez entrer l'emplacement, le nom d'hôte ou l'adresse IP, le nom de la base de données et les informations d'authentification.
2. Dans la base de données, vous devez sélectionner la table de formation en sélectionnant le schéma et la table.
3. Sélectionnez la colonne de libellé dans la table de formation.
4. Sélectionnez les fonctions utilisées pour former l'déploiement d'IA.
5. Sélectionnez les fonctions texte et catégorielles.
6. Sélectionnez la colonne de prévision du déploiement.
7. Enfin, vous pouvez vérifier les informations relatives à votre modèle avant de les enregistrer.

Les sections suivantes fournissent des informations spécifiques
que vous rencontrez en fonction du type de modèle :
[données numériques/catégorielles](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mo-config#mo-datan)
ou [images et texte non structuré](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mo-config#mo-datai).


### Données numériques/catégorielles
{: #mo-nuca}

Pour les données numériques ou catégorielles, vous devez fournir des informations sur les données de formation de votre modèle pour configurer les moniteurs.

- **Configurer les moniteurs manuellement** - vous devez fournir les informations de connexion à vos données de formation.

    - Sélectionnez le [type d'algorithme](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-understand) et cliquez sur **Suivant** :

      Le format des données de formation doit correspondre au modèle.
Par exemple, si le modèle attend `M` et `F` pour la fonction `Sexe`,
les données de formation doivent contenir `M` et `F`, et non `Masculin` et `Féminin`.
L'édition actuelle de {{site.data.keyword.aios_short}} n'accepte qu'une base de données Db2 ou un emplacement Cloud Object Storage.
        {: important}

    - Indiquez l'emplacement (`Db2` ou `Cloud Object Storage`) puis :

        - Pour une base de données Db2, entrez les informations suivantes :

            - Nom d'hôte ou adresse IP
            - Port
            - Base de données (nom)
            - Nom d'utilisateur
            - Mot de passe

        - Pour Cloud Object Storage, entrez les informations suivantes :

            - URL de connexion : l'URL de connexion doit correspondre au paramètre de région du compartiment où se trouvent vos données de formation.
Vous indiquerez le compartiment des données de formation à l'étape suivante.
            - Instance de ressource (ID)
            - Clé d'API

    - Pour vous assurer que la connexion est bonne, cliquez sur le bouton **Tester** pour vous connecter aux données de formation.
    - Indiquez l'emplacement exact des données de formation dans la base de données Db2 ou dans Cloud Object Storage.

        - Pour une base de données Db2, sélectionnez un schéma et une table de formation contenant les colonnes attendues par votre modèle.
        - Pour Cloud Object Storage, sélectionnez un compartiment et un ensemble de données.

- **Télécharger un fichier de configuration** - Choisissez cette option si vous préférez garder privées vos données de formation. Vous pouvez utiliser un bloc-notes Python personnalisé pour fournir à {{site.data.keyword.aios_short}}
les informations pour analyser vos données de formation sans lui donner accès à celles-ci.

  Le bloc-notes Python vous permet de capturer des valeurs distinctes dans les colonnes du schéma, ainsi que le nom des colonnes. Il vous permet également de préconfigurer le moniteur d'équité.

   - Téléchargez le [bloc-notes personnalisé](https://github.com/IBM-Watson/aios-data-distribution/blob/master/training_statistics_notebook.ipynb){: external}
et remplacez les identifiants par les vôtres.
   - Passez soigneusement en revue le bloc-notes, en indiquant les données pour votre modèle aux endroits appropriés. Enregistrez le bloc-notes.
   - Exécutez le bloc-notes pour générer un fichier de configuration formaté en JSON.
   - Téléchargez le fichier de configuration JSON.

     ![Téléchargement du JSON de configuration](images/config-json-monitor.png)

- {{site.data.keyword.aios_short}} localise vos données de formation à partir des métadonnées stockées avec le modèle dans {{site.data.keyword.pm_full}}.
Choisissez la colonne de libellé dans les données de formation qui contient vos valeurs de prévision.
- Sélectionnez les colonnes utilisées pour former le modèle ; il s'agit des fonctions attendues par votre déploiement de modèle dans une demande.
- Enfin, sélectionnez les colonnes qui contenaient du texte et ont été converties en entiers. Par exemple, si les données de formation initiales contenaient `Masculin` et `Féminin` pour `Sexe`
et qu'elles sont maintenant mappées sur `0` et `1` respectivement,
elles contiennent maintenant les valeurs `0` et `1` pour la colonne `Sexe`. Identifiez ces colonnes qui contiennent maintenant des entiers mais contenaient initialement des valeurs texte.

### Images et texte non structuré
{: #mo-imun}

- **Images**

  Pour les modèles qui acceptent des images en entrée,
l'image doit être représentée sous la forme (hauteur) x (largeur) x (nombre de canaux),
chaque point étant la valeur monochrome ou RVB d'un pixel.

- **Texte non structuré**

   Les modèles qui acceptent du texte en entrée doivent accepter la totalité du texte, et non une représentation vectorisée de celui-ci.

## Vérification et enregistrement de la configuration
{: #mo-save}

Vérifiez le récapitulatif de vos sélections et cliquez sur **Enregistrer** pour continuer.

  ![Sélection de la table de données](images/config-summary-monitor.png)

### Etapes suivantes
{: #mo-next}

Pour commencer à configurer les moniteurs, cliquez sur l'onglet **Exactitude** puis sur **Commencer**.
