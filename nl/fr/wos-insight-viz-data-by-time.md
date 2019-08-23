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

# Visualisation des données d'une heure spécifique
{: #it-vdet}

Pour voir les détails d'une statistique d'équité particulière, cliquez sur le graphe, à l'endroit correspondant à l'instant que vous souhaitez examiner. Un affichage s'ouvre des points de données d'une caractéristique surveillée à l'heure sélectionnée. Dans l'exemple suivant, qui est dans la continuité de l'exemple précédent,
les détails affichés sont ceux de la caractéristique Age.
{: shortdesc}

Notez les trois filtres en haut de la page (Caractéristique, Date et Heure) qui vous permettent de sélectionner une autre caractéristique ou une date/heure différente.

![Le graphe de temps est affiché avec des colonnes représentant le contenu utile et les données perturbées pour l'âge et le nombre de résultats favorables](images/wos-insight-data-detail.png)

## Interprétation du graphe
{: #it-intp}

Le graphe montre plusieurs choses :

- Vous pouvez voir la population qui fait l'objet du biais (les clients âgés de 18 à 23 ans). Le graphe indique également le pourcentage de résultat attendu pour cette population.

- Le graphe indique le pourcentage de résultat attendu (70%) pour la population de référence. Il s'agit de la moyenne de résultat attendu pour toutes les populations de référence.

- Le graphe indique la présence de biais car le rapport du pourcentage de résultats attendus pour les populations âgées de 18 à 23 ans
sur celui pour la population de référence dépasse le seuil. En d'autres termes, 0,52/0,7 = 0,74, qui est inférieur au seuil de 0,8.

- Le graphe montre aussi la distribution des valeurs de référence et surveillée
pour chaque valeur distincte de l'attribut dans les données de la table de contenu utile analysées pour identifier le biais. En d'autres termes, si l'algorithme de détection de biais a analysé les 1790 derniers enregistrements de la table de contenu utile,
120 de ces enregistrements avaient un âge du client entre 18 et 23 ans,
et le graphe à barres représente les résultats `Approved` et `Denied` de cette distribution. La distribution des données de contenu utile est indiquée pour chaque valeur distincte de l'attribut d'équité (même les valeurs de référence sont indiquées). Ces informations permettent de corréler le biais avec la quantité de données reçues par le modèle.

- Le graphe indique également que la population âgée de 31 à 35 ans a reçu 91 % de résultats attendus. Cela donne la source du biais : les données de ce groupe ont faussé les résultats,
elles ont fait augmenter le pourcentage de résultats attendus pour la classe de référence. Ces informations peuvent être utilisées pour identifier des parties des données qui peuvent être ensuite sous-échantillonnées lors de la reformation du modèle.

- Une autre chose importante indiquée par le graphe est le nom de la table qui contient les données identifiées pour un étiquetage manuel. Chaque fois que l'algorithme détectes un biais dans un modèle, il identifie également les points de données
qui peuvent être envoyés pour étiquetage manuel par des humains. Ces données étiquetées manuellement peuvent ensuite être utilisées avec les données de formation initiales pour reformer le modèle. Le modèle reformé n'aura probablement plus le biais. La table d'étiquetage manuel se trouve dans la base de données associée à l'instance de {{site.data.keyword.aios_short}}.
