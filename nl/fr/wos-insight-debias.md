---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: fairness, monitoring, charts, de-biasing, bias, accuracy

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

# Options de débiaisement
{: #it-dbo}

{{site.data.keyword.aios_short}} utilise deux types de débiaisement : passif et actif. Le débiaisement passif vous permet de savoir comment vous avez étiez biaisé,
tandis que le débiaisement actif vous empêche de prolonger le biais en modifiant le modèle en temps réel pour l'application en cours.

- *Débiaisement passif* - le débiaisement passif est le travail qu'OpenScale effectue lui-même, automatiquement, toutes le heures. Il est considéré passif car il s'effectue sans intervention de l'utilisateur. Lorsque {{site.data.keyword.aios_short}} effectue un contrôle de biais, il effectue également un débiaisement des données,
en analysant le comportement du modèle et en identifiant les données où il agit de manière biaisée.

  {{site.data.keyword.aios_short}} construit ensuite un modèle d'apprentissage automatique pour
prévoir si le modèle risque d'agir de manière biaisée sur un nouveau point de données particulier. Puis il analyse les données reçues par le modèle, sur une heure,
et trouve les points de données où il pense que celui-ci agit de manière biaisée. Pour ces points de données, l'attribut d'équité est perturbé de la minorité à la majorité,
et les données perturbées sont envoyées au modèle initial pour prévision. Cette prévision du modèle initial est utilisée comme sortie débiaisée.

  {{site.data.keyword.aios_short}} effectue ce débiaisement toutes les heures,
sur toutes les données reçues par le modèle au cours de la dernière heure. Il calcule également l'équité de la sortie débiaisée et l'affiche dans l'onglet **Modèle débiaisé**.

- *Débiaisement actif* -
le débiaisement actif est une manière pour vous de demander des résultats débiaisés dans votre application via le point d'extrémité d'API REST. Vous demandez activement à {{site.data.keyword.aios_short}} d'exécuter un débiaisement et de modifier le modèle
pour que vous puissiez utiliser votre application d'une manière non biaisée. Dans le débiaisement actif, vous pouvez utiliser un point d'extrémité d'API REST de débiaisement depuis votre application. Ce point d'extrémité d'API REST appellera votre modèle en interne et contrôlera son comportement.

  Si {{site.data.keyword.aios_short}} détecte que le modèle agit de manière biaisée,
il perturbe les données comme indiqué précédemment et les renvoie au modèle initial. La sortie du modèle initial avec les données perturbées sera renvoyée comme prévision débiaisée. Si {{site.data.keyword.aios_short}} détermine que le modèle initial n'agit pas de manière biaisée,
il renverra la prévision de celui-ci comme prévision débiaisée. Ainsi, en utilisant ce point d'extrémité d'API REST,
vous pouvez faire en sorte que votre application ne prenne pas de décisions basées sur une sortie biaisée de vos modèles.

Pour trouver votre point d'extrémité d'API REST de débiaisement, sélectionnez le lien **Point d'extrémité d'évaluation débiaisée**

![Ecran de détails du point d'extrémité d'API de débiaisement avec l'exemple cURL dans la zone de fragment de code](images/insight-debias-api.png)

## Etapes suivantes
{: #it-dbo-nextsteps}

- Pour atténuer le biais, après sa détection, vous devez générer une nouvelle version du modèle qui corrige le problème.
{{site.data.keyword.aios_short}} stocke les enregistrements biaisés dans la table d'étiquetage manuel.
Vous devez les étiqueter manuellement puis former à nouveau le modèle avec ces données supplémentaires
pour en générer une nouvelle version non biaisée.


