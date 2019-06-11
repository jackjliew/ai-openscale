---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: accuracy, 

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

# Exactitude
{: #acc-monitor}

L'exactitude vous permet de savoir si votre modèle prévoit bien les résultats.
{: shortdesc}

## Comprendre l'exactitude
{: #acc-understand}

L'exactitude peut signifier différentes choses selon le type de l'algorithme :

- *Classification multi-classes* :
L'exactitude mesure le nombre de fois qu'une classe quelconque a été prévue correctement, normalisé par le nombre de points de données. Pour plus de détails, voir
[Multi-class classification
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#multiclass-classification){: new_window}
dans la documentation d'Apache Spark.

- *Classification binaire* :
Pour un algorithme de classification binaire, l'exactitude est mesurée comme la zone située sous une courbe ROC. Pour plus de détails, voir
[Binary classification
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#binary-classification){: new_window}
dans la documentation d'Apache Spark.

- *Régression* :
Les algorithmes de régression sont mesurés à l'aide du coefficient de détermination, ou R2. Pour plus de détails, voir
[Regression model evaluation
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://spark.apache.org/docs/2.1.0/mllib-evaluation-metrics.html#regression-model-evaluation){: new_window}
dans la documentation d'Apache Spark.

### Fonctionnement
{: #acc-works}

Vous devez ajouter des données de commentaires étiquetées manuellement via l'interface utilisateur {{site.data.keyword.aios_short}} comme indiqué ci-dessous,
avec un [client Python
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://ai-openscale-python-client.mybluemix.net/#feedbacklogging){: new_window}
ou une [API REST
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/apidocs/ai-openscale#post-feedback-payload){: new_window}.

Reportez-vous aux [Infrastructures prises en charge](/docs/services/ai-openscale?topic=ai-openscale-in-ov#in-fram)
pour connaître les limitations de la surveillance de l'exactitude.

### Exactitude débiaisée
{: #acc-debias-view}

Lorsqu'il y a des données pour, l'exactitude du modèle comprend à la fois le modèle d'origine et le modèle débiaisé. {{site.data.keyword.aios_full_notm}} calcule l'exactitude pour la sortie débiaisée et l'enregistre dans la table de journalisation de contenu
sous la forme d'une colonne additionnelle.

![affichage d'un modèle avec l'exactitude calculée à la fois pour le modèle d'origine et le modèle débiaisé.](images/debiased-accuracy.png)

## Configuration du moniteur d'exactitude
{: #acc-config}

1.  Sur la page *Qu'est-ce que l'exactitude ?*, cliquez sur **Suivant** pour démarrer le processus de configuration.

    ![Page Qu'est-ce que l'exactitude ?](images/accuracy-what-is.png)

1.  Sur la page *Définir le seuil d'exactitude*, sélectionnez une valeur représentant un niveau d'exactitude acceptable.

    L'exactitude est une valeur synthétisée à partir de métriques pertinentes de sciences des données pour chaque type de modèle particulier. Le score est une mesure normalisée qui vous permet de la comparer facilement entre différents types de modèle. Dans les cas ordinaires, un score d'exactitude de 80 est suffisant.
    {: note}

    ![Définir la limite d'exactitude](images/accuracy-set-limit.png)

    Cliquez sur **Suivant** pour continuer.

1.  Maintenant, définissez les tailles d'échantillon minimale et maximale. La taille minimale empêche de mesurer l'exactitude
tant qu'un nombre minimum d'enregistrements n'est pas disponible dans l'ensemble de données d'évaluation,
afin que les résultats ne risquent pas d'être faussés. La taille maximale aide à mieux gérer le temps et l'effort nécessaires à l'évaluation de l'ensemble de données ;
si elle est dépassée, seuls les enregistrements les plus récents sont évalués.

     ![Configurer la taille d'échantillon](images/accuracy-config-sample.png)

1.  Cliquez sur le bouton **Suivant**.

    Un récapitulatif de vos sélections est présenté pour vérification. Pour changer quoi que ce soit, cliquez sur le lien **Modifier** correspondant.

1.  Cliquez sur **Enregistrer** pour achever la configuration.

Vous avez maintenant la possibilité de fournir directement des données de commentaires à votre modèle, pour l'évaluation de l'exactitude.

  ![Envoyer des données de commentaires](images/accuracy-send-feedback0.png)

Cliquez sur le bouton *Ajouter des données de commentaires* pour télécharger un fichier de données au format CSV ;
définissez le délimiteur pour qu'il corresponde à vos données.

Le fichier CSV de commentaires doit avoir toutes les valeurs de fonction, ainsi que la valeur cible/libellé affectée manuellement. Par exemple, les données de formation du modèle de médicaments contiennent les valeurs de fonction
`"AGE"`, `"SEX"`, `"BP"`, `"CHOLESTEROL"`,`"NA"`,`"K"`
et la valeur cible/libellé `"DRUG"`. Le fichier CSV de commentaires doit comprendre des valeurs pour ces zones ;
par exemple : `[43, M, HIGH, NORMAL, 0.6345, 1.4587, DrugX]`. Si un en-tête est fourni pour le fichier CSV de commentaires, les noms de zone sont mappés à partir de lui. Sinon, l'ordre des zones **DOIT** doit être exactement le même que dans le schéma de formation. Pour plus d'informations sur les données de formation, voir [Pourquoi {{site.data.keyword.aios_short}} a-t-il besoin d'accéder à mes données de formation ?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)
{: important}

Notez que les types de prévision renvoyés par votre modèle et la colonne libellé/cible de vos données de commentaires doivent correspondre.
{: note}

  ![Délimiteur d'exactitude](images/accuracy-delimit.png)

La taille de fichier est actuellement limitée à 8 Mo.
{: note}

Vous pouvez également publier les données de commentaires à l'aide des fragments de code `cURL` ou `Python` fournis.

Les zones et les valeurs des fragments de code doivent être remplacées par vos valeurs réelles, car les valeurs fournies ne sont que des exemples.
{: important}

Vous pouvez également sauter cette étape facultative en sélectionnant **Quitter** ;
vous pourrez télécharger un fichier CSV pour l'évaluation ultérieurement.

### Etapes suivantes
{: #acc-next}

Sur la page *Configurer les moniteurs*, vous pouvez sélectionner une autre catégorie de surveillance.
