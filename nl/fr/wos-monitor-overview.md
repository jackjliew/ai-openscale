---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

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

Par exemple, si vous utilisez le **modèle German Credit Risk** pour le tutoriel interactif,
sélectionnez le déploiement de modèle, définissez le type de données pour la journalisation du contenu utile
et vérifiez les paramètres présentés dans la section des détails du modèle.

## Sélection d'un déploiement
{: #mo-select-deploy}

1. Dans l'onglet **Analyses**, cliquez sur le bouton **Ajouter au tableau de bord**. 

   La liste des déploiements de modèle disponibles s'affiche.
Si vous n'en voyez aucun, vous devez déployer un modèle avec votre fournisseur d'apprentissage automatique.
Pour le tutoriel, sélectionnez le **modèle German Credit Risk**.

   ![Ecran de sélection de déploiement de modèle avec sélection d'un fournisseur d'apprentissage automatique et d'un déploiement.](images/wos-select-model-deployment.png)

2. Cliquez sur un déploiement de modèle, puis sur **Configurer**.

   S'il y a plusieurs déploiements pour un modèle donné, lorsque vous en configurez un, tous les autres pour le même modèle sont également configurés.

   Une fois vos sélections enregistrées, vous êtes prêt à configurer les moniteurs, qui incluent la journalisation du contenu utile, l'exactitude et l'équité. 

2. Pour commencer, cliquez sur **Configurer les moniteurs**.

## Fournissez les informations pour la journalisation du contenu utile
{: #mo-work-data}

Vous devez fournir des information sur votre modèle et les données de formation.
Pour plus d'information sur les données de formation, voir
[Pourquoi {{site.data.keyword.aios_short}}
a-t-il besoin d'accéder à mes données de formation ?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)
Pour le tutoriel, sélectionnez **Numérique/catégoriel** dans le champ **Type de données**
et **Classification binaire** pour le **Type d'algorithme**.

![Ecran de spécification du type d'entrée avec sélection d'un type de données et d'un type d'algorithme](images/config-what-monitor.png)

- Si vous utilisez une instance d'{{site.data.keyword.pm_full}} qui se trouve dans la même région que votre instance de {{site.data.keyword.aios_short}}, vous devez sélectionner le type de données et le type d'algorithme, mais une partie des informations de journalisation du contenu utile est configurée automatiquement pour vous. 
- Dans le cas contraire,
vous devez entrer les informations sur vos données et vos types d'algorithme et sur votre journalisation du contenu utile
dans l'onglet et les fenêtres **Journalisation du contenu utile**. 

   Il y a des exigences spécifiques en fonction de vos sélections. Pour plus d'informations, consultez
[Données numériques/catégorielles](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-datan).

   Avant de configurer vos moniteurs, vous devez copier l'un des fragments de code à exécuter. Exécutez la commande cURL dans votre application client ou la commande Python dans votre bloc-notes de sciences des données. Cela fournit un moyen de journaliser les demandes du déploiement de modèle et d'écrire les données de réponse dans la base de données de contenu utile.
   
Après avoir envoyé les détails de journalisation du contenu utile, que ce soit en passant par la méthode {{site.data.keyword.pm_full}} locale ou par l'API, vous devez retourner à l'écran **Journalisation de contenu utile** et cliquer sur **J'ai terminé**.

![écran de journalisation du contenu utile](images/payload-logging-gosales001.png)

Si l'évaluation a été envoyée correctement à {{site.data.keyword.aios_short}}, l'écran suivant apparaît lorsque vous cliquez sur le bouton **J'ai terminé**. Le bouton est masqué et vous voyez à la place le message **Journalisation activée correctement**.

![Ecran Journalisation du contenu utile après un envoi réussi des données](images/payload-logging-gosales002.png)


### Fournissez les informations sur le modèle
{: #mo-work-model-dets}

Fournissez les informations relatives à votre modèle afin que {{site.data.keyword.aios_short}}
puisse accéder à la base de données et comprendre comment le modèle est configuré.
Par exemple, si vous utilisez le **modèle German Credit Risk** pour le tutoriel interactif,
plusieurs des champs suivants sont renseignés automatiquement pour vous.

Spécifiquement pour configurer les moniteurs, vous devez effectuer les opérations suivantes :

1. Indiquez l'emplacement des données de formation. Vous devez entrer l'emplacement, le nom d'hôte ou l'adresse IP, le nom de la base de données et les informations d'authentification.
2. Dans la base de données, vous devez sélectionner la table de formation en sélectionnant le schéma et la table.
3. Sélectionnez la colonne de libellé dans la table de formation ; par example, pour le tutoriel, cliquez sur le carreau **Risk**.
4. Sélectionnez les caractéristiques utilisées pour former le déploiement d'IA.
5. Sélectionnez les caractéristiques texte et catégorielles.
6. Sélectionnez la colonne de prévision du déploiement ; par exemple, pour le tutoriel, cliquez sur le carreau **predictedLabel**.
7. Enfin, vous pouvez vérifier les informations relatives à votre modèle avant de les enregistrer.

Les sections suivantes fournissent des informations spécifiques
que vous rencontrez en fonction du type de modèle :
[données numériques/catégorielles](/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-datan)
ou [images et texte non structuré](/docs/services/ai-openscale?topic=ai-openscale-mo-config#mo-datai).


### Données numériques/catégorielles
{: #mo-nuca}

Pour les données numériques ou catégorielles, vous devez fournir des informations sur les données de formation de votre modèle pour configurer les moniteurs.

- **Configurer les moniteurs manuellement** - vous devez fournir les informations de connexion à vos données de formation.

    - Sélectionnez le [type d'algorithme](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor#acc-understand) et cliquez sur **Suivant** :

      Le format des données de formation doit correspondre au modèle. Par exemple, si le modèle attend `M` et `F` pour la caractéristique `Sexe`,
les données de formation doivent contenir `M` et `F`, et non `Masculin` et `Féminin`.  L'édition actuelle de {{site.data.keyword.aios_short}} n'accepte qu'une base de données Db2 ou un emplacement Cloud Object Storage.
        {: important}

    - Indiquez l'emplacement (`Db2` ou `Cloud Object Storage`) puis :

        - Pour une base de données Db2, entrez les informations suivantes :

            - Nom d'hôte ou adresse IP
            - Port
            - Base de données (nom)
            - Nom d'utilisateur
            - Mot de passe

        - Pour Cloud Object Storage, entrez les informations suivantes :

            - URL de connexion : l'URL de connexion doit correspondre au paramètre de région du compartiment où se trouvent vos données de formation. Vous indiquerez le compartiment des données de formation à l'étape suivante.
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

- {{site.data.keyword.aios_short}} localise vos données de formation à partir des métadonnées stockées avec le modèle dans {{site.data.keyword.pm_full}}. Choisissez la colonne de libellé dans les données de formation qui contient vos valeurs de prévision.
- Sélectionnez les colonnes utilisées pour former le modèle ; il s'agit des caractéristiques attendues par votre déploiement de modèle dans une demande.
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

Pour poursuivre la configuration des moniteurs, cliquez sur l'onglet **Qualité** puis sur **Commencer**.
Pour plus d'information, voir [Configuration du moniteur de qualité](/docs/services/ai-openscale?topic=ai-openscale-acc-monitor).
