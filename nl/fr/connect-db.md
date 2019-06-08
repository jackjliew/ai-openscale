---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: databases, connections, scoring, requests

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

# Spécification d'une base de données
{: #connect-db}

Spécifier une base de données pour votre instance de {{site.data.keyword.aios_short}}.
{: shortdesc}

## Connexion à votre base de données
{: #cdb-connect}

{{site.data.keyword.aios_short}} utilise une base de données pour stocker les données de contenu, de commentaires et de mesure. En plus de sélectionner une base de données, vous pouvez également sélectionner un schéma pour celle-ci
(un schéma est une collection de tables avec un nom dans la base de données).

1.  Choisissez une base de données. Vous avez deux options : la base de données gratuite ou une base de données existante ou nouvelle.

    ![Sélection de la base de données](images/gs-config-database.png)

    Si vous avez un compte {{site.data.keyword.cloud_notm}} payant,
vous pouvez mettre à disposition un service `Databases for PostgreSQL` ou `Db2 Warehouse`
pour profiter pleinement de l'intégration avec Watson Studio et des services d'apprentissage continu. Si vous choisissez de ne pas mettre à disposition un service payant,
vous pouvez utiliser le stockage PostgreSQL interne gratuit
avec {{site.data.keyword.aios_short}}, mais vous ne pourrez pas configurer l'apprentissage continu pour votre modèle.
    {: note}

### Base de données gratuite du forfait Lite
{: #cdb-lite}

**REMARQUE** : la base de données gratuite comporte des limitations importantes :

- La base de données gratuite est hébergée et ne vous est pas directement accessible.
- {{site.data.keyword.aios_full}} aura l'accès complet à votre base de données et donc à vos données.
- La base de données gratuite n'est pas en conformité avec le RGPD. Vous ne pouvez pas l'utiliser si votre modèle traite des informations à caractère personnel. Vous devez en acheter une nouvelle ou en utiliser une existante qui soit en conformité avec les règles du RGPD. Pour en savoir plus, voir [Sécurité des informations](/docs/services/ai-openscale?topic=ai-openscale-is-ov).

Pour utiliser la base de données gratuite, cliquez sur le carreau **Utiliser la base de données gratuite hébergée par {{site.data.keyword.aios_short}}**, puis vérifiez le récapitulatif et cliquez sur **Enregistrer**.

  ![Sélection de la base de données](images/gs-config-database2.png)
  
Vous pouvez effectuer une mise à niveau vers une autre base de données à partir de la base de données gratuite, mais il n'est pas possible de reconfigurer une instance Compose for Postgres, Database for Postgres ou Db2 vers la base de données gratuite. Après la mise à niveau, il est impossible de revenir à l'utilisation de la base de données gratuite. Toutes les données en cours, telles que la configuration, les résultats d'évaluation et les explications ne peuvent pas être réutilisées. En sélectionnant un autre schéma ou une autre base de données, l'environnement {{site.data.keyword.aios_short}} est entièrement réinitialisé.



### Base de données existante ou nouvelle
{: #cdb-exn}

1.  Lorsque vous sélectionnez l'option "Utiliser une base de données existante ou en acheter une nouvelle",
{{site.data.keyword.aios_short}} regarde dans votre compte {{site.data.keyword.Bluemix_notm}} s'il y a déjà des bases de données.

1.  Sélectionnez le type de votre base de données existante (Compose for Postgres, Database for Postgres, ou Db2)
et une base de données dans le menu déroulant **Base de données**, puis un **schéma** :

    {{site.data.keyword.aios_short}} utilise une base de données PostgreSQL ou Db2 pour stocker
les données se rapportant aux modèles (données de commentaires, contenu d'évaluation) et les métriques calculées. Les forfaits Db2 Lite ne sont pas pris en charge actuellement. Pour plus d'informations sur les données de formation, voir [Pourquoi {{site.data.keyword.aios_short}} a-t-il besoin d'accéder à mes données de formation ?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)
    {: note}

    ![Sélection de la base de données](images/gs-config-database3.png)

1.  Vous pouvez également cliquer sur **Sélectionner un autre emplacement**
et spécifier un emplacement de base de données en dehors de votre compte {{site.data.keyword.Bluemix_notm}}.

    {{site.data.keyword.aios_short}} utilise une base de données PostgreSQL ou Db2 pour stocker
les données se rapportant aux modèles (données de commentaires, contenu d'évaluation) et les métriques calculées. Les forfaits Db2 Lite ne sont pas pris en charge actuellement.
    {: note}

    - Sélectionnez le **Type de base de données**
(`Compose for PostgreSQL`, `Database for PostgreSQL` ou `Db2`),
puis fournissez les informations de connexion :

        - Pour une base de données `Compose for PostgreSQL`, indiquez les informations suivantes :

            - Nom d'hôte ou adresse IP
            - Port
            - Base de données (nom)
            - Nom d'utilisateur
            - Mot de passe

            ![Spécification d'un emplacement de base de données Compose for Postgres](images/db-config-cpostgres.png)

        - Pour une base de données `Database for PostgreSQL`, indiquez les informations suivantes :

            - Nom d'hôte ou adresse IP
            - Port SSL
            - Certificat codé en base 64
            - Base de données (nom)
            - Nom d'utilisateur
            - Mot de passe

            ![Spécification d'un emplacement de base de données Database for Postgres](images/db-config-dpostgres.png)

        - Pour une base de données `Db2`, indiquez les informations suivantes :

            - Nom d'hôte ou adresse IP
            - Port SSL
            - Base de données (nom)
            - Nom d'utilisateur
            - Mot de passe

            ![Spécification d'un emplacement Db2](images/db-config-db2.png)

    - Une fois connecté, vous pouvez sélectionner un schéma.

      Le nom du schéma doit être indiqué explicitement si vous fournissez une instance de Db2 avec accès limité, ce qui ne permet pas la génération automatique du nom de schéma. Cela s'applique au forfait Entry Db2 Warehouse.
      {: important}

      ![Sélection du schéma](images/gs-config-database5.png)

1.  Cliquez sur **Suivant**, vérifiez le récapitulatif et cliquez sur **Enregistrer**.

## Envoi d'une demande d'évaluation
{: #cdb-score}

Pour configurer les moniteurs, {{site.data.keyword.aios_short}} requiert que vous envoyiez un contenu d'évaluation,
afin de commencer à journaliser les données qui seront surveillées.

Pour les modèles déployés dans {{site.data.keyword.pm_full}}, évaluez simplement votre déploiement,
{{site.data.keyword.pm_short}} envoie automatiquement le contenu d'évaluation à {{site.data.keyword.aios_short}}.
Pour les autres moteurs d'apprentissage automatique, comme Microsoft Azure, Amazon SageMaker ou un moteur d'apprentissage automatique personnalisé,
le contenu d'évaluation doit être envoyé avec l'API de journalisation de contenu.

Sélectionnez un déploiement, ici "Fraud Detector", puis utilisez les fragments de code `cURL` ou `Python` fournis
pour journaliser les données de demande et de réponse de déploiement de modèle. Pour plus de détails, voir [Journalisation du contenu pour les instances de service non-Watson Machine Learning](/docs/services/ai-openscale?topic=ai-openscale-cml-connect).

Les zones et les valeurs des fragments de code doivent être remplacées par vos valeurs réelles, car les valeurs fournies ne sont que des exemples.
{: important}

![Sélection de la base de données](images/config-send-scoring.png)

Une fois que vous aurez exécuté votre journalisation du contenu, vous verrez une coche dans la colonne "Prêt à surveiller" pour le déploiement sélectionné. Cliquez sur **Configurer les moniteurs** pour continuer.

## Etapes suivantes
{: #cdb-next}

{{site.data.keyword.aios_short}} est maintenant prêt
à ce que vous [configuriez les moniteurs pour vos déploiements](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
