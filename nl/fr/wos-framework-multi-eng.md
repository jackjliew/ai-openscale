---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: multiple engines, non-Watson, machine learning, frameworks, provision

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

# Possibilité de moteurs d'apprentissage automatique multiples
{: #fmrk-workaround-multmleng}

{{site.data.keyword.aios_short}} accepte plusieurs moteurs d'apprentissage automatique au sein d'une même instance. Vous pouvez les ajouter via la configuration du tableau de bord {{site.data.keyword.aios_short}} ou le [SDK Python](http://ai-openscale-python-client.mybluemix.net/?cm_mc_uid=70732728440115575086192&cm_mc_sid_50200000=62539451560175957820).
{: shortdesc}

Lorsque vous avez configuré {{site.data.keyword.aios_short}} au départ,
vous avez peut-être utilisé l'interface utilisateur ou l'option de configuration automatisée
pour mettre à disposition votre premier moteur d'apprentissage automatique. L'ajout d'autres moteurs d'apprentissage automatique nécessite d'utiliser soit l'onglet Configuration du tableau de bord {{site.data.keyword.aios_short}}, soit le SDK Python.

## Utilisation du tableau de bord pour ajouter des fournisseurs
{: #fmrk-workaround-multmleng-dashboard}

1. Après avoir ouvert {{site.data.keyword.aios_short}}, dans l'onglet **Configurer**, cliquez sur le bouton **Ajouter des fournisseurs d'apprentissage automatique**.

   ![bouton d'ajout de fournisseurs dans la fenêtre des fournisseurs d'apprentissage automatique](images/wos-configure-multi-providers.png)

2. Cliquez sur le carreau du fournisseur que vous souhaitez ajouter, puis sur **Suivant**.

   ![l'écran de sélection des fournisseurs d'apprentissage automatique est affiché](images/wos-machine-learning-providers-selection.png)

3. Entrez les informations requises, telles que les identifiants, puis cliquez sur **Enregistrer**.

Une fois votre configuration enregistrée, possibilité vous est donnée d'aller au tableau de bord, de choisir des déploiements ou de configurer des moniteurs.

## Modification des fournisseurs d'apprentissage automatique
{: #fmrk-workaround-editingproviders-dashboard}

Vous avez besoin de modifier un fournisseur d'apprentissage automatique ?
Cliquez sur l'icône du menu de carreaux ![icône du menu de carreaux](images/v-three-dots.png) puis sur **Afficher et éditer les détails**.

   ![option d'affichage et d'édition des fournisseurs d'apprentissage automatique](images/wos-machine-learning-providers-edit.png)

## Ajout de fournisseurs d'apprentissage automatique en utilisant la méthode de liaison (binding) du SDK Python
{: #fmrk-workaround-multmleng-binding}

Vous pouvez lier plusieurs moteurs d'apprentissage automatique à {{site.data.keyword.aios_short}}
en utilisant la méthode `client.data_mart.bindings.add` de l'API Python. 

### {{site.data.keyword.pm_full}}
{: #fmrk-workaround-multmleng-binding-wml}

- Pour lier le moteur d'apprentissage automatique {{site.data.keyword.pm_full}}, exécutez la commande suivante :

   `binding_uid = client.data_mart.bindings.add('WML instance', WatsonMachineLearningInstance(WML_CREDENTIALS))`

### Microsoft Azure ML Studio
{: #fmrk-workaround-multmleng-binding-azurestudio}

- Pour lier le moteur d'apprentissage automatique Azure ML Studio, exécutez la commande suivante :

  `binding_uid_2 = client.data_mart.bindings.add('My Azure ML Studio engine', AzureMachineLearningInstance(AZURE_ENGINE_CREDENTIALS))`

### Amazon Sagemaker
{: #fmrk-workaround-multmleng-binding-aws}

- Pour lier le moteur d'apprentissage automatique AWS Sagemaker, exécutez la commande suivante :

  `binding_uid_3 = client.data_mart.bindings.add('My AWS SageMaker engine', SageMakerMachineLearningInstance(SAGEMAKER_ENGINE_CREDENTIALS)) `

### Microsoft Azure ML Service
{: #fmrk-workaround-multmleng-binding-azureservice}

- Pour lier le moteur d'apprentissage automatique Azure ML Service, exécutez la commande suivante :

  `binding_uid_4 = client.data_mart.bindings.add('Mon moteur Azure ML Service', AzureServiceMachineLearningInstance(AZURE_SRVR_ENGINE_CREDENTIALS))`

### Production de la liste des fournisseurs d'apprentissage automatique
{: #fmrk-workaround-multmleng-binding-list}

Pour afficher la liste de toutes les liaisons, exécutez la méthode `list` :

`    client.data_mart.bindings.list()
    `


| uid | name | service_type | created |
|:---|:---:|:---:|:---:
| e88ms###-####-####-############ | Mon moteur Azure ML Service | azure_machine_learning | 2019-04-04T09:50:33.189Z |
| e88sl###-####-####-############ | Mon moteur Azure ML Studio | azure_machine_learning | 2019-04-04T09:50:33.186Z |
| e00sjl###-####-####-############ | Instance WML | watson_machine_learning | 2019-03-04T09:50:33.338Z |
| e43kl###-####-####-############ | Mon moteur AWS SageMaker | sagemaker_machine_learning | 2019-04-04T09:50:33.186Z |
{: caption="Tableau 1. Services liés" caption-side="top"}


Pour des informations sur les différents moteurs d'apprentissage automatique, consultez les rubriques suivantes :

- [Lier votre moteur d'apprentissage automatique personnalisé](/docs/services/ai-openscale?topic=ai-openscale-cml-cusbind#cml-cusbind).
- [Lier votre moteur d'apprentissage automatique Microsoft Azure Studio](/docs/services/ai-openscale?topic=ai-openscale-cml-azbind#cml-azbind)
- [Lier votre moteur d'apprentissage automatique Microsoft Azure Service](/docs/services/ai-openscale?topic=ai-openscale-cml-azsrvconfig#cml-azsrvbind)
- [Lier votre moteur d'apprentissage automatique Amazon SageMaker](/docs/services/ai-openscale?topic=ai-openscale-cml-smbind#cml-smbind)


Pour un exemple de bloc-notes fonctionnel, consultez [les exemples de bloc-note {{site.data.keyword.aios_short}}](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks).

