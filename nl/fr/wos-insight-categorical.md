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

# Explication d'un modèle catégoriel
{: #ie-class}

Cet exemple d'explicabilité concerne un modèle de classification binaire qui approuve ou refuse des demandes d'indemnisation au titre d'une assurance. Vous pouvez voir les facteurs qui ont contribué positivement ou négativement au résultat final, `DENIED` (refusé) ici.
{: shortdesc}

C'est la caractéristique *POLICY AGE* (âge du contrat), avec une valeur de `<ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling serviceyear`, qui a eu le plus d'influence dans la décision de refus du modèle. Les autres caractéristiques qui ont contribué à ce résultat sont
*CLAIM FREQUENCY* (fréquence des demandes) (`High`) (élevée) et *AGE* (`18`) ;
*CAR VALUE* (valeur du véhicule) (`$50,000`) n'a eu qu'une influence mineure.

![Explicabilité de classification binaire avec des détails sur les demandes refusées et approuvées](images/insight-explain-binary.png)

Les graphes sont utiles pour voir les facteurs les plus importants dans le résultat d'une transaction,
mais les modèles de classification peuvent également inclure des explications avancées,
détaillées dans les sections `Modifications minimales pour le résultat Approved` et `Modifications minimales pour ce résultat`.

Les explications avancées ne sont pas disponibles pour les modèles de régression, d'image et de texte non structuré.
{: note}

La section `Modifications minimales pour le résultat Approved` nous indique que
si les valeurs des caractéristiques étaient remplacées par celles indiquées, la prévision du modèle changerait.

De même, la section `Modifications minimales pour ce résultat` nous indique que
même si les valeurs des caractéristiques étaient remplacées par celles indiquées, la prévision du modèle ne changerait pas.

Ainsi, ces deux valeurs nous indiquent le comportement du modèle autour du point de données pour lequel l'explication est générée.

![Détails d'explicabilité de classification binaire avec les changements minimaux qui seraient nécessaires pour changer les résultats](images/insight-explain-binary2.png)
