---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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

# Panoramica sulle metriche di correttezza
{: #anlz_metrics_fairness}

Utilizzare il monitoraggio della correttezza di {{site.data.keyword.aios_full}} per determinare se i risultati prodotti dal modello sono corretti o meno per il gruppo monitorato. Quando il monitoraggio della correttezza è abilitato, genera una serie di metriche ogni ora per impostazione predefinita. È possibile generare queste metriche on-demand facendo clic sul pulsante **Controlla qualità ora** o utilizzando il client Python.
{: shortdesc}

{{site.data.keyword.aios_short}} identifica automaticamente se sono presenti attributi protetti noti in un modello. Quando {{site.data.keyword.aios_short}} rileva tali attributi, raccomanda automaticamente di configurare i monitor della distorsione per ogni attributo presente, per garantire che venga tracciata in produzione la distorsione su tali attributi potenzialmente sensibili.  

Attualmente, {{site.data.keyword.aios_short}} rileva e raccomanda i monitoraggi per i seguenti attributi protetti: 

- sex
- ethnicity
- marital status
- age
- zip code

Oltre a rilevare gli attributi protetti, {{site.data.keyword.aios_short}} consiglia quali valori all'interno di ciascun attributo devono essere impostati come valori monitorati e di riferimento. Così, ad esempio, {{site.data.keyword.aios_short}} raccomanda che all'interno dell'attributo "Sex", il monitor di distorsione sia configurato in modo tale che "Woman" e "Non-Binary" siano i valori monitorati e "Male" sia il valore di riferimento. Se si desidera modificare una delle raccomandazioni, è possibile farlo tramite il pannello di configurazione della distorsione.  

I monitor di distorsione consigliati aiutano a velocizza la configurazione e assicurano che nei modelli AI venga controllata la correttezza rispetto agli attributi sensibili. Poiché i regolatori iniziano ad essere più attenti rispetto alla distorsione algoritmica, è ancora più importante per le organizzazioni capire come funzionano i modelli e se producono risultati scorretti per determinati gruppi. 

Le metriche di correttezza sono calcolate in base alle seguenti informazioni:

- calcolo del punteggio dei dati del payload.

Al fine di un corretto monitoraggio, ogni richiesta di calcolo del punteggio dovrebbe essere registrata anche in {{site.data.keyword.aios_short}}. La registrazione dei dati di payload è automatizzata per i motori {{site.data.keyword.pm_full}}.

Per altri motori di machine learning, i dati del payload possono essere forniti utilizzando il client Python o l'API REST.

Per i motori di machine learning diversi da {{site.data.keyword.pm_full}}, il monitoraggio della correttezza crea ulteriori richieste di calcolo del punteggio sulla distribuzione monitorata.
{: note}

È possibile esaminare tutti i valori di metrica nel tempo sul dashboard {{site.data.keyword.aios_short}}:

![grafico delle metriche di correttezza che mostra la deviazione al di sotto della soglia impostata](images/fairness_metrics_001.png)

È possibile esaminare i dettagli correlati, ad esempio risultati favorevoli e sfavorevoli:

![dettagli correttezza](images/fairness_metrics_002.png)

È possibile visualizzare transazioni dettagliate:

![un grafico della correttezza che mostra un elenco di transazioni](images/fairness_metrics_003.png)

È possibile visualizzare l'endpoint di calcolo del punteggio senza distorsione consigliato:

![dettagli dell'endpoint di calcolo del punteggio senza distorsione](images/fairness_metrics_004.png)

### Metriche di correttezza supportate
{: #anlz_metrics_supfairmets}

Le seguenti metriche di correttezza sono supportate da {{site.data.keyword.aios_short}}:

- [Correttezza per un gruppo](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-quality_group)

I seguenti attributi protetti sono supportati da {{site.data.keyword.aios_short}}: 

- [sex](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-sex)
- [ethnicity](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-ethnicity)
- [marital status](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-marital)
- [age](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-age)
- [zip code](/docs/services/ai-openscale?topic=ai-openscale-quality_group#quality_group-zip)


### Dettagli di correttezza supportati
{: #anlz_metrics_supfairdets}

I seguenti dettagli delle metriche di correttezza sono supportati da {{site.data.keyword.aios_short}}:

- Le percentuali di risultati favorevoli per ciascuno dei gruppi
- Le medie di correttezza per tutti i gruppi di correttezza

```
                           (% di risultati favorevoli nel gruppo monitorato)
Rapporto impatto eterogeneo =  ____________________________________________
                          (% di risultati favorevoli nel gruppo di riferimento)
```

- Distribuzione dei dati per ciascuno dei gruppi monitorati
- Distribuzione dei dati del payload
