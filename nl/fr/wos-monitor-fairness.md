---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: fairness, fairness monitor, payload, perturbation, training data, debiased

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

# Configuration du moniteur d'équité
{: #mf-monitor}

Dans {{site.data.keyword.aios_full}}, le moniteur d'équité analyse les biais dans votre déploiement,
afin de garantir des résultats équitables entre les différentes populations.
{: shortdesc}

## Procédure
{: #mf-config}

Dans l'onglet **Equité**, sur la page **Qu'est-ce que l'équité ?**, cliquez sur **Commencer** pour démarrer le processus de configuration.

![Page Qu'est-ce que l'équité ?](images/fair-what-is.png)

Tout au long de ce processus, {{site.data.keyword.aios_full}} analyse votre modèle et fait des recommandations basées sur le résultat le plus logique. Sur les pages successives de l'onglet **Equité**, vous devez effectuer les opérations suivantes :

1. Sélectionnez les fonctions à surveiller. Seules sont prises en charge les caractéristiques qui sont de type de données d'équité catégoriel, numérique (entier), flottant ou double. Les caractéristiques qui ont un autre type de données ne sont pas prises en charge.

1. Spécifiez le groupe de référence et le groupe surveillé.

   Chaque caractéristique a des exigences spécifiques à configurer. Par exemple, si vous choisissez `age` pour l'une des caractéristiques à surveiller,
vous devez définir la plage d'âge d'un **Groupe de référence** et celle d'un **Groupe surveillé**
en entrant les valeurs directement dans chaque groupe.

1.  Définissez le seuil d'alerte d'équité pour la caractéristique.

    Un seuil d'équité sert à spécifier une différence acceptable entre le pourcentage de résultats favorables pour le groupe surveillé
et pour le groupe de référence.

    Considérez un modèle qui prévoit qui doit obtenir un prêt (`favorable outcome=loan granted`)
et qui ne doit pas (`unfavorable outcome=loan denied`). D'autre part, la valeur surveillée pour l'âge est `[18,25]` et la valeur de référence, `[26,100]`. Lors de l'exécution de l'algorithme de détection de biais, s'il trouve que le pourcentage de résultats favorables pour les personnes du groupe d'âge `[18,25]`
dans les `N` derniers enregistrements plus les données perturbées est de `50 %` 
tandis qu'il est de `70 %` pour le groupe d'âge `[26,100]`,
l'équité sera 50*100/70 = 71,42.

    Si le seuil d'équité est réglé à 80 %, l'algorithme marquera le modèle comme biaisé
car l'équité calculée dépasse le seuil. En revanche, si le seuil est réglé à 70 %, l'algorithme ne signalera pas le modèle comme biaisé.

     Les valeurs que vous entrez dans ces écrans doivent être celles qui sont envoyées au point d'extrémité d'évaluation du modèle
(et qui seront ajoutées à la table de contenu utile). Si les données sont manipulées avant d'être envoyées au point d'extrémité d'évaluation, entrez les valeurs manipulées. Par exemple, si les données initiales ont les valeurs `Masculin` et `Féminin` pour le *Sexe*,
qu'elles sont manipulées et que les données envoyées au point d'extrémité d'évaluation sont `M` et `F`,
vous devez entrer `M` et `F` sur cet écran.

1.  Spécifiez les valeurs qui représentent un résultat favorable pour le modèle. Elles sont tirées de la colonne `libellé` dans les [données de formation](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata), si le schéma de sortie du modèle contient une colonne de mappage. Dans {{site.data.keyword.pm_full}}, la colonne `prediction` a toujours une valeur double. La colonne de mappage sert à spécifier le mappage de cette valeur `prediction` au libellé de classe.

    Par exemple, si la valeur `prediction` est `1.0`,
la colonne de mappage peut avoir la valeur `Prêt refusé` ;
cela signifie que la prévision du modèle est `Prêt refusé`. Ainsi, si le schéma de sortie du modèle contient une colonne de mappage, spécifiez les valeurs favorable et défavorable en utilisant celles présentes dans cette colonne.

    En revanche, s'il n'y a pas de colonne de mappage dans le schéma de sortie du modèle,
les valeurs favorable et défavorable doivent être spécifiées en utilisant la valeur de la colonne `prediction`
(`0.0`, `1.0`, etc.).

1.  Enfin, définissez une taille d'échantillon minimale,
pour ne pas mesurer l'équité tant qu'un nombre minimum d'enregistrements n'est pas disponible dans l'ensemble de données d'évaluation, afin que les résultats ne risquent pas d'être faussés. Chaque fois que le contrôle de biais s'exécute, il utilise la taille d'échantillon minimale
pour décider du nombre d'enregistrements sur lesquels effectuer le calcul de biais.

    Un récapitulatif de vos sélections est présenté pour vérification. Pour changer quoi que ce soit, cliquez sur le lien **Modifier** correspondant ;
sinon, cliquez sur **Enregistrer**.

    Vous pouvez également cliquer sur **Ajouter une autre caractéristique**
pour revenir à l'écran de sélection de caractéristique et ajouter d'autres caractéristiques,
comme `City`, `Zip Code` ou `Account Balance`, au moniteur d'équité.

### Fonctionnement du débiaisement
{: #mf-debias}

Pour vérifier le point d'extrémité de débiaisement, cliquez sur le bouton **Point d'extrémité de débiaisement**. Vous pouvez alors voir et copier le point d'extrémité dans différents formats, comme cURL, Java ou Python. 

Le point d'extrémité d'évaluation débiaisé peut être utilisé exactement comme le point d'extrémité d'évaluation normal du modèle déployé. En plus de la réponse du modèle déployé, il renvoie les colonnes `debiased_prediction` et `debiased_probability`.

- La colonne `debiased_prediction` contient la valeur de prévision débiaisée. Dans le cas d'{{site.data.keyword.pm_full}}, il s'agit d'une représentation codée de la prévision. Par exemple, si la prévision du modèle est soit "Prêt accordé", soit "Prêt refusé", {{site.data.keyword.pm_full}} peut coder ces deux valeurs respectivement "0.0" et "1.0". La colonne `debiased_prediction` contient une telle représentation codée de la prévision débiaisée.

- La colonne `debiased_probability`, elle, représente la probabilité de la prévision débiaisée. Il s'agit d'un tableau de valeur double où chaque valeur représente la probabilité que la prévision débiaisée appartienne à l'une des classes de prévision.

Une autre colonne, `debiased_decoded_target`, est également renvoyée,
si vous avez une colonne dans votre schéma de sortie qui contient une colonne avec `modeling-role` comme `decoded-target`.

- La colonne `debiased_decoded_target` contient la représentation chaîne de la prévision débiaisée. Dans l'exemple précédent, où la valeur de prédiction était "0.0" ou "1.0",
la colonne `debiased_decoded_target` contiendra "Prêt accordé" ou "Prêt refusé".

Idéalement, il faut appeler ce point d'extrémité directement depuis votre application de production,
au lieu d'appeler directement le point d'extrémité d'évaluation de votre modèle déployé dans votre moteur de service de modèle
({{site.data.keyword.pm_full}}, Amazon Sagemaker, Microsoft Azure ML Studio, etc.). Ainsi, {{site.data.keyword.aios_short}} enregistre également les valeurs `débiaisées`
dans la table de journalisation de contenu utile de votre déploiement de modèle. Toute l'évaluation effectuée via ce point d'extrémité est alors automatiquement débiaisé.

Comme ce point d'extrémité s'occupe du biais à l'exécution,
il continue d'effectuer des contrôles en arrière-plan pour les dernières données d'évaluation de la table de journalisation du contenu utile
et de mettre à jour le modèle d'atténuation de biais utilisé pour débiaiser les demandes d'évaluation envoyées. Ainsi, {{site.data.keyword.aios_short}} est toujours à jour avec les dernières données entrantes, et pour la détection et l'atténuation des biais.

Enfin, {{site.data.keyword.aios_short}} utilise un seuil pour décider que les données sont acceptables et non biaisées. Ce seuil est le plus faible des seuils définis dans le moniteur d'équité pour tous les attributs d'équité configurés.

## Etapes suivantes
{: #mf-next}

Pour poursuivre la configuration des moniteurs, cliquez sur l'onglet **Dérive** puis sur **Commencer**.
Pour plus d'information, voir [Configuration du moniteur de détection de dérive](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-config).
