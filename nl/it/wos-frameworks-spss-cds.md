---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"


keywords: supported frameworks, models, model types, limitations, limits, spss, c&ds

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
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Framework IBM SPSS C&DS
{: #frmwrks-spss}

{{site.data.keyword.aios_full}} prevede di supportare completamente i seguenti framework di IBM SPSS Collaboration and Deployment Services (C&DS):
{: shortdesc}

Attualmente, il supporto è limitato a {{site.data.keyword.wos4d_full}}.
{: note}

Tabella 1. Dettagli supporto framework

| Framework | Tipo di problema | Tipo di dati |
|:---|:---:|:---:|
| SPSS | Classificazione | Struttura |
{: caption="Dettagli supporto framework" caption-side="top"}

Se `deployment_id` per una sottoscrizione contiene un carattere di sottolineatura, l'accuratezza senza distorsione che normalmente compare sulla scheda Distorsione annullata delle metriche di correttezza, non verrà visualizzata.
{: note}


## Supporto dell'esplicabilità per i framework IBM SPSS Collaboration and Deployment Services (C&DS)
{: #frmwrks-spss-exp-supp}

- L'esplicabilità è supportata per i modelli binari e per i modelli SPSS multiclasse che restituono le probabilità per tutte le classi. 
- L'esplicabilità non è supportata per i modelli SPSS multiclasse che restituono solo la probabilità della classe vincente.



