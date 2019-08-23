---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"


keywords: deployment, monitoring 

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

# Sélection des déploiements à surveiller
{: #dpl-select}

Pour ajouter des moniteurs au tableau de bord {{site.data.keyword.aios_short}},
vous devez avoir des modèles déployés disponibles via l'un des fournisseurs d'apprentissage automatique que vous avez configurés pour {{site.data.keyword.aios_short}}.
Vous sélectionnez le fournisseur d'apprentissage automatique et les déploiements à surveiller.
{: shortdesc}

## Choix des déploiements
{: #dpl-config}

1.  Dans le tableau de bord de {{site.data.keyword.aios_short}}, cliquez sur **Ajouter au tableau de bord**.
1.  {{site.data.keyword.aios_short}} vérifie vos fournisseurs d'apprentissage automatique pour compiler la liste des modèles déployés. Dans la liste des déploiements, vous pouvez sélectionner ceux que vous souhaitez surveiller.

    ![Fenêtre en incrustation de sélection de déploiements, avec un fournisseur d'apprentissage automatique sélectionné et la liste des déploiements disponibles pour ce fournisseur](images/wos-select-model-deployment.png)

1.  Cliquez sur **Configurer**.

Vous avez sélectionné des déploiements à surveiller.
Vous devez maintenant configurer les moniteurs pour ce modèle. 

## Etapes suivantes
{: #dpl-next}

{{site.data.keyword.aios_short}} est maintenant prêt
à ce que vous [configuriez les moniteurs](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
