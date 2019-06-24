---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

keywords: fairness, monitoring, charts, de-biasing, bias, accuracy

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

# Surveillance de l'équité, du nombre moyen de demandes par minute et de l'exactitude
{: #it-ov}

Les données de surveillance des différents déploiements sont affichées sur un graphe de temps. Le graphe présente l'équité, le nombre moyen de demandes par minute et l'exactitude sur les sept derniers jours.
{: shortdesc}

## Affichage des données d'un déploiement
{: #it-vdep}

Pour afficher les données de surveillance d'un déploiement, sélectionnez-le dans le tableau de bord. Le haut du graphe des données de surveillance fournit des informations sur le modèle déployé et indique
l'heure de la dernière évaluation de son équité et de son exactitude et de la prochaine.

![Graphe de temps](images/insight-time-chart.png)

Comme les contrôles de l'algorithme ne sont exécutés que toutes les heures,
des boutons sont également fournis pour vous permettre de contrôler l'équité et l'exactitude à la demande. Si vous n'avez pas fourni suffisamment d'enregistrements de contenu (équité) ou d'enregistrements de commentaires (exactitude),
le message suivant est affiché, par exemple :

![Bouton Exactitude](images/accuracy-button.png)

Ensuite, déplacez le marqueur sur le graphe pour voir les statistiques d'une heure particulière. Dans cet exemple, l'heure sélectionnée est 13h00 CST le 18 septembre, qui donne les statistiques suivantes :

![Détail du graphe de temps](images/insight-time-detail.png)

- ***Equité*** : deux fonctions d'équité sur trois, Car Value et Area Code, ont atteint leur seuil d'approbation défini. La troisième fonction d'équité, Age, a été marquée comme biaisée. Vous pouvez aussi voir le nombre de résultats attendus (ici le pourcentage des approbations et des refus) d'une population donnée dans les fonctions dont l'équité est surveillée.
- ***Exactitude*** : la métrique moyenne d'exactitude a été de 78 %.
- ***Nbre moyen de demandes / mn*** : en moyenne, 300 enregistrements ont été traités par minute entre 13h00 et 14h00 CST. Le débit est calculé toutes les minutes et sa valeur moyenne sur l'heure est indiquée sur le graphe.

## Visualisation des données d'une heure spécifique
{: #it-vdet}

Pour voir les détails derrière une statistique d'équité particulière, cliquez sur le lien **Afficher les détails** pour l'heure sélectionnée.

Un affichage s'ouvre des points de données d'une fonction surveillée à l'heure sélectionnée. Avec l'exemple précédent, la fonction Age, marquée comme biaisée, est affichée.

Notez les trois filtres en haut de la page (Fonction, Date et Heure) qui vous permettent de sélectionner une autre fonction ou une date/heure différente.

![Graphe de temps](images/insight-data-detail.png)

### Interprétation du graphe
{: #it-intp}

Le graphe montre plusieurs choses :

- Vous pouvez voir la population qui fait l'objet du biais (les clients âgés de 18 à 23 ans). Le graphe indique également le pourcentage de résultat attendu (52%) pour cette population.

- Le graphe indique le pourcentage de résultat attendu (70%) pour la population de référence. Il s'agit de la moyenne de résultat attendu pour toutes les populations de référence.

- Le graphe indique la présence de biais car le rapport du pourcentage de résultats attendus pour les populations âgées de 18 à 23 ans
sur celui pour la population de référence est inférieur au seuil. En d'autres termes, 0,52/0,7 = 0,74, qui est inférieur au seuil de 0,8.

- Le graphe montre aussi la distribution des valeurs de référence et surveillée
pour chaque valeur distincte de l'attribut dans les données de la table de contenu analysées pour identifier le biais. En d'autres termes, si l'algorithme de détection de biais a analysé les 1790 derniers enregistrements de la table de contenu,
120 de ces enregistrements avaient un âge du client entre 18 et 23 ans,
et le graphe à barres représente les résultats `Approved` et `Denied` de cette distribution. La distribution des données de contenu est indiquée pour chaque valeur distincte de l'attribut d'équité (même les valeurs de référence sont indiquées). Ces informations permettent de corréler le biais avec la quantité de données reçues par le modèle.

- Le graphe indique également que la population âgée de 31 à 35 ans a reçu 91 % de résultats attendus. Cela donne la source du biais : les données de ce groupe ont faussé les résultats,
elles ont fait augmenter le pourcentage de résultats attendus pour la classe de référence. Ces informations peuvent être utilisées pour identifier des parties des données qui peuvent être ensuite sous-échantillonnées lors de la reformation du modèle.

- Une autre chose importante indiquée par le graphe est le nom de la table qui contient les données identifiées pour un étiquetage manuel. Chaque fois que l'algorithme détectes un biais dans un modèle, il identifie également les points de données
qui peuvent être envoyés pour étiquetage manuel par des humains. Ces données étiquetées manuellement peuvent ensuite être utilisées avec les données de formation initiales pour reformer le modèle. Le modèle reformé n'aura probablement plus le biais. La table d'étiquetage manuel se trouve dans la base de données associée à l'instance de {{site.data.keyword.aios_short}}.

## Données d'exécution et de formation
{: #it-rtsw}

Le commutateur Données d'exécution / Données de formation vous permet de commuter les différences
entre votre modèle formé et les données collectées à l'exécution qui déclenchent un avertissement de biais. Pour plus d'informations sur les données de formation, voir [Pourquoi {{site.data.keyword.aios_short}} a-t-il besoin d'accéder à mes données de formation ?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)

![Commutateur Exécution / Formation](images/runtime_train_data.png)

## Afficher les transactions
{: #it-tra}

Cette option vous permet d'afficher les différentes transactions qui ont contribué au biais lorsque vous cliquez sur le bouton **Afficher les transactions**.

![Afficher les transactions](images/view_transactions.png)

La liste des transactions où le déploiement a agi de manière biaisée s'affiche. Pour obtenir des détails sur une transaction dans l'onglet Explicabilité, cliquez sur le lien **Expliquer** pour son ID. Pour plus d'information, voir [Surveillance de l'explicabilité](/docs/services/ai-openscale?topic=ai-openscale-ie-ov).

Vous pouvez voir toutes les transactions de la fonction (ici "AGE") et de la période (ici "15 septembre 2018 13:00") sélectionnées
en sélectionnant la vue **Toutes les transactions** :

![Liste de toutes les transactions](images/transaction_list1.png)

Vous pouvez n'afficher que les transactions qui ont obtenu un résultat biaisé
en sélectionnant la vue **Transactions biaisées**. Chaque transaction biaisée est comparée à une transaction similaire mais légèrement modifiée (perturbée)
qui montre comment le changement de la valeur de la fonction surveillée (AGE)
donnera un résultat favorable :

![Liste des transactions biaisées](images/transaction_list2.png)

## Modèle de production et Modèle débiaisé
{: #it-prdb}

Vous pouvez utiliser ces deux onglets pour basculer entre votre modèle de production et un modèle débiaisé créé par {{site.data.keyword.aios_short}}. Pour plus de détails, voir [Fonctionnement du débiaisement](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor#mf-debias).

![Commutateur Exécution / Formation](images/bias-debias.png)

En sélectionnant l'onglet **Modèle débiaisé**, vous voyez les changements dans le modèle débiaisé par rapport au modèle en production. Dans cet exemple, l'équité du modèle est passée de 74 % à 93 %, avec seulement 1 % de baisse de l'exactitude. Le graphe reflète également l'amélioration des résultats pour les groupes de 18 à 23 ans.

![Commutateur Exécution / Formation](images/insight-data-detail2.png)

### Options de débiaisement
{: #it-dbo}

- *Débiaisement passif* -
Lorsque {{site.data.keyword.aios_short}} effectue un contrôle de biais, il effectue également un débiaisement des données,
en analysant le comportement du modèle et en identifiant les données où il agit de manière biaisée.

  {{site.data.keyword.aios_short}} construit ensuite un modèle d'apprentissage automatique pour
prévoir si le modèle risque d'agir de manière biaisée sur un nouveau point de données particulier. Puis il analyse les données reçues par le modèle, sur une heure,
et trouve les points de données où il pense que celui-ci agit de manière biaisée. Pour ces points de données, l'attribut d'équité est perturbé de la minorité à la majorité,
et les données perturbées sont envoyées au modèle initial pour prévision. Cette prévision du modèle initial est utilisée comme sortie débiaisée.

  {{site.data.keyword.aios_short}} effectue ce débiaisement toutes les heures,
sur toutes les données reçues par le modèle au cours de la dernière heure. Il calcule également l'équité de la sortie débiaisée et l'affiche dans l'onglet **Modèle débiaisé**.

- *Débiaisement actif* -
Dans le débiaisement actif, vous pouvez utiliser un noeud final d'API REST de débiaisement depuis votre application. Ce noeud final d'API REST appellera votre modèle en interne et contrôlera son comportement.

  Si {{site.data.keyword.aios_short}} pense que le modèle agit de manière biaisée,
il perturbera les données comme indiqué plus haut et les renverra au modèle initial. La sortie du modèle initial avec les données perturbées sera renvoyée comme prévision débiaisée. Si {{site.data.keyword.aios_short}} détermine que le modèle initial n'agit pas de manière biaisée,
il renverra la prévision de celui-ci comme prévision débiaisée. Ainsi, en utilisant ce noeud final d'API REST,
vous pouvez faire en sorte que votre application ne prenne pas de décisions basées sur une sortie biaisée de vos modèles.

Pour trouver votre noeud final d'API REST de débiaisement, sélectionnez le lien **Noeud final d'évaluation débiaisée**

![Noeud final d'API de débiaisement](images/insight-debias-api.png)
