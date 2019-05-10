---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-28"

keywords: ai, artificial intelligence, high availability, disaster recovery, recovery, load-balancing, postgres

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

# Alta disponibilità e ripristino di emergenza
{: #openscale-availability-recovery}

{{site.data.keyword.aios_full}} è altamente disponibile all'interno di più ubicazioni {{site.data.keyword.cloud_notm}}, come Dallas e Washington, DC. Tuttavia, il ripristino da potenziali emergenze che influenza un'intera ubicazione richiede pianificazione e preparazione.
{: shortdesc}

Si è responsabili della comprensione della configurazione, della personalizzazione e dell'utilizzo del servizio. Si è anche responsabili di essere in grado di ricreare un'istanza del servizio in una nuova ubicazione e di ripristinare i dati in qualsiasi ubicazione. Vedi [Come garantisco nessun tempo di inattività? ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](/docs/overview?topic=overview-zero-downtime#zero-downtime){: new_window} per ulteriori informazioni. 

##Alta disponibilità 
{: #openscale-high-availability}

{{site.data.keyword.aios_short}} è distribuito e disponibile nei data center **degli Stati Uniti meridionali** con MZR (multiple zone routing) su tre zone di disponibilità. In qualsiasi momento, se una zona non è disponibile, il sistema continuerà ad essere disponibile in altre zone di disponibilità. Il sistema di bilanciamento del carico globale e il server DNS instradano il traffico verso le zone disponibili senza alcuna interruzione dell'utente.

I dati memorizzati nei database PostgreSQL sono anche altamente disponibili e sono presenti in più zone di disponibilità. È comunque responsabilità del cliente eseguire il backup dei dati a sostegno di un piano di ripristino di emergenza in modo che i servizi possano essere ricreati.

Il traffico {{site.data.keyword.aios_short}} è bilanciato su più zone in una regione. Ogni zona è un datacenter nella stessa regione. 

I database Compose, come i database PostgreSQL e <code>etc</code> directory (etcd) distribuiti sono sottoposti periodicamente a backup per garantire un'alta disponibilità e, in caso di disastro, il team operativo di  {{site.data.keyword.aios_short}} sarà in grado di ripristinare il servizio all'interno dell'RPO (Recovery Point Objective).
 
{{site.data.keyword.cloud_notm}} offre la ridondanza dei dati in-regione abilitando la protezione ad alta disponibilità. IBM fornisce la replica automatica dei dati per i database client che contengono dati modello personalizzati e/o di training senza costi aggiuntivi. La replica viene completata tra le zone di disponibilità in-regione all'interno dei data center {{site.data.keyword.cloud_notm}}.
 
## Backup & ripristino
{: #openscale-restore}

I clienti sono responsabili del backup e del ripristino dei propri dati, compresi i dati modello personalizzati e/o di training nonché i modelli personalizzati generati dal cliente. Per le istruzioni di backup e ripristino del cliente, consultare la documentazione di {{site.data.keyword.cloud_notm}}.
 
##Ripristino di emergenza
{: #openscale-disaster-recovery}

La continuità del business in-regione è completata grazie allo sfruttamento della replica automatica tra zone di disponibilità in-regione all'interno dei data center {{site.data.keyword.cloud_notm}}. I clienti sono responsabili del ripristino di emergenza tra più regioni. Le responsabilità includono il backup, il ripristino e la sincronizzazione delle politiche di sicurezza, i dati modello personalizzati e/o di training così come i modelli personalizzati generati dal cliente. Inoltre, il cliente è responsabile dell'instradamento e/o del bilanciamento del carico tra le regioni. Per le istruzioni di backup e ripristino del cliente, consultare la documentazione di {{site.data.keyword.cloud_notm}}.
