---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: accuracy, 

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

# Configuration du moniteur de détection de dérive ![étiquette bêta](images/beta.png)
{: #behavior-drift-config}

Le moniteur de dérive {{site.data.keyword.aios_full}} ne peut commencer à analyser votre modèle que lorsque vous l'avez configuré. Vous pouvez soit entraîner votre modèle en ligne, soit utiliser un bloc-notes.
{: shortdesc}

Vous pouvez entraîner votre modèle en ligne avec {{site.data.keyword.aios_short}} si vous utilisez {{site.data.keyword.pm_full}} et que vos données ne dépassent pas 500 Mo. Sinon, vous devez utiliser un bloc-notes.

## Etapes pour configurer la détection de dérive dans {{site.data.keyword.aios_short}}
{: #behavior-drift-config-steps-wos}

Si vous utilisez {{site.data.keyword.pm_full}}, vous avez la possibilité de configurer la détection de dérive avec l'interface utilisateur de {{site.data.keyword.aios_short}}.

1. Dans l'onglet **Dérive**, page **Qu'est-ce que la dérive ?** , cliquez sur **Commencer** pour démarrer le processus de configuration.

   ![Page Qu'est-ce que la dérive ?](images/wos-drift-config-1.png)

2. Cliquez sur le carreau **Entraîner dans Watson OpenScale**.

   ![Page Qu'est-ce que la dérive ?](images/drift-config-2.png)

3. Fixez le seuil d'alerte.

   ![Page Qu'est-ce que la dérive ?](images/drift-config-3.png)

3. Fixez la taille d'échantillon.

   ![Page Qu'est-ce que la dérive ?](images/drift-config-4.png)
   
3. Cliquez sur **Enregistrer**.


## Etapes pour configurer la détection de dérive à l'aide d'un bloc-notes
{: #behavior-drift-config-steps-ntbk}

Si vous utilisez un fournisseur d'apprentissage automatique autre que {{site.data.keyword.pm_full}}, tel que Microsoft Azure, Amazon SageMaker ou un moteur d'apprentissage automatique personnalisé, vous devez configurer la détection de dérive à l'aide d'un bloc-notes. Notez que l'utilisation d'un bloc-notes pour configurer la détection de dérive est également possible si vous utilisez {{site.data.keyword.pm_full}} comme fournisseur d'apprentissage automatique.

Cette option est utile si les données d'entraînement ne sont pas stockées dans Db2 ni dans {{site.data.keyword.cos_full}}. Avec un bloc-notes, vous devez lire les données d'entraînement dans un dataframe (cadre de données). Le bloc-notes spécialisé que vous pouvez télécharger depuis {{site.data.keyword.aios_short}} crée une sortie spécialisée que vous pouvez remonter vers {{site.data.keyword.aios_short}}.

1. Créez un bloc-notes pour générer le modèle de détection de dérive. Utilisez [l'exemple de bloc-notes](https://github.com/IBM-Watson/aios-data-distribution/blob/master/training_statistics_notebook.ipynb) disponible dans l'interface utilisateur de {{site.data.keyword.aios_short}}.
2. Utilisez un outil de compression pour compresser le modèle de détection de dérive en un fichier .tar.gz.

1. Dans l'onglet **Dérive**, page **Qu'est-ce que la dérive ?** , cliquez sur **Commencer** pour démarrer le processus de configuration.

   ![Page Qu'est-ce que la dérive ?](images/wos-drift-config-1.png)

2. Cliquez sur le carreau **Entraîner dans un bloc-notes**.

   ![Page de configuration de la dérive avec une option en ligne et une option bloc-notes](images/drift-config-2.png)

3. Faites glisser le fichier du modèle compressé jusqu'à la zone cible ou recherchez-le et sélectionnez-le dans votre système de fichiers, puis cliquez sur **Suivant**.

   ![Page Qu'est-ce que la dérive ?](images/wos-drift-config-2b.png)
   
3. Remontez le modèle de détection de dérive et cliquez sur **Suivant**.

   ![Page Qu'est-ce que la dérive ?](images/drift-config-upload.png)
   
3. Fixez le seuil d'alerte.

   ![Page Qu'est-ce que la dérive ?](images/drift-config-3.png)

3. Fixez la taille d'échantillon.

   ![Page Qu'est-ce que la dérive ?](images/drift-config-4.png)
   
3. Cliquez sur **Enregistrer**.

## Etapes suivantes
{: #behavior-drift-config-next-steps}

- Pour plus d'information sur l'interprétation de la dérive, voir [Ampleur de la dérive](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-ovr)
