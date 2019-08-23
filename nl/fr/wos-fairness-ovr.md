---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds

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

# Présentation des métriques d'équité
{: #anlz_metrics_fairness}

Utilisez la surveillance de l'équité de {{site.data.keyword.aios_full}}
pour déterminer si les résultats produits par votre modèle sont équitables ou non pour le groupe surveillé. Lorsque la surveillance de l'équité est activée, elle génère un ensemble de métriques toutes les heures par défaut. Vous pouvez générer ces métriques sur demande en cliquant sur le bouton **Vérifier la qualité maintenant** ou en utilisant le client Python.
{: shortdesc}

{{site.data.keyword.aios_short}} détecte automatiquement si un modèle comporte des attributs protégés connus. Lorsqu'il détecte ces attributs, il recommande automatiquement de configurer un moniteur de biais pour chaque attribut présent,
pour garantir le suivi du biais en production sur ces attributs potentiellement sensibles. 

Actuellement, {{site.data.keyword.aios_short}} détecte et recommande des moniteurs pour les attributs protégés suivants : 

- sexe
- ethnicité
- état matrimonial
- âge
- code postal

En plus de détecter les attributs protégés, {{site.data.keyword.aios_short}} recommande
les valeurs dans chaque attribut qui doivent être définies comme valeurs surveillées et valeurs de référence. Ainsi, par exemple, {{site.data.keyword.aios_short}} recommande de configurer le moniteur de biais dans l'attribut "Sex"
en définissant "Woman" et "Non-Binary" comme valeurs surveillées, et "Male" comme valeur de référence. Si vous voulez apporter des modifications par rapport aux recommandations, vous pouvez éditer celles-ci via le panneau de configuration du biais. 

Les moniteurs de biais recommandés accélèrent la configuration et garantissent le contrôle de vos modèles d'IA quant à l'équité par rapport aux attributs sensibles. Les organismes de réglementation commencent à regarder de plus près le biais algorithmique
et il devient essentiel pour les organisations de bien comprendre le fonctionnement de leurs modèles et s'ils donnent des résultats inéquitables pour certains groupes.

## Comprendre l'équité
{: #mf-understand}

{{site.data.keyword.aios_short}} vérifie à l'exécution si votre modèle déployé est biaisé. Pour détecter les biais d'un modèle déployé,
vous devez définir des attributs d'équité, comme l'Age ou le Sexe,
comme expliqué dans la section [Configuration du moniteur d'équité](#mf-config) qui suit.

Il est obligatoire de spécifier le schéma de sortie d'un modèle ou d'une fonction dans {{site.data.keyword.pm_short}},
pour que le contrôle de biais soit activé dans {{site.data.keyword.aios_short}}. Le schéma de sortie peut être spécifié avec la propriété `client.repository.ModelMetaNames.OUTPUT_DATA_SCHEMA`
dans la partie métadonnées de l'API `store_model`. Pour plus d'informations, consultez la
[documentation du client {{site.data.keyword.pm_full}}](http://wml-api-pyclient-dev.mybluemix.net/#repository){: external}.

### Fonctionnement
{: #mf-works}

Avant de configurer le moniteur d'équité, il est indispensable de comprendre quelques concepts clés :

- Les attributs d'équité sont les attributs pour lesquels le modèle risque de présenter un biais. Par exemple, pour l'attribut d'équité **`Sexe`**,
le modèle pourrait être biaisé avec certaines valeurs (`Féminin`, `Transgenre`, etc.). Un autre exemple d'attribut d'équité est l'**`Age`**,
où le modèle pourrait présenter un biais pour les personnes d'un groupe d'âge, comme `18 à 25`.

- Les valeurs de référence et surveillées : les valeurs des attributs d'équité sont divisées en deux catégories distinctes : Référence et Surveillée. Les valeurs surveillées sont celles susceptibles d'être discriminées. Dans le cas d'un attribut d'équité comme le **`Sexe`**,
les valeurs surveillées pourraient être `Féminin` et `Transgenre`. Pour un attribut d'équité numérique, tel que l'**`Age`**,
ce pourrait être `[18-25]`. Toutes les autres valeurs d'un attribut d'équité sont alors considérées comme des valeurs de référence,
par exemple `Sexe=Masculin` ou `Age=[26,100]`.

- Résultats favorable et défavorable : la sortie du modèle est classée comme favorable ou défavorable. Par exemple, si le modèle prévoit si une personne doit obtenir un prêt ou non,
le résultat favorable pourrait être `Prêt accordé` ou `Prêt partiellement accordé`,
et le résultat défavorable, `Prêt refusé`. Le résultat favorable est celui qui est considéré comme positif, et le résultat défavorable, celui qui est considéré comme négatif.

L'algorithme de {{site.data.keyword.aios_short}} calcule le biais sur une base horaire,
en utilisant les `N` derniers enregistrements présents dans la table de journalisation du contenu utile ;
la valeur de `N` se spécifie à la configuration de l'équité. L'algorithme perturbe ces `N` derniers enregistrements pour générer des données supplémentaires.

La perturbation est effectuée en passant la valeur de l'attribut d'équité de référence à surveillée ou vice versa. Les données perturbées sont ensuite envoyées au modèle pour évaluer son comportement. L'algorithme examine les `N` derniers enregistrements dans la table de contenu utile, ainsi que le comportement du modèle sur les données perturbées,
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
par rapport à celle à laquelle le groupe privilégié le reçoit. Par exemple, si un modèle de risque de crédit
attribue la prévision "sans risque" à 80 % des candidats non privilégiés et à 100 % des candidats privilégiés,
il aura un impact disparate (présenté comme le score d'équité dans {{site.data.keyword.aios_short}}) de 80 %.

Dans {{site.data.keyword.aios_short}}, les résultats positifs sont appelés les résultats favorables
et les résultats négatifs, les résultats défavorables. Le groupe privilégié est appelé le groupe de référence et le groupe non privilégié, le groupe surveillé.


### Affichage du biais ![étiquette bêta](images/beta.png)
{: #mf-monitor-bias-viz}

Lorsqu'un biais potentiel est détecté,
{{site.data.keyword.aios_short}} effectue plusieurs opérations pour vérifier sa réalité. Il perturbe les données en basculant la valeur surveillée sur la valeur de référence puis en exécutant ce nouvel enregistrement avec le modèle. Il fait ensuite ressortir la sortie résultante comme la sortie débiaisée. {{site.data.keyword.aios_short}} forme également un modèle débiaisé reflet qu'il utilise ensuite pour détecter quand un modèle va faire une prévision biaisée. 

Deux ensembles de données différents sont utilisés pour calculer l'équité et l'exactitude. L'équité est calculée en utilisant le contenu utile + les données perturbées. L'exactitude est calculée en utilisant les données de retour. Pour calculer l'exactitude, {{site.data.keyword.aios_short}} a besoin de données étiquetées manuellement, qui ne sont présentes que dans la table de retours.

Les résultats de ces déterminations sont disponibles dans l'affichage du biais, qui comprend les vues suivantes. (Vous ne voyez ces vues que s'il y a des données à prendre en charge

- **Contenu + Données perturbées** :
Comprend la demande d'évaluation reçue pour l'heure sélectionnée
plus des enregistrements d'heures précédentes si le nombre minimum d'enregistrements requis pour l'évaluation n'était pas atteint. Comprend les enregistrements perturbés/synthétisés supplémentaires utilisés pour tester la réponse du modèle lorsque la valeur de la caractéristique surveillée change.

   Remarquez les détails suivants du contenu utile et des données perturbées :

   - Nombre d'enregistrements lus dans cette heure de la table de contenu utile
   - Enregistrements supplémentaires lus d'heures précédentes
(par exemple, si la valeur `min_records` est définie à 1000 dans la configuration de l'équité
et que seulement 10 enregistrements sont ajoutés entre 14h et 15h,
le système lira 990 autres enregistrements des heures précédentes afin d'atteindre le minimum requis.)
   - Enregistrements perturbés selon l'attribut d'équité
   - Horodate du plus ancien enregistrement de la fenêtre de données pour lequel le biais doit être calculé
   - Horodate du dernier enregistrement de la fenêtre de données pour lequel le biais doit être calculé

  ![exemple de contenu utile plus données perturbées](images/payload&perturbed.png)



- **Contenu** :
Demandes d'évaluation réelles reçues par le modèle durant l'heure sélectionnée.

   Remarquez les détails suivants du contenu utile :
   
   - Nombre d'enregistrements lus/sur lesquels le débiaisement est effectué à partir de la table de contenu utile
   - Horodate du plus ancien enregistrement de la fenêtre de données pour lequel le biais doit être calculé
   - Horodate du dernier enregistrement de la fenêtre de données pour lequel le biais doit être calculé


  ![exemple de données de contenu utile](images/payload.png)

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
Sortie de l'algorithme de débiaisement après traitement des données d'exécution et perturbées. En sélectionnant le bouton d'option **Débiaisé**, vous voyez les changements dans le modèle débiaisé par rapport au modèle en production. Le graphe reflète l'amélioration des résultats pour les groupes.


   Remarquez les détails suivants des données débiaisées :
   
   - Nombre d'enregistrements lus/sur lesquels le débiaisement est effectué à partir de la table de contenu utile
   - Enregistrements supplémentaires lus pour effectuer le biais, et donc débiaisés aussi. Même nombre que pour la sélection `Contenu + Données perturbées`
   - Enregistrements perturbés selon l'attribut d'équité
   - Horodate du plus ancien enregistrement de la fenêtre de données pour lequel le biais doit être calculé
   - Horodate du dernier enregistrement de la fenêtre de données pour lequel le biais doit être calculé
   - La partie en-tête de la vue débiaisée affiche les valeurs de l'équité avant et après. 
      - L'exactitude **après** est calculée en prenant les données de retour et en les envoyant à l'API de débiaisement active. Cette API renvoie la prévision débiaisée. Les données de retour contiennent également l'étiquette manuelle. Celle-ci est comparée à la prévision débiaisée pour calculer l'exactitude. Cette API renvoie la prévision débiaisée. La table de retours contient également l'étiquette manuelle. Celle-ci est comparée à la prévision débiaisée pour calculer l'exactitude. 
      - L'exactitude **avant** est calculée en utilisant les mêmes données de retour. Celles-ci sont envoyées au modèle pour obtenir sa prévision et l'exactitude est obtenue en comparant la valeur prévue à l'étiquette manuelle.

  ![exemple de données débiaisées](images/debiased.png)
  
### Exemple
{: #mf-ex1}

Considérez un point de données où, pour `Sexe=Masculin` (valeur de référence),
le modèle prévoit un résultat favorable,
mais où lorsque l'enregistrement est perturbé par le changement du `Sexe` en `Féminin` (valeur surveillée),
en gardant inchangées toutes les autres valeurs de caractéristique, il prévoit un résultat défavorable. Un modèle est dit présenter un biais globalement s'il y a suffisamment de points de données
(sur les `N` derniers enregistrements de la table de contenu utile, plus les données perturbées)
où il agit de manière biaisée.

### Modèles pris en charge
{: #mf-supmo}

 {{site.data.keyword.aios_short}} ne prend en charge la détection de biais que pour les modèles et les fonctions Python
qui attendent des données structurées dans leur vecteur de caractéristique.

Les métriques d'équité sont calculées en fonction des informations suivantes :

- données de contenu utile d'évaluation.

En vue d'une surveillance adéquate, toutes les demandes d'évaluation doivent être consignées également dans {{site.data.keyword.aios_short}}. La journalisation des données de contenu utile est automatisée pour les moteurs {{site.data.keyword.pm_full}}.

Pour les autres moteurs d'apprentissage automatique, les données de contenu utile peuvent être fournies à l'aide du client Python ou de l'API REST.

Pour les moteurs d'apprentissage automatique autres que {{site.data.keyword.pm_full}}, la surveillance de l'équité crée des demandes d'évaluation supplémentaires sur le déploiement surveillé.
{: note}

Vous pouvez examiner la valeur de toutes les métriques au fil du temps dans le tableau de bord {{site.data.keyword.aios_short}} :

![graphique des métriques d'équité montrant une dérive au-dessous du seuil défini](images/fairness_metrics_001.png)

Vous pouvez consulter les détails connexes, tels que des résultats favorables et défavorables :

![détails de l'équité](images/fairness_metrics_002.png)

Vous pouvez consulter les transactions détaillées :

![graphique de l'équité montrant une liste de transactions](images/fairness_metrics_003.png)

Vous pouvez consulter le point d'extrémité d'évaluation débiaisée recommandé :

![détails du point d'extrémité d'évaluation débiaisée](images/fairness_metrics_004.png)

### Métriques d'équité prises en charge
{: #anlz_metrics_supfairmets}

Les métriques d'équité suivantes sont prises en charge par {{site.data.keyword.aios_short}} :

- [Equité d'un groupe](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_group)

Les attributs protégés suivants sont pris en charge par {{site.data.keyword.aios_short}} : 

- [sexe](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-sex)
- [ethnicité](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-ethnicity)
- [état matrimonial](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-marital)
- [âge](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-age)
- [code postal](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-zip)


### Détails d'équité pris en charge
{: #anlz_metrics_supfairdets}

Les détails suivants des métriques d'équité sont pris en charge par {{site.data.keyword.aios_short}} :

- Pourcentages favorables pour chacun des groupes
- Moyennes d'équité pour tous les groupes d'équité

```
                          (% de résultats favorables dans le groupe surveillé)
Taux d'impact disparate = ____________________________________________________
                          (% de résultats favorables dans le groupe de référence)
```

- Distribution des données pour chacun des groupes surveillés
- Distribution des données de contenu utile
