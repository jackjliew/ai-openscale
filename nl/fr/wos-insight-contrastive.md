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

# Les explications contrastives utilisent des positifs pertinents et des négatifs pertinents
{: #ie-pp-pn}

Pour des explications contrastives, {{site.data.keyword.aios_short}} affiche les valeurs positives pertinentes et négatives pertinentes. 
{: shortdesc}

- Les positifs pertinents sont des constatations essentielles à la détermination de ce qu'est une chose.
- Les négatifs pertinents sont des non-constatations qui importent par leur absence.

{{site.data.keyword.aios_short}} affiche toujours un positif pertinent. En revanche, il n'y a pas toujours de négatif pertinent à afficher. Dans ce cas, soit les valeurs de cette caractéristique sont déjà à la médiane, soit la prévision n'a pas changé consécutivement à un éloignement des valeurs de la médiane.

Pour mieux comprendre cela, il faut savoir que lorsque {{site.data.keyword.aios_short}} calcule la valeur du négatif pertinent, il éloigne de leur valeur médiane les valeurs de toutes les caractéristiques. Pour les négatifs pertinents, cela signifie les valeurs des caractéristiques qui sont les plus éloignées de la médiane. Si les valeurs d'un point de données sont déjà à la médiane, ou si la prévision ne change pas même après un éloignement de la valeur de la médiane, c'est qu'il n'y a pas de négatifs pertinents à afficher. Dans le cas des positifs pertinents, {{site.data.keyword.aios_short}} détermine de combien il peut rapprocher les valeurs des caractéristiques de leur médiane sans que la prévision ne change. Dans la pratique, cela signifie qu'il y a presque toujours un positif pertinent pour expliquer une transaction.

