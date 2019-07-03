---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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

## Comprendre l'équité
{: #mf-understand}

{{site.data.keyword.aios_short}} vérifie à l'exécution si votre modèle déployé est biaisé. Pour détecter les biais d'un modèle déployé,
vous devez définir des attributs d'équité, comme l'Age ou le Sexe,
comme expliqué dans la section [Configuration du moniteur d'équité](#mf-config) qui suit.

Il est obligatoire de spécifier le schéma de sortie d'un modèle ou d'une fonction dans Watson {{site.data.keyword.pm_short}}
pour que le contrôle de biais soit activé dans {{site.data.keyword.aios_short}}. Le schéma de sortie peut être spécifié avec la propriété `client.repository.ModelMetaNames.OUTPUT_DATA_SCHEMA`
dans la partie métadonnées de l'API `store_model`. Pour plus d'information, voir la
[documentation du client {{site.data.keyword.pm_full}}](http://wml-api-pyclient-dev.mybluemix.net/#repository){: external}.

### Fonctionnement
{: #mf-works}

Avant de configurer le moniteur d'équité, il est indispensable de comprendre quelques concepts clés :

- Les attributs d'équité sont les attributs pour lesquels le modèle risque de présenter un biais.
Par exemple, pour l'attribut d'équité **`Sexe`**,
le modèle pourrait être biaisé avec certaines valeurs (`Féminin`, `Transgenre`, etc.). Un autre exemple d'attribut d'équité est l'**`Age`**,
où le modèle pourrait présenter un biais pour les personnes d'un groupe d'âge, comme `18 à 25`.

- Les valeurs de référence et surveillées : les valeurs des attributs d'équité sont divisées en deux catégories distinctes : Référence et Surveillée.
Les valeurs surveillées sont celles susceptibles d'être discriminées. Dans le cas d'un attribut d'équité comme le **`Sexe`**,
les valeurs surveillées pourraient être `Féminin` et `Transgenre`. Pour un attribut d'équité numérique, tel que l'**`Age`**,
ce pourrait être `[18-25]`. Toutes les autres valeurs d'un attribut d'équité sont alors considérées comme des valeurs de référence,
par exemple `Sexe=Masculin` ou `Age=[26,100]`.

- Résultats favorable et défavorable : la sortie du modèle est classée comme favorable ou défavorable.
Par exemple, si le modèle prévoit si une personne doit obtenir un prêt ou non,
le résultat favorable pourrait être `Prêt accordé` ou `Prêt partiellement accordé`,
et le résultat défavorable, `Prêt refusé`. Le résultat favorable est celui qui est considéré comme positif, et le résultat défavorable, celui qui est considéré comme négatif.

L'algorithme de {{site.data.keyword.aios_short}} calcule le biais sur une base horaire,
en utilisant les `N` derniers enregistrements présents dans la table de journalisation du contenu ;
la valeur de `N` se spécifie à la configuration de l'équité. L'algorithme perturbe ces `N` derniers enregistrements pour générer des données supplémentaires.

La perturbation est effectuée en passant la valeur de l'attribut d'équité de référence à surveillée ou vice versa. Les données perturbées sont ensuite envoyées au modèle pour évaluer son comportement. L'algorithme examine les `N` derniers enregistrements dans la table de contenu, ainsi que le comportement du modèle sur les données perturbées,
et décide si celui-ci agit de manière biaisée.

Un modèle est considéré comme biaisé si, sur cet ensemble de données combiné,
le pourcentage de résultats favorables pour la classe surveillée est inférieur au pourcentage de résultats favorables pour la classe de référence, d'une valeur seuil donnée. Cette valeur seuil doit être spécifiée à la configuration de l'équité.

Les valeurs d'équité peuvent être supérieures à 100 %
si le groupe surveillé obtient davantage de résultats favorables que le groupe de référence. Par ailleurs, si aucune nouvelle requête d'évaluation n'est envoyée, la valeur d'équité demeure constante.
{: note}

### Calculs
{: #mf-bias-math}

La métrique d'équité utilisée dans {{site.data.keyword.aios_short}} est l'impact disparate,
qui est une mesure du taux d'un certain résultat pour un groupe non privilégié, au taux du même résultat pour un groupe privilégié.

L'impact disparate est calculé avec la formule mathématique suivante :

```
                     (nb_positifs(non privilégié) / nb_instances(non privilégié))
Impact disparate =   ______________________________________________________________________

                     (nb_positifs(privilégié) / nb_instances(privilégié))
```

où `nb_positifs` est le nombre d'individus du groupe
(non privilégié ou privilégié) qui ont reçu un résultat positif, et nb_instances, le nombre total d'individus du groupe.

Le nombre résultant est le pourcentage
de la fréquence à laquelle le groupe non privilégié reçoit le résultat positif
par rapport à celle à laquelle le groupe privilégié le reçoit.
Par exemple, si un modèle de risque de crédit
attribue la prévision "sans risque" à 80 % des candidats non privilégiés et à 100 % des candidats privilégiés,
il aura un impact disparate (présenté comme le score d'équité dans {{site.data.keyword.aios_short}}) de 80 %.

Dans {{site.data.keyword.aios_short}}, les résultats positifs sont appelés les résultats favorables
et les résultats négatifs, les résultats défavorables.
Le groupe privilégié est appelé le groupe de référence et le groupe non privilégié, le groupe surveillé.


### Affichage du biais ![étiquette bêta](images/beta.png)
{: #mf-monitor-bias-viz}

Lorsqu'un biais potentiel est détecté,
{{site.data.keyword.aios_short}} effectue plusieurs opérations pour vérifier sa réalité. Il perturbe les données en basculant la valeur surveillée sur la valeur de référence puis en exécutant ce nouvel enregistrement avec le modèle. Il fait ensuite ressortir la sortie résultante comme la sortie débiaisée. {{site.data.keyword.aios_short}} forme également un modèle débiaisé reflet qu'il utilise ensuite pour détecter quand un modèle va faire une prévision biaisée. 

Deux ensembles de données différents sont utilisés pour calculer l'équité et l'exactitude.
L'équité est calculée en utilisant le contenu + les données perturbées.
L'exactitude est calculée en utilisant les données de commentaires.
Pour calculer l'exactitude, {{site.data.keyword.aios_short}} a besoin de données étiquetées manuellement, qui ne sont présentes que dans la table des commentaires.

Les résultats de ces déterminations sont disponibles dans l'affichage du biais, qui comprend les vues suivantes : 

- **Contenu + Données perturbées** :
Comprend la demande d'évaluation reçue pour l'heure sélectionnée
plus des enregistrements d'heures précédentes si le nombre minimum d'enregistrements requis pour l'évaluation n'était pas atteint. Comprend les enregistrements perturbés/synthétisés supplémentaires utilisés pour tester la réponse du modèle lorsque la valeur de la fonction surveillée change.

   Remarquez les détails suivants du contenu et des données perturbées :

   - Nombre d'enregistrements lus dans cette heure de la table de contenu
   - Enregistrements supplémentaires lus d'heures précédentes
(par exemple, si la valeur `min_records` est définie à 1000 dans la configuration de l'équité
et que seulement 10 enregistrements sont ajoutés entre 14h et 15h,
le système lira 990 autres enregistrements des heures précédentes afin d'atteindre le minimum requis.)
   - Enregistrements perturbés selon l'attribut d'équité
   - Horodate du plus ancien enregistrement de la fenêtre de données pour lequel le biais doit être calculé
   - Horodate du dernier enregistrement de la fenêtre de données pour lequel le biais doit être calculé

  ![exemple de contenu plus données perturbées](images/payload&perturbed.png)



- **Contenu** :
Demandes d'évaluation réelles reçues par le modèle durant l'heure sélectionnée.

   Remarquez les détails suivants du contenu :
   
   - Nombre d'enregistrements lus/sur lesquels le débiaisement est effectué à partir de la table de contenu
   - Horodate du plus ancien enregistrement de la fenêtre de données pour lequel le biais doit être calculé
   - Horodate du dernier enregistrement de la fenêtre de données pour lequel le biais doit être calculé


  ![exemple de données de contenu](images/payload.png)

- **Formation** :
Enregistrements de données de formation utilisés pour former le modèle.

   Remarquez les détails suivants de la formation :
   
   - Nombre d'enregistrements de données de formation. Les données de formation sont lues une fois et la distribution est stockée
dans la variable `subscription/fairness_configuration`. Lors du calcul de la distribution, nous devons également trouver le nombre d'enregistrements de données de formation et le stocker dans la même distribution. D'autre part, si les données de formation sont changées,
c'est-à-dire en cas de nouvelle exécution de la commande `POST /data_distribution`,
cette valeur est mise à jour dans la variable `fairness_configuration/training_data_distribution`. Lors de l'envoi de la métrique, nous devons également envoyer cette valeur aussi.
   - Heure du dernier traitement des données de formation (premier moment et mises à jour suivantes)

  ![exemple de données de formation](images/training.png)
   

   
- **Données débiaisées** :
Sortie de l'algorithme de débiaisement après traitement des données d'exécution et perturbées.

   Remarquez les détails suivants des données débiaisées :
   
   - Nombre d'enregistrements lus/sur lesquels le débiaisement est effectué à partir de la table de contenu
   - Enregistrements supplémentaires lus pour effectuer le biais, et donc débiaisés aussi. Même nombre que pour la sélection `Contenu + Données perturbées`
   - Enregistrements perturbés selon l'attribut d'équité
   - Horodate du plus ancien enregistrement de la fenêtre de données pour lequel le biais doit être calculé
   - Horodate du dernier enregistrement de la fenêtre de données pour lequel le biais doit être calculé
   - La partie en-tête de la vue débiaisée affiche les valeurs de l'équité avant et après. 
      - L'exactitude **après** est calculée en prenant les données de commentaires et en les envoyant à l'API de débiaisement active.
Cette API renvoie la prévision débiaisée.
Les données de commentaires contiennent également l'étiquette manuelle.
Celle-ci est comparée à la prévision débiaisée pour calculer l'exactitude.
Cette API renvoie la prévision débiaisée.
La table des commentaires contient également l'étiquette manuelle.
Celle-ci est comparée à la prévision débiaisée pour calculer l'exactitude. 
      - L'exactitude **avant** est calculée en utilisant les mêmes données de commentaires.
Celles-ci sont envoyées au modèle pour obtenir sa prévision et l'exactitude est obtenue en comparant la valeur prévue à l'étiquette manuelle.

  ![exemple de données débiaisées](images/debiased.png)
  
### Exemple
{: #mf-ex1}

Considérez un point de données où, pour `Sexe=Masculin` (valeur de référence),
le modèle prévoit un résultat favorable,
mais où lorsque l'enregistrement est perturbé par le changement du `Sexe` en `Féminin` (valeur surveillée),
en gardant inchangées toutes les autres valeurs de fonction, il prévoit un résultat défavorable. Un modèle est dit présenter un biais globalement s'il y a suffisamment de points de données
(sur les `N` derniers enregistrements de la table de contenu, plus les données perturbées)
où il agit de manière biaisée.

### Modèles pris en charge
{: #mf-supmo}

 {{site.data.keyword.aios_short}} ne prend en charge la détection de biais que pour les modèles et les fonctions Python
qui attendent des données structurées dans leur vecteur de fonctions.

## Configuration du moniteur d'équité
{: #mf-config}

Dans l'onglet **Equité**, sur la page **Qu'est-ce que l'équité ?**,
cliquez sur **Commencer** pour démarrer le processus de configuration.

![Page Qu'est-ce que l'équité ?](images/fair-what-is.png)

Tout au long de ce processus, {{site.data.keyword.aios_full}} analyse votre modèle et fait des recommandations basées sur le résultat le plus logique.
Sur les pages successives de l'onglet **Equité**, vous devez effectuer les opérations suivantes :

1. Sélectionnez les fonctions à surveiller.
Seules sont prises en charge les fonctions qui sont de type de données d'équité catégoriel, numérique (entier), flottant ou double. Les fonctions qui ont un autre type de données ne sont pas prises en charge.

1. Spécifiez le groupe de référence et le groupe surveillé.

   Chaque fonction a des exigences spécifiques à configurer.
Par exemple, si vous choisissez `age` pour l'une des fonctions à surveiller,
vous devez définir la plage d'âge d'un **Groupe de référence** et celle d'un **Groupe surveillé**
en entrant les valeurs directement dans chaque groupe.

1.  Définissez le seuil d'alerte d'équité pour la fonction.

    Un seuil d'équité sert à spécifier une différence acceptable entre le pourcentage de résultats favorables pour le groupe surveillé
et pour le groupe de référence.

    Considérez un modèle qui prévoit qui doit obtenir un prêt (`favorable outcome=loan granted`)
et qui ne doit pas (`unfavorable outcome=loan denied`). D'autre part, la valeur surveillée pour l'âge est `[18,25]` et la valeur de référence, `[26,100]`. Lors de l'exécution de l'algorithme de détection de biais, s'il trouve que le pourcentage de résultats favorables pour les personnes du groupe d'âge `[18,25]`
dans les `N` derniers enregistrements plus les données perturbées est de `50 %` 
tandis qu'il est de `70 %` pour le groupe d'âge `[26,100]`,
l'équité sera 50*100/70 = 71,42.

    Si le seuil d'équité est réglé à 80 %, l'algorithme marquera le modèle comme biaisé
car l'équité calculée dépasse le seuil. En revanche, si le seuil est réglé à 70 %, l'algorithme ne signalera pas le modèle comme biaisé.

     Les valeurs que vous entrez dans ces écrans doivent être celles qui sont envoyées au noeud final d'évaluation du modèle
(et qui seront ajoutées à la table de contenu).
Si les données sont manipulées avant d'être envoyées au noeud final d'évaluation, entrez les valeurs manipulées. Par exemple, si les données initiales ont les valeurs `Masculin` et `Féminin` pour le *Sexe*,
qu'elles sont manipulées et que les données envoyées au noeud final d'évaluation sont `M` et `F`,
vous devez entrer `M` et `F` sur cet écran.

1.  Spécifiez les valeurs qui représentent un résultat favorable pour le modèle.
Elles sont tirées de la colonne `libellé` dans les [données de formation](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata), si le schéma de sortie du modèle contient une colonne de mappage. Dans {{site.data.keyword.pm_full}}, la colonne `prediction` a toujours une valeur double. La colonne de mappage sert à spécifier le mappage de cette valeur `prediction` au libellé de classe.

    Par exemple, si la valeur `prediction` est `1.0`,
la colonne de mappage peut avoir la valeur `Prêt refusé` ;
cela signifie que la prévision du modèle est `Prêt refusé`. Ainsi, si le schéma de sortie du modèle contient une colonne de mappage, spécifiez les valeurs favorable et défavorable en utilisant celles présentes dans cette colonne.

    En revanche, s'il n'y a pas de colonne de mappage dans le schéma de sortie du modèle,
les valeurs favorable et défavorable doivent être spécifiées en utilisant la valeur de la colonne `prediction`
(`0.0`, `1.0`, etc.).

1.  Enfin, définissez une taille d'échantillon minimale,
pour ne pas mesurer l'équité tant qu'un nombre minimum d'enregistrements n'est pas disponible dans l'ensemble de données d'évaluation, afin que les résultats ne risquent pas d'être faussés. Chaque fois que le contrôle de biais s'exécute, il utilise la taille d'échantillon minimale
pour décider du nombre d'enregistrements sur lesquels effectuer le calcul de biais.

    Un récapitulatif de vos sélections est présenté pour vérification.
Pour changer quoi que ce soit, cliquez sur le lien **Modifier** correspondant ;
sinon, cliquez sur **Enregistrer**.

    Vous pouvez également cliquer sur **Ajouter une autre fonction**
pour revenir à l'écran de sélection de fonction et ajouter d'autres fonctions,
comme `City`, `Zip Code` ou `Account Balance`, au moniteur d'équité.

### Fonctionnement du débiaisement
{: #mf-debias}

Pour vérifier le noeud final de débiaisement, cliquez sur le bouton **Noeud final de débiaisement**.
Vous pouvez alors voir et copier le noeud final dans différents formats, comme cURL, Java ou Python. 

Le noeud final d'évaluation débiaisé peut être utilisé exactement comme le noeud final d'évaluation normal du modèle déployé.
En plus de la réponse du modèle déployé, il renvoie les colonnes `debiased_prediction` et `debiased_probability`.

- La colonne `debiased_prediction` contient la valeur de prévision débiaisée. Dans le cas d'{{site.data.keyword.pm_full}}, il s'agit d'une représentation codée de la prévision. Par exemple, si la prévision du modèle est soit "Prêt accordé", soit "Prêt refusé", {{site.data.keyword.pm_full}} peut coder ces deux valeurs respectivement "0.0" et "1.0". La colonne `debiased_prediction` contient une telle représentation codée de la prévision débiaisée.

- La colonne `debiased_probability`, elle, représente la probabilité de la prévision débiaisée. Il s'agit d'un tableau de valeur double où chaque valeur représente la probabilité que la prévision débiaisée appartienne à l'une des classes de prévision.

Une autre colonne, `debiased_decoded_target`, est également renvoyée,
si vous avez une colonne dans votre schéma de sortie qui contient une colonne avec `modeling-role` comme `decoded-target`.

- La colonne `debiased_decoded_target` contient la représentation chaîne de la prévision débiaisée. Dans l'exemple précédent, où la valeur de prédiction était "0.0" ou "1.0",
la colonne `debiased_decoded_target` contiendra "Prêt accordé" ou "Prêt refusé".

Idéalement, il faut appeler ce noeud final directement depuis votre application de production,
au lieu d'appeler directement le noeud final d'évaluation de votre modèle déployé dans votre moteur de service de modèle
({{site.data.keyword.pm_full}}, Amazon Sagemaker, Microsoft Azure ML Studio, etc.). Ainsi, {{site.data.keyword.aios_short}} enregistre également les valeurs `débiaisées`
dans la table de journalisation de contenu de votre déploiement de modèle. Toute l'évaluation effectuée via ce noeud final est alors automatiquement débiaisé.

Comme ce noeud final s'occupe du biais à l'exécution,
il continue d'effectuer des contrôles en arrière-plan pour les dernières données d'évaluation de la table de journalisation du contenu
et de mettre à jour le modèle d'atténuation de biais utilisé pour débiaiser les demandes d'évaluation envoyées. Ainsi, {{site.data.keyword.aios_short}} est toujours à jour avec les dernières données entrantes, et pour la détection et l'atténuation des biais.

Enfin, {{site.data.keyword.aios_short}} utilise un seuil pour décider que les données sont acceptables et non biaisées. Ce seuil est le plus faible des seuils définis dans le moniteur d'équité pour tous les attributs d'équité configurés.

## Etapes suivantes
{: #mf-next}

Sur la page **Configurer les moniteurs**, vous pouvez sélectionner une autre catégorie de surveillance.
