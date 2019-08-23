---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits

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
{:external: target="_blank" .external}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:faq: data-hd-content-type='faq'}

# Problèmes et limitations connus de {{site.data.keyword.aios_short}}
{: #rn-12ki}

Les listes qui suivent répertorient les problèmes et limitations connus d'{{site.data.keyword.aios_full}} et d'{{site.data.keyword.wos4dfull}}.
{: shortdesc}

<p>&nbsp;</p>

## Limitations
{: #wos-limitations}

- {{site.data.keyword.aios_short}} peut prendre en charge plusieurs moteurs d'apprentissage automatique
à condition que vous configuriez les moteurs supplémentaires avec le SDK Python.

- L'édition actuelle ne prend en charge qu'une seule base de données, une seule instance d'{{site.data.keyword.pm_full}}
et une seule instance de {{site.data.keyword.aios_short}}

- La base de données et l'instance d'{{site.data.keyword.pm_full}} doivent être déployées dans le même compte {{site.data.keyword.cloud_notm}}.

- Le forfait Lite (gratuit) comporte les limites mensuelles suivantes :

    - Deux modèles déployés surveillés
    - 20 transactions expliquées
    - 50 000 enregistrements de contenu utile (cumulés)
    - 50 000 enregistrements de retour (cumulés)

- {{site.data.keyword.aios_short}} utilise une base de données PostgreSQL ou Db2 pour stocker
les données se rapportant aux modèles (données de retour, contenu utile d'évaluation) et les métriques calculées. Les forfaits Db2 Lite ne sont pas pris en charge actuellement.

- Il y a une limite de licence de 20 modèles déployés par instance de {{site.data.keyword.aios_short}}.

- Pour {{site.data.keyword.pm_full}}, l'entrée d'évaluation pour les modèles de classification d'image envoyés pour journalisation de contenu utile ne peut pas dépasser 1 Mo. Afin d'éviter des problèmes de dépassement de délai, les images ne doivent pas dépasser 125 x 125 pixels
et doivent être envoyées séquentiellement pour que l'explication de la seconde image soit demandée lorsque la première est terminée.

- La base de données gratuite du forfait Lite n'est pas en conformité avec le RGPD. Si votre modèle traite des informations à caractère personnel,
vous devez acheter une nouvelle base de données ou utiliser une base de données existante conforme au RGPD. 

- L'explicabilité pour les modèles de texte non structuré n'est pas prise en charge
pour les langues à écriture continue, comme le japonais, le chinois ou le coréen,
qui n'utilisent pas d'espaces ni de caractères de ponctuation pour séparer les mots.



<p>&nbsp;</p>

## Problèmes courants
{: #wos-common-issues}

Les problèmes suivants sont communs à {{site.data.keyword.aios_full}} sur {{site.data.keyword.Bluemix}} et {{site.data.keyword.wos4d_full}}.

<p>&nbsp;</p>

### Des erreurs dans la configuration de détection de la dérive empêchent de configurer le moniteur de dérive
{: #wos-common-issues-mismatchdatatype}

La souplesse de l'écran de configuration du modèle peut également entraîner des problèmes lors de la configuration ultérieure des moniteurs, tels que le moniteur de détection de dérive. Comme vous pouvez choisir les types de données, vous devez veiller à ce que vos choix reflètent le modèle original. L'erreur suivante risque de se produire si le type de la colonne de prévision n'est pas correctement sélectionné :

```
"error": AIQDS2003E",
"message": "The model predictions '[0. 1.]' are different from class names in training data '['No' 'Yes']' for the subscription <<number>> in datamart <<datamart ID>> and service binding <<binding ID>>.
```

Les cas suivants sont la cause la plus probable :

- L'étiquette `class` est du type chaîne (string) et la **prediction**
`modeling_role` est affectée à la colonne **prediction** en tant que type double, car c'est ainsi que le schéma des données
de sortie est défini.
- Vous sélectionnez la colonne **prediction** du type double dans l'interface utilisateur, ce qui n'est pas interdit.


### Formats de contenu utile
{: #wos-common-issues-payloadformat}

Pour le bon traitement des analyses de contenu utile, {{site.data.keyword.aios_short}} n'accepte pas les noms de colonne
avec des guillemets (") dans le contenu utile. Cela concerne à la fois le contenu utile d'évaluation et les données de retour au format CSV ou JSON.

<p>&nbsp;</p>



### Microsoft Azure ML Studio
{: #wos-common-issues-msazure}

- Des deux types de services web Azure Machine Learning, seul le `nouveau` est accepté par {{site.data.keyword.aios_short}}. Le type `classique` ne l'est pas.

- __*Il faut utiliser le nom d'entrée par défaut*__ :
Dans le service web Azure, le nom d'entrée par défaut est `"input1"`. Cette zone est actuellement obligatoire pour {{site.data.keyword.aios_short}}, qui ne peut pas fonctionner si elle manque.

  Si votre service web Azure n'utilise pas le nom par défaut, remplacez le nom d'entrée par `"input1"` et le code fonctionnera.

- Si l'appel de Microsoft Azure ML Studio pour afficher les modèles d'apprentissage automatique
dépasse le délai d'attente maximum de la réponse,
par exemple si vous avez beaucoup de services web, vous devez augmenter les valeurs d'attente maximum. Par exemple, si vous utilisez l'équilibreur de charge HAProxy,
il est peut-être nécessaire de contourner ce problème en émettant les commandes suivantes :

   - Connectez-vous au noeud de l'équilibreur de charge et mettez à jour `/etc/haproxy/haproxy.cfg` pour remplacer le délai client et serveur de `1m` par `5m`:

       ```bash
       timeout client           5m
       timeout server           5m
      ```

   - Exécutez la commande `systemctl restart haproxy` pour redémarrer l'équilibreur de charge HAProxy.

Si vous utilisez un équilibreur de charge autre que HAProxy, vous devrez peut-être ajuster les valeurs de délai de la même manière.
      {: note}

- Des deux types de services web Azure Machine Learning, seul le `nouveau` est accepté par {{site.data.keyword.aios_short}}. Le type `classique` ne l'est pas.

- Dans le service Web Azure, le nom d'entrée par défaut est `"input1"`. Cette zone est actuellement obligatoire pour {{site.data.keyword.aios_short}} et son absence fait échouer la surveillance de l'exactitude.

   Si votre service web Azure n'utilise pas le nom par défaut, remplacez le nom d'entrée par `"input1"`.

<p>&nbsp;</p>


### Amazon SageMaker
{: #wos-common-issues-aws}

- __*L'algorithme BlazingText n'est pas pris en charge*__ :
Le format de contenu utile d'entrée de l'algorithme Amazon SageMaker BlazingText n'est pas pris en charge dans l'édition actuelle de {{site.data.keyword.aios_short}}.

<p>&nbsp;</p>


### Instance de service d'apprentissage automatique personnalisé
{: #wos-common-issues-custom}

- Avec le [module Python](/docs/services/ai-openscale?topic=ai-openscale-as-module),
l'explicabilité ne fonctionne pas pour l'instance de service personnalisée. Ceci est dû au fait que l'instance de service personnalisée requiert une prévision numérique dans les données de réponse,
qui n'est pas incluse avec le script du module.

<p>&nbsp;</p>


- **Fragments de code non valides**

    - Les fragments de code cURL et Python fournis pour la configuration des moniteurs sont tous deux non valides. Les fragments de code corrects sont fournis ici :

      *Journalisation de contenu utile*

      ```cURL
      # Génération d'un jeton d'accès ICP en transmettant un nom d'utilisateur ($USERNAME) et un mot de passe ($PASSWORD) ICP dans la demande suivante

      curl -k -X GET \
      -user "$USERNAME:$PASSWORD" \
      "https://{{icp_hostname}:{{icp_port}}/v1/preauth/validateAuth"

      # la demande CURL précédente renverra un jeton auth sous "accessToken", que vous utiliserez pour {icp_token} dans la demande suivante de journalisation de contenu utile
      # A FAIRE : définir manuellement et transmettre :
      # request - entrée du point d'extrémité d'évaluation dans un format accepté par {{site.data.keyword.aios_short}} - remplacer les exemples de zones et de valeurs par ce qui convient
      # response - sortie du modèle évalué dans un format accepté par {{site.data.keyword.aios_short}} - remplacer les exemples de zones et de valeurs par ce qui convient
      # - $SCORING_ID - ID de la transaction d'évaluation
      # - $SCORING_TIME - Temps (ms) pris par la prévision (pour la surveillance des performances)

      SCORING_PAYLOAD='[{
        "scoring_id": "$SCORING_ID",
        "response_time": "$SCORING_TIME",
        "request": {
          "fields": ["AGE", "SEX", "BP", "CHOLESTEROL", "NA", "K"],
          "values": [[28, "F", "LOW", "HIGH", 0.61, 0.026]]
      },
      "response": {
        "fields": ["AGE", "SEX", "BP", "CHOLESTEROL", "NA", "K", "probability", "prediction", "DRUG"],
        "values": [[28, "F", "LOW", "HIGH", 0.61, 0.026, [0.82, 0.07, 0.0, 0.05, 0.03], 0.0, "drugY"]]
        },
        "binding_id": "{{binding_id}}",
        "subscription_id": "{{subscription_id}}",
        "deployment_id": "{{deployment_id}}"
      }]'

      curl -k -X POST https://{{icp_hostname}:{{icp_port}}/v1/data_marts/{{data_mart_id}}/scoring_payloads -d "$SCORING_PAYLOAD" \
      --header 'Content-Type: application/json' --header 'Accept: application/json' --header "Authorization: Bearer $ICP_TOKEN"
      ```

      *Journalisation des retours*

      ```cURL
      # Génération d'un jeton d'accès ICP en transmettant un nom d'utilisateur ($USERNAME) et un mot de passe ($PASSWORD) ICP dans la demande suivante

      curl -k -X GET \
      --user "$USERNAME:$PASSWORD" \
      "https://{{icp_hostname}:{{icp_port}}/v1/preauth/validateAuth"

      # la demande CURL précédente renverra un jeton auth sous "accessToken", que vous utiliserez pour {icp_token} dans la demande suivante de journalisation de contenu utile
      # A FAIRE : définir manuellement et transmettre :
      # fields - liste de noms de zone - remplacer les exemples de valeur par ce qui convient
      # values - enregistrements de données de retour - remplacer les exemples de valeur par ce qui convient
      # - $SCORING_ID - ID de la transaction d'évaluation
      # - $SCORING_TIME - Temps (ms) pris par la prévision (pour la surveillance des performances)

      FEEDBACK_DATA='{
        "fields": ["AGE", "SEX", "BP", "CHOLESTEROL", "NA", "K", "DRUG"],
        "values": [[28, "F", "LOW", "HIGH", 0.61, 0.026, "drugB"]],
        "binding_id": "{{binding_id}}",
        "subscription_id": "{{subscription_id}}"
      }'

      curl -k -X POST https://{{icp_hostname}:{{icp_port}}/v1/data_marts/{{data_mart_id}}/feedback_payloads -d "$FEEDBACK_DATA" \
      --header 'Content-Type: application/json' --header 'Accept: application/json' --header "Authorization: Bearer $ICP_TOKEN"
      ```

    - Le fragment de code Java fourni pour le point d'extrémité de débiaisement n'est pas valide. Le fragment de code correct est fourni ici :

      *Point d'extrémité de débiaisement*

      ```java
      /**
      Au moment de l'exécution, vous devez remplacer les valeurs des paramètres suivants :

      <HOSTNAME> - Nom d'hôte, par exemple aiopenscale.test.cloud.ibm.com
      <PORT> - Port du serveur
      <DATA_MART_ID> - ID du magasin de données
      <SERVICE_BINDING_ID> - ID de la liaison de service
      <ASSET_ID> - ID d'actif ou ID de modèle
      <DEPLOYMENT_ID> - ID du déploiement
      <TOKEN> - Jeton bearer

      */
      import org.apache.http.HttpVersion;
      import org.apache.http.client.fluent.Request;
      import org.apache.http.entity.ContentType;

      String bearerToken = "Bearer <TOKEN>";
      String URL = "https://<HOSTNAME>:<PORT>/v1/data_marts/<DATA_MART_ID>/service_bindings/<SERVICE_BINDING_ID>/subscriptions/<ASSET_ID>/deployments/<DEPLOYMENT_ID>/online";

      String payload = "{ \"fields\": [ \"field1\", \"field2\", \"field3\" ], \"values\": [ [ \"field1Value1\", \"field2Value1\", \"field3Value1\" ], [ \"field1Value2\", \"field2Value2\", \"field3Value2\" ]] }";

      byte[] res = Request.Post(URL).addHeader("Authorization", bearerToken).useExpectContinue().version(HttpVersion.HTTP_1_1)
                .bodyString(payload, ContentType.APPLICATION_JSON).execute().returnContent().asBytes();
      ```

<p>&nbsp;</p>


## Problèmes connus de {{site.data.keyword.wos4d_notm}}
{: #rn-16April2019ki}

Les problèmes suivants sont spécifiques à {{site.data.keyword.wos4d_full}}.

<p>&nbsp;</p>

### Microsoft Azure Machine Learning Service
{: #icp4d-azure-service-status403}

Lors de l'utilisation d'{{site.data.keyword.wos4d_full}}, il peut arriver que {{site.data.keyword.aios_short}} ne parvienne pas à communiquer avec Azure Machine Learning Service alors qu'il a besoin d'appeler les points d'extrémité d'évaluation du déploiement. Les outils de sécurité qui mettent en application vos politiques de sécurité d'entreprise, tels que Symantec Blue Coat, peuvent empêcher un tel accès.

Si vous constatez des erreurs indiquant que l'évaluation par rapport à Azure Machine Learning Service ne peut être jointe (par exemple, si vous recevez un code d'état HTTP 403), vérifiez les politiques de sécurité de votre entreprise et veillez à ce que l'URL des points d'extrémité d'évaluation soit correctement re-catégorisée avec les outils utilisés, selon nécessité, pour permettre à {{site.data.keyword.aios_short}} d'accéder normalement à ces points d'extrémité.

<p>&nbsp;</p>


### IBM SPSS Collaboration and Deployment Services (C&DS)
{: #rn-16April2019ki-icp-spss}

- **Prise en charge limitée de l'explicabilité**

   - L'explicabilité est prise en charge pour les modèles binaires et pour les modèles multi-classes SPSS qui renvoient une probabilité pour chacune des classes. 
   - L'explicabilité n'est pas prise en charge pour les modèles multi-classes SPSS qui ne renvoient que la probabilité de la classe gagnante.



<p>&nbsp;</p>




- **IBM SPSS Collaboration and Deployment Services (C&DS) (type binaire uniquement) nécessite une demande de contenu utile supplémentaire**

    - Pour les abonnements binaires d'IBM SPSS Collaboration & Deployment Services,
vous devez faire une autre [demande de journalisation de contenu utile (évaluation)](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-cdb-connect#cdb-scoring)
après la  [préparation des moniteurs pour un déploiement](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mo-config#mo-config)
ou une fois tous les moniteurs configurés. Cela garantit l'exactitude de l'[explicabilité](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-ie-ov#ie-ov).

<p>&nbsp;</p>


- Le nombre d'enregistrements corrigés par **IBM SPSS C&DS (type binaire uniquement) peut être incorrect**

    - Pour les abonnements binaires IBM SPSS Collaboration & Deployment Services,
le nombre d'*enregistrements corrigés* peut ne pas être exact
quand il est affiché avec le bouton **Afficher les transactions**.

<p>&nbsp;</p>

### Métriques
{: #rn-16April2019ki-icp-metrics}

- **Métriques de performances d'{{site.data.keyword.pm_full}} non collectées**

    - Dans un environnement Cloud Pak for Data, les métriques de performances d'{{site.data.keyword.pm_full}} ne sont pas collectées.

<p>&nbsp;</p>

- **Limitations de la prise en charge de l'explicabilité**

    - Lors de la génération de vos modèles, n'incluez pas la colonne cible (libellé) issue de la demande d'évaluation en entrée. Si le modèle exige que la colonne cible soit incluse dans la demande d'entrée, le contrôle de biais, le débiaisement et l'explicabilité ne fonctionneront pas.


<p>&nbsp;</p>


### Fonctions Python
{: #rn-16April2019ki-icp-python}

- **Fonctions Python non prises en charge**

    - Le contrôle de biais, le débiaisement et l'explicabilité ne sont pas pris en charge pour les fonctions Python dans l'édition actuelle.

<p>&nbsp;</p>


### Installation et configuration
{: #rn-16April2019ki-icp-install}


- **Le script de désinstallation ne supprime pas les rubriques Kafka**

    - L'exécution du script de désinstallation ne supprime pas les rubriques Kafka {{site.data.keyword.aios_short}} créées dans EventStream lors de l'installation.

<p>&nbsp;</p>

### Bases de données
{: #rn-16April2019ki-icp-dbs}

- **Limitation de la taille des lignes avec Db2 Warehouse**

    - La taille des lignes est limitée à 1 Mo avec Db2 Warehouse. Lorsqu'il existe plusieurs colonnes de texte (plus de 30) (32 000 octets pour chaque VARCHAR), la limite est dépassée. Cette limitation est particulièrement sensible avec Amazon SageMaker car dans le format natif SageMaker, toutes les colonnes sont au format chaîne de caractères.

       Comme {{site.data.keyword.aios_short}} utilise l'esapce de tables par défaut pour la création des objets de base de données,
les limites effectives dépendent de la configuration de votre base de données. Pour plus d'information sur cette limitation, consultez la
[documentation Db2 sur IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/SSEPGG_11.1.0/com.ibm.db2.luw.sql.ref.doc/doc/r0001029.html).





## Navigateurs pris en charge
{: #abt-browser}

Les outils du service {{site.data.keyword.aios_short}} nécessitent le même niveau de navigateur qu'{{site.data.keyword.cloud_notm}}. Pour le détail, consultez la rubrique {{site.data.keyword.cloud_notm}} [Prérequis](/docs/overview?topic=overview-prereqs-platform#browsers).

<p>&nbsp;</p>


## Client Python
{: #abt-python}

Le [client Python {{site.data.keyword.aios_short}}](http://ai-openscale-python-client.mybluemix.net/){: external}
est une bibliothèque Python qui vous permet de travailler directement avec le service {{site.data.keyword.aios_short}}. Vous pouvez l'utiliser, à la place de l'interface utilisateur client {{site.data.keyword.aios_short}},
pour configurer la base de données de magasin de données, lier votre moteur d'apprentissage automatique, et sélectionner et surveiller des déploiements directement. Pour des exemples utilisant le client Python ainsi, consultez les
[exemples de bloc-note {{site.data.keyword.aios_short}}](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks).

<p>&nbsp;</p>
## Etapes suivantes
{: #abt-next}

- [Initiez-vous](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-gs-get-started) au service.
- [](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-gettingstarted)
- Consulter la [documentation de référence de l'API](https://{DomainName}/apidocs/ai-openscale){: external}.

Vous avez encore des questions ? 

- [Nouveautés dans {{site.data.keyword.wos4dfull}}](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-rn-relnotes)
- [Contacter IBM](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson){: external}.
