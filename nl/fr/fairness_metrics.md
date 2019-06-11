---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds

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

# Analyse des métriques et des transactions ![balise bêta](images/beta.png)
{: #anlz_metrics}

{{site.data.keyword.aios_full}} permet d'analyser les métriques et les transactions par divers moyens.
{: shortdesc}

## Matrice de confusion ![balise bêta](images/beta.png)
{: #it-conf-mtx}

Comme détail des métriques de qualité, vous pouvez afficher les enregistrements que le modèle a analysés de manière incorrecte. De telles anomalies peuvent être des faux positifs ou des faux négatifs pour des modèles de classification binaire ou être des affectations de classes incorrectes pour des modèles multi-classes. Vous pouvez également afficher la liste des enregistrements de commentaires que le modèle n'a pas analysés correctement.
{: shortdesc}

1. A partir de l'un des graphiques **Qualité**, tels que **Equité**, cliquez sur une valeur d'heure/jour dans le graphique.
    
    ![Liste des transactions biaisées](images/Confusion_Matrix_040819.004.png)

1. Une matrice de confusion affiche les faux positifs et les faux négatifs. Cliquez sur une cellule pour afficher le sous-ensemble d'enregistrements de commentaires.

    ![Liste des transactions biaisées](images/Confusion_Matrix_040819.005.png)

1. Passez en revue les enregistrements de commentaires et demandez une explication de l'analyse par rapport à l'enregistrement de commentaire.

    ![Liste des transactions biaisées](images/Confusion_Matrix_040819.006.png)

1. Les transactions apparaissent en ligne.

    ![Liste des transactions biaisées](images/Confusion_Matrix_040819.007.png)

